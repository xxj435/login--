<template>
  <div id="app">
    <div class="layui-container">
      <form
        class="layui-form"
        action=""
      >
        <div
          class="layui-form-item"
          :class="{'form-group--error': $v.name.$error}"
        >
          <label class="layui-form-label">用户名</label>
          <div class="layui-input-inline">
            <input
              type="text"
              name="title"
              required
              lay-verify="required"
              placeholder="请输入标题"
              autocomplete="off"
              class="layui-input"
              v-model.trim="name"
            >
          </div>
          <div
            class="error"
            v-if="!$v.name.required"
          >
            用户名不得为空
          </div>
          <div
            class="error"
            v-if="!$v.name.email"
          >
            用户名输入为邮箱格式
          </div>
        </div>
        <div
          class="layui-form-item"
          :class="{'form-group--error': $v.password.$error}"
        >
          <label class="layui-form-label">密码</label>
          <div class="layui-input-block">
            <input
              type="password"
              name="title"
              required
              lay-verify="required"
              placeholder="请输入密码"
              autocomplete="off"
              class="layui-input"
              v-model="password"
            >
          </div>
        </div>
        <div
          class="layui-form-item"
          :class="{'form-group--error': $v.code.$error}"
        >
          <label class="layui-form-label">验证码</label>
          <div class="layui-input-inline">
            <input
              type="password"
              name="password"
              required
              lay-verify="required"
              placeholder="请输入验证码"
              autocomplete="off"
              class="layui-input"
              v-model="code"
            >
          </div>
          <div
            class="layui-form-mid layui-word-aux"
            v-html="svgUrl"
            @click="getCaptcha"
            style="position: relative; top: -15px;"
          >

          </div>
        </div>
        <button
          type="button"
          class="layui-btn"
          @click="checkForm"
        >点击登录</button>
        <a
          href="http://www.layui.com"
          class="imooc-link"
        >忘记密码?</a>
      </form>
    </div>

  </div>
</template>
<script>
import axios from "axios";
import { required, email } from "vuelidate/lib/validators";
export default {
  name: "app",
  data() {
    return {
      svgUrl: "",
      name: "",
      password: "",
      code: "",
      errorMsg: [],
    };
  },
  validations: {
    name: {
      required,
      email,
    },
    password: {
      required,
    },
    code: {},
  },
  mounted() {
    this.getCaptcha();
  },
  methods: {
    getCaptcha() {
      axios.get("http://127.0.0.1:4000/getCaptcha").then((res) => {
        if (res.data.code == 200) {
          this.svgUrl = res.data.data;
        }
      });
    },
    checkForm() {
      this.errorMsg = [];
      if (!this.name.trim()) {
        this.errorMsg.push("登录名为空");
      }
      if (!this.password.trim()) {
        this.errorMsg.push("密码为空");
      }
      if (!this.code.trim()) {
        this.errorMsg.push("验证码为空");
      }
      console.log(this.errorMsg);
    },
  },
};
</script>
<style lang="scss" scoped>
#app {
  background: #f2f2f2;
}
.layui-container {
  background: #ffff;
}
input {
  width: 190px;
}
.imooc-link {
  margin-left: 20px;
  &:hover {
    color: #42b983;
  }
}
</style>
