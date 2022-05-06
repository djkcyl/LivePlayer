<template>
  <div class="px-5 mx-auto mt-5 justify-center container">
    <input type="text" v-model="room" />
    <input type="checkbox" name="rtc" id="rtc" v-model="irtc">
    <video v-show="irtc" id="video-webrtc" controls></video>
    <div  v-show="!irtc" id="video-flv"></div>
  </div>
</template>

<script lang="ts" setup>
import DPlayer from "dplayer";
import { onMounted, ref, watch } from "vue";

let room = ref("djkcyl");
let irtc = ref(false);

watch(room, () => apply());
watch(irtc, () => apply());

onMounted(() => apply());

function apply() {
  const rtc = "webrtc://a60.one/live/" + room.value;
  const flv = `http://a60.one:8090/live/${room.value}.flv`;
  const video = document.getElementById("video-webrtc");
  const video2 = document.getElementById("video-flv");
  if (irtc.value) {
    const player = new JSWebrtc.Player(rtc, {
      video: video,
      autoplay: true
    });
  } else {
    const dp = new DPlayer({
      container: video2,
      autoplay: true,
      video: {
        name: "flv",
        url: flv,
        type: "flv",
      },
    });
  }
}
</script>
