<template>
  <div class="px-5 m-auto mt-5 flex justify-center">
    <video id="video-webrtc" controls></video>
  </div>
</template>

<script lang="ts" setup>
import { onMounted, ref } from "vue";

const room = ref("djkcyl");
onMounted(() => {
  const video = document.getElementById("video-webrtc");
  const player = new JSWebrtc.Player("webrtc://a60.one/live/" + room.value, {
    video: video,
    autoplay: true,
    onPlay: () => {
      document.title = "▶️ 当前直播 " + room.value;
    },
  });
});
</script>
