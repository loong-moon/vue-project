<template>
  <div class="player">
    <video id="my-video" ref="video" class="video-js" width="600" height="300">
      <source src="http://localhost:8090/dahai/index.mpd" type='application/dash+xml' />
      <p class="vjs-no-js">
        观看视频请启用JavaScript，并且把浏览器升级到
        <a href="http://videojs.com/html5-video-support/" target="_blank">支持HTML5 video</a>
      </p>
    </video>
  </div>
</template>


<script>
import videojs from 'video.js'
import 'videojs-contrib-dash'
import 'video.js/dist/video-js.css'
export default {
    name: 'DashPlayer',
    data () {
        return {
            tokens: null
        }
    },
    mounted () {
        this.initPlayer()
    },
    methods: {
        initPlayer () {
            var myCustomCallback = function (player, mediaPlayer) {
                // Log MediaPlayer messages through video.js
                if (videojs && videojs.log) {
                    mediaPlayer.getDebug().setLogToBrowserConsole(false)
                    //               mediaPlayer.on('log', function (event) {
                    //                videojs.log(event.message)
                    //               })
                }
            }
            videojs.Html5DashJS.hook('beforeinitialize', myCustomCallback)

            videojs(this.$refs.video, {
                controls: true,
                autoplay: false,
                preload: 'auto'
            })
        }
    }
}
</script>

<style lang="scss" scoped>

</style>
