<template>
  <div id="app">
    <div class="layui-container">
      <form class="layui-form" action="">
        <div class="layui-form-item">
          <label class="layui-form-label">输入框</label>
          <div class="layui-input-block">
            <input type="text" name="title" required  lay-verify="required" placeholder="请输入标题" autocomplete="off" class="layui-input">
          </div>
        </div>
        <div class="layui-form-item">
          <label class="layui-form-label">密码</label>
          <div class="layui-input-block">
            <input type="password" name="title" required  lay-verify="required" placeholder="请输入密码" autocomplete="off" class="layui-input">
          </div>
        </div>    <div class="layui-form-item">
        <label class="layui-form-label">验证码</label>
        <div class="layui-input-inline">
          <input type="password" name="password" required lay-verify="required" placeholder="请输入验证码" autocomplete="off" class="layui-input">
        </div>
        <div class="layui-form-mid layui-word-aux" v-html="svgUrl" @click="getCaptcha" style="position: relative; top: -15px;">

        </div>
      </div>
        <button type="button" class="layui-btn">点击登录</button>
        <a href="http://www.layui.com" class="imooc-link">忘记密码?</a>
      </form>
    </div>

  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'app',
  data(){
    return {
      svgUrl: ''
    }
  },
  mounted() {
    this.getCaptcha()
  },
  methods:{
    getCaptcha(){
      axios.get('http://127.0.0.1:4000/getCaptcha').then(res => {
        if(res.data.code == 200){
          this.svgUrl = res.data.data
        }
      })
    }
  }
}
</script>
<style lang="scss" scoped>
#app {
  background: #f2f2f2;
}
.layui-container{
  background: #ffff;
}
input{
  width: 190px;
}
.imooc-link{
  margin-left: 20px;
  &:hover{
    color: #42b983;
  }
}
</style>
