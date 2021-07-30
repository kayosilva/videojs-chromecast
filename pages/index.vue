<template>
  <video ref="vjs" class="video-js" height="360" width="640"></video>
</template>

<script>
import videojs from "video.js";
import chromecast from "@silvermine/videojs-chromecast";
import "video.js/dist/video-js.css";
import "@silvermine/videojs-chromecast/dist/silvermine-videojs-chromecast.css";

export default {
  data() {
    return {
      player: null,
    };
  },
  mounted() {
    const options = {
      controls: true,
      techOrder: ["chromecast", "html5"], // You may have more Tech, such as Flash or HLS
      plugins: {
        chromecast: {},
      },
      sources: [
        {
          src:
            "http://www.caminandes.com/download/03_caminandes_llamigos_1080p.mp4",
          type: "video/mp4",
        },
      ],
    };

    this.player = videojs(this.$refs.vjs, options);
    this.player.chromecast();

    //console.log("vjs version", videojs.VERSION);
    //chromecast(videojs);
    /*this.player = videojs(this.$refs.vjs, {
      autoplay: false,
      controls: true,
      techOrder: ["chromecast", "html5"],
      plugins: {
        chromecast: {},
      },
      sources: [
        {
          src:
            "http://www.caminandes.com/download/03_caminandes_llamigos_1080p.mp4",
          type: "video/mp4",
        },
      ],
    });*/
  },
  head() {
    return {
      script: [
        {
          src:
            "https://www.gstatic.com/cv/js/sender/v1/cast_sender.js?loadCastFramework=1",
        },
      ],
    };
  },
  beforeDestroy() {
    if (this.player) {
      this.player.dispose();
    }
    this.player = null;
  },
};
</script>
