<template>
  <div id="app">
    <el-row>
      <el-col :span="24">
        <h4>H265播放器</h4>
        <div class="player-box">
          <div id="wasmPlayer"></div>
        </div>
        <el-input v-model="input" placeholder="请输入播放地址接口" size="mini"></el-input>
        <p>列如：http://127.0.0.1:8080/flv/hls/stream.flv</p>
        <el-button class="player-button" size="mini" type="success" @click="play">播放</el-button>
      </el-col>
    </el-row>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        input: '',      //地址栏
        player: ''      //播放器对象
      }
    },
    mounted() {
      //实例化播放器
      this.player = new WasmPlayer(null, 'wasmPlayer', this.callbackfun,{
        Height:true
      })
    },
    methods: {
      // 播放事件
      play() {
        if(!this.input){
          this.$message.error('请输入接口地址！');
        }else{
          this.player.play(this.input,1);
        }
      },
      //回调函数
      callbackfun(e) { 
        console.log(e);
      }
    }
  }
</script>

<style lang="scss">
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
  }
  .el-row,
  .el-col {
    min-height: 300px;
    max-width: 600px;
    margin: auto;
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
  .player-box {
    height: 400px;
    width: 600px;
    margin: auto;
    margin-top: 2%;
    border: 1px solid #eee;
  }
  .el-input__inner:focus {
    border-color: #67c23a !important;
  }
</style>