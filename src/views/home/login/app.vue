<template>
  <div class="login">
    <div class="login-info">
      <img :src="logo" alt />
      <p>宁波二次供水智慧管理</p>
    </div>
    <div class="login-form">
      <h3>登录</h3>
      <div class="form-cont">
        <div>
          <img :src="userIcon" alt />
          <input type="text" v-model="form.username" placeholder="请输入您的用户名" />
        </div>
        <div>
          <img :src="pwdIcon" alt />
          <input type="password" v-model="form.password" placeholder="请输入您的密码" />
        </div>
      </div>
      <button class="login-btn" @click="login">登录</button>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
import userIcon from "./img/user-icon.png";
import pwdIcon from "./img/pwd-icon.png";
import logo from "./img/logo.png";
export default {
  data() {
    return {
      userIcon,
      pwdIcon,
      logo,
      form: {
        username: "",
        password: ""
      }
    };
  },
  methods: {
    login() {
      this.api.getSysLogin(this.form).then(res => {
        if (res.code === 200) {
          this.$hero.msg.show({
            text: "登录成功"
          });
          setTimeout(() => {
            this.until.href("./index.html");
          }, 1500);
        }
      });
    }
  },
  components: {}
};
</script>

<style scoped lang="less">
.login {
  width: 100%;
  height: 100%;
  background: url("./img/bg.png") no-repeat;
  background-size: cover;
  position: relative;
  .login-info {
    position: absolute;
    top: 16%;
    width: 80%;
    left: 10%;
    display: flex;
    display: -webkit-flex;
    flex-flow: row nowrap;
    align-items: center;
    img {
      width: 30px;
    }
    p {
      flex: 1;
      margin-left: 0.4rem;
      color: #fff;
      font-size: 22px;
      font-weight: 700;
    }
  }
  .login-form {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 80%;
    height: 5.8rem;
    transform: translate3d(-50%, -50%, 0);
    background-color: rgba(0, 0, 0, 0.3);
    h3 {
      font-size: 18px;
      padding: 0.6rem 0;
      color: #fff;
      text-align: center;
    }
    .form-cont {
      width: 80%;
      margin: 0 auto;
      > div {
        display: flex;
        display: -webkit-flex;
        flex-flow: row nowrap;
        padding: 0.2rem 0.3rem;
        background-color: #fff;
        border-radius: 0.1rem;
        &:nth-of-type(1) {
          margin-bottom: 0.6rem;
        }
        img {
          width: 0.3rem;
        }
        input {
          flex: 1;
          margin-left: 0.2rem;
          padding-left: 0.2rem;
          border: 0;
          outline: none;
          border-left: 1px solid #cacaca;
        }
      }
    }
    .login-btn {
      width: 80%;
      margin: 1rem 0 0 10%;
      line-height: 0.8rem;
      height: 0.8rem;
      background-color: #01aef0;
      color: #fff;
      border: 0;
      border-radius: 0.6rem;
      font-size: 20px;
    }
  }
}
</style>
