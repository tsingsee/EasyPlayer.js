<template>
  <div id="app">
    <el-row>
      <el-col :span="24">
        <EasyPlayer v-model="videoUrl" :muted="muted" ref="easyPlayer" live :reconnection="true"></EasyPlayer>
        <el-input v-model="input" placeholder="请输入播放地址" size="mini"></el-input>
        <p>列如：http://127.0.0.1:10800/test.flv <a href="http://www.easydarwin.org/easyplayer/" target="_blank"> 在线演示</a></p>
        <el-button class="player-button" size="mini" type="success" @click="player">播放</el-button>
        <div style="display: flex;flex-direction: row;margin-top: 30px">
          <el-button size="mini" type="primary" @click="play">播放</el-button>
          <el-button size="mini" type="primary" @click="saveSnap">快照</el-button>
          <el-button size="mini" type="primary" @click="videotape">{{startVideotape? "停止录像":"开始录像"}}</el-button>
          <el-button size="mini" type="primary" @click="switchAudio">{{muted ? '开始声音' : '静音'}}</el-button>
          <el-button size="mini" type="primary" @click="fullScreen">全屏</el-button>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  import EasyPlayer from "@easydarwin/easyplayer"
  export default {
    data() {
      return {
        videoUrl: '',
        input: '',
        startVideotape:false,
        muted:true
      }
    },
    components: {
      EasyPlayer
    },
    mounted() {},
    methods: {
      player() {
        if(!this.input){
          this.$message.error('请输入播放地址地址！');
        }else{
          this.videoUrl = this.input
        }
      },
      //保存快照
      saveSnap(){
        if(!this.videoUrl){
          this.$message.error('请输入播放地址地址！');
        }else{
          this.$refs.easyPlayer.saveLocalSnapshot()
        }
      },
      //录像
      videotape(){
        if(!this.videoUrl){
          this.$message.error('请输入播放地址地址！');
        }else{
          if(this.$refs.easyPlayer.switchRecording){
            this.$refs.easyPlayer.switchRecording()
            this.startVideotape = !this.startVideotape
          }
        }
      },
      play(){
        this.$refs.easyPlayer.play()
      },
      pause(){
        this.$refs.easyPlayer.pause()
      },
      switchAudio(){
        this.$refs.easyPlayer.switchAudio()
        this.muted = !this.muted
      },
      fullScreen(){
        this.$refs.easyPlayer.fullscreen()
      }
    }
  }
</script>

<style lang="scss">
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    // text-align: center;
    color: #2c3e50;
  }

  .el-row,
  .div-btn {
    max-width: 800px;
    margin: auto;
  }

  .div-btn {
    padding: 5px 0;
  }

  .el-col {
    min-height: 300px;
    // border: 1px pink solid
    .easy-player {
      height: 500px !important;
    }
  }

  .el-input {
    padding: 5px;
    box-sizing: border-box;
  }

  .player-button {
    margin: 5px;
    width: 100%;
  }
  p {
    font-size: 12px;
    color: #67c23a;
  }
  .el-input__inner:focus {
    border-color: #67c23a !important;
  }
</style>