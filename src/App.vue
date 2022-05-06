<template>
  <div class="mx-auto max-w-7xl xl:mt-5 justify-center container">
    <video v-show="irtc" class="min-w-full" id="video-webrtc" controls></video>
    <div v-show="!irtc" id="video-flv"></div>
    <div class="mx-4 mt-4 flex justify-between">
      <div>
        <span class="label-text">房间号：</span>
        <input type="text" class="input input-bordered max-w-xs" v-model="room" />
      </div>
      <label class="label cursor-pointer">
        <span class="label-text">WebRTC Mode：</span>
        <input type="checkbox" name="rtc" id="rtc" v-model="irtc" class="toggle" checked />
      </label>
    </div>
  </div>
</template>

<script lang="ts" setup>
import DPlayer from "dplayer";
import { onMounted, ref, watch } from "vue";

let room = ref("djkcyl");
let irtc = ref(true);

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
