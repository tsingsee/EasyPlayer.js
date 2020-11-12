<template>
  <div id="app">
    <el-row>
      <el-col :span="24">
        <EasyPlayer :videoUrl="videoUrl" fluent autoplay live stretch></EasyPlayer>
        <el-input v-model="input" placeholder="请输入播放地址" size="mini"></el-input>
        <p>列如：http://127.0.0.1:10800/test.flv <a href="http://www.easydarwin.org/easyplayer/" target="_blank"> 在线演示</a></p>
        <el-button class="player-button" size="mini" type="success" @click="player">播放</el-button>
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
        input: ''
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