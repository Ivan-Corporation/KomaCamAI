<template>
  <div>
    <div>
      <div>
        <h1>KomCam Objects Detector <v-icon icon="mdi-camera-control" size="sm"/></h1>
        <p>Bring objects from the <a style="cursor: pointer;" @click="$emit('change-tab-three')">list</a> to your camera (Need permission)</p>
        <div v-if="!showBtn" style="margin-top: 35%; margin-bottom: 35%;">
          <v-progress-circular color="blue-lighten-3" indeterminate :size="52"></v-progress-circular>
          
        </div>
        <section ref="demosSection" v-if="showBtn">
          <p></p>
          <div ref="liveView" class="camView">
            <v-btn
              v-if="!camStarted"
              prepend-icon="mdi-webcam"
            
              @click="enableCam"
            >
              Enable Webcam
            </v-btn>
            
            <video
              ref="video"
              autoplay
              muted
              style="height: 550px; width: 100%"
            ></video>
          </div>
          <div v-if="camStarted">
          <p>On your camera detected:</p>
          <p ref="onTheScreen" style="height: 250px" class="detected"></p>
        </div>
          
          <audio ref="audio">
            <source :src="alarm" type="audio/wav"/>
            Your browser does not support the audio element.
          </audio>
          <audio ref="audioPhone">
            <source :src="phone_sound" type="audio/wav"/>
            Your browser does not support the audio element.
          </audio>
        </section>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import "@tensorflow/tfjs-backend-cpu";
import "@tensorflow/tfjs-backend-webgl";
import * as cocoSsd from "@tensorflow-models/coco-ssd";
import alarm from "../assets/sounds/person2.wav";
import phone_sound from "../assets/sounds/phone.wav";

defineProps({
  tab: String,
})

const video = ref(null);
const liveView = ref(null);
const demosSection = ref(null);
const onTheScreen = ref(null);
const audio = ref(null);
const audioPhone = ref(null);
const showBtn = ref(false);
const camStarted = ref(false);

let model = undefined;



//loading the model
cocoSsd.load().then(function (loadedModel) {
  model = loadedModel;
  showBtn.value = true;
});

async function enableCam(event) {
  if (!model) {
    return;
  }
  camStarted.value = true;
  const constraints = {
    video: true,
  };

  // Activate the webcam stream.
  await navigator.mediaDevices
    .getUserMedia(constraints)
    .then(function (stream) {
      try {
        video.value.srcObject = stream;
        console.log("try", stream);
      } catch (error) {
        console.log("catch", error);
      }

      video.value.addEventListener("loadeddata", predictWebcam);
    });
}

const children2 = ref([]);
function predictWebcam() {
  //classifying a frame in the stream.
  model.detect(video.value).then(function (predictions) {
    for (let i = 0; i < children2.value.length; i++) {
      onTheScreen.value.removeChild(children2.value[i]);
    }

    children2.value.splice(0);

    // loop through predictions
    for (let n = 0; n < predictions.length; n++) {
      if (predictions[n].score > 0.47) {
        const div = document.createElement("div");
        div.innerHTML = predictions[n].class;
        //check if prediction class is person to play alarm
        if (predictions[n].class == "person") {   
            audio.value.play();
        }
        if (predictions[n].class == "cell phone") {       
            audioPhone.value.play();
        }
        onTheScreen.value.appendChild(div);
        // console.log(onTheScreen.value)
        children2.value.push(div);
      }
    }

    // Call this function again to keep predicting when the browser is ready.
    window.requestAnimationFrame(predictWebcam);
  });
}
</script>

<style scoped>
body {
  font-family: helvetica, arial, sans-serif;
  margin: 2em;
  color: #3d3d3d;
}

video {
  display: block;
}

section {
  opacity: 1;
  transition: opacity 500ms ease-in-out;
}

.camView {
  position: relative;
  float: left;
  width: calc(100% - 20px);
  margin: 10px;
  cursor: pointer;
  filter: drop-shadow(0 0 0.5em rgb(11, 132, 145));

}

.detected {
    text-transform: capitalize;
    font-size: 16px;
    font-weight: 500;
}

</style>
