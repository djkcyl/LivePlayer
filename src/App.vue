<template>
  <div class="px-5 m-auto mt-5 flex justify-center">
    <input type="text" v-model="room" />
    <input type="radio" name="rtc" id="rtc">
    <input type="radio" name="flv" id="flv">
    <video id="video-webrtc" controls></video>
  </div>
</template>

<script lang="js" setup>
import { onMounted, ref, watch } from "vue";
import DPlayer from 'dplayer';

let room = ref("djkcyl");
watch(room,()=>{
  const video = document.getElementById("video-webrtc");
  const dp = DPlayer({
    container: video,
video:{
url:room
}
  });
})
</script>
