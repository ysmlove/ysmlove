- 👋 Hi, I’m @ysmlove
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
ysmlove/ysmlove is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
</template>

<script>
import { mapState } from 'vuex'
import Bus from 'web/common/live-source/bus.js'
export default {
  name: 'Player',
        loop: false,
        btn_text: '',
        fullScreenFlag: false,
        hasDanMu: false,
        hasDanMu: true,
        closedanmu: true,
        showBtnTimeOut: null,
        csdnPlayerDom: ''
      }
    }
  },
  computed: {
    ...mapState(['pageData']),
    isNode () {
      return EASY_ENV_IS_NODE
    },
    cId () {
      return this.$route.params.courseId
    },
    userInfo () {
      return this.pageData.data['edu-user-info'] || {}
    },
    showDisabled () {
      return this.checkBug === ''
    },
        })
    },
    setVideoFun () {
      // 计算视频可视范围 距离顶部距离
      // 1根据宽度可视范围高度 计算 16*9 16*10  4*3
      function getVideoSize (ele) {
        ele = document.querySelector('#videoPlayer')
        let containerHeight = ele.offsetHeight
        let containerWidth = ele.offsetWidth
        let videoHeight = containerWidth * 9 / 16
        let vtop = (containerHeight - videoHeight) / 2
        let vbottom = vtop + videoHeight
        return { vtop, vbottom, vwidth: containerWidth }
      }
      function randomNum (min, max) {
        return Math.floor(Math.random() * (max - min) + min)
      }
      const danmuInterval = 16 // s
      let danmun = { // 发送弹幕
        duration: (danmuInterval - 1) * 1000,
        id: 'id',
        start: 5000, // 不提供该项则立即发送
        txt: this.userInfo.userName,
        mode: 'scroll',
        style: {
          color: '#fff',
          margin: '314px 0 0',
          opacity: 0.6,
          filter: 'alpha(opacity=60)',
          textShadow: '0 0 0.2em #000',
          fontSize: '16px'
        }
      }
      let { vtop, vbottom, vwidth } = getVideoSize()
      let newsize
      let mtop = 0 // 弹幕位置
      let danmuId = 1
      let sendDanduTime = 0
      let danmuStart = false
      console.log('当前时间', this.currentMaterialItem.currViewTime)
      console.log('当前csdnPlayer', this.$refs.csdnPlayer)
      if (this.$refs.csdnPlayer) {
        this.csdnPlayerDom.focus()
        this.$refs.csdnPlayer.player.on('play', (e) => {
          console.log('开始了')
          if (!danmuStart) {
            danmuStart = true
            this.$refs.csdnPlayer.player.danmu.start()
          }
          console.log(this.currentMaterialItem.currViewTime)
          if (this.totalTimeNeedUpdate && e.duration > 1) {
            this.totalTimeNeedUpdate = false
        })
        this.$refs.csdnPlayer.player.on('timeupdate', e => {
          const curSeconds = parseInt(e.currentTime)
                // console.log('curSeconds is ', curSeconds)
          let playbackrate = Number(sessionStorage.getItem('playbackrate') || 1)
          playbackrate = playbackrate > 1 ? playbackrate : 1
          if (curSeconds > 0 && curSeconds % (danmuInterval * playbackrate) === 0 && curSeconds !== sendDanduTime && danmuStart) {
            newsize = getVideoSize()
            if (newsize.vwidth !== vwidth) {
              vwidth = newsize.vwidth
              vtop = newsize.vtop
              vbottom = newsize.vbottom
              // console.log('video width change', videoWidth)
              this.$refs.csdnPlayer.player.danmu.pause() // 更新容器宽度位置
              this.$refs.csdnPlayer.player.danmu.play()
            }
            console.log('sendDanduTime ', curSeconds)
            sendDanduTime = curSeconds
            danmun = JSON.parse(JSON.stringify(danmun))
            mtop = randomNum(vtop, vbottom - 30)
            danmun.style.margin = `${mtop}px 0 0`
            danmun.id = ++danmuId
            danmun.start = (sendDanduTime + 1) * 1000
            this.$refs.csdnPlayer.player.danmu.sendComment(danmun)
            setTimeout(() => { this.$refs.csdnPlayer.player.danmu.removeComment(danmuId - 1) }, 2000) // 2s移除上一个 避免重复出现
          }
                // if (e.currentTime !== 0) {
                //   that.currentMaterialItem.currViewTime = curSeconds
                // }
  right: 20px;
  cursor: pointer;
  text-align: center;
  z-index: 11;
}
.uploadBtn:hover {
  color: #fff;
