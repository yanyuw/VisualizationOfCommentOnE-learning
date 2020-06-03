<template>
    <div class="screenBtn">
        <img src="../assets/fullscreen.png" v-show="!isFullscreen" v-on:click="screen"/>
        <img src="../assets/outfullscreen.png" v-show="isFullscreen" v-on:click="screen"/>
    </div>
</template>

<script>
export default {
  name: "FullscreenBtn",
  data(){
      return {
          isFullscreen: false
      }
  },
  methods: {
    screen() {
      let element = document.documentElement;
      if (this.isFullscreen) {
        if (document.exitFullscreen) {
          document.exitFullscreen();
        } else if (document.webkitCancelFullScreen) {
          document.webkitCancelFullScreen();
        } else if (document.mozCancelFullScreen) {
          document.mozCancelFullScreen();
        } else if (document.msExitFullscreen) {
          document.msExitFullscreen();
        }
      } else {
        if (element.requestFullscreen) {
          element.requestFullscreen();
        } else if (element.webkitRequestFullScreen) {
          element.webkitRequestFullScreen();
        } else if (element.mozRequestFullScreen) {
          element.mozRequestFullScreen();
        } else if (element.msRequestFullscreen) {
          // IE11
          element.msRequestFullscreen();
        }
      }
      this.isFullscreen = !this.isFullscreen;
    }
  }
};
</script>

<style >
.screenBtn{
    position: absolute;
    top: 20px;
    right: 20px;

}
</style>
