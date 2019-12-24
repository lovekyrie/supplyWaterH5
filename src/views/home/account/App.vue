<template>
  <div id="container">
    <main-header :title="title"></main-header>
    <div class="account">
      <div class="avatar-info">
        <div class="avatar-img">
          <img :src="avatar" alt />
        </div>
        <div class="user-info">
          <div>
            <p>
              <span>巡检人员：</span>
              <span>张尚三</span>
            </p>
            <p>
              <span>手机号码：</span>
              <span>15547865421</span>
            </p>
            <p>
              <span>巡检单位：</span>
              <span>太平洋水处理工程有限公司</span>
            </p>
          </div>
          <img :src="arrow" alt />
        </div>
      </div>
      <div class="change-pwd">
        <img :src="changePwd" alt />
        <div>
          <p>修改密码</p>
          <img :src="arrow" alt />
        </div>
      </div>
      <div class="about-us">
        <img :src="aboutUs" alt />
        <div>
          <p>关于我们</p>
          <img :src="arrow" alt />
        </div>
      </div>
      <div class="operate">
        <button @click="quit">退出</button>
      </div>
    </div>
    <tab cd="user"></tab>
  </div>
</template>

<script type="text/ecmascript-6">
import aboutUs from "./img/about-us.png";
import arrow from "./img/arrow-right.png";
import avatar from "./img/avatar.png";
import changePwd from "./img/change-pwd.png";

export default {
  data() {
    return {
      title: "账号",
      aboutUs,
      arrow,
      avatar,
      changePwd
    };
  },
  methods: {
    quit() {
      this.api.getSysLoginOut().then(res => {
        if (res.code === 200) {
          this.$hero.msg.show({
            text: "退出成功"
          });
          setTimeout(() => {
            this.until.href("./login.html");
          }, 1500);
        }
      });
    }
  },
  components: {}
};
</script>

<style scoped lang="less">
@import "../../../assets/css/mobile.less";
#container {
  width: 100%;
  background: @bgColor;
  height: 100%;
  display: flex;
  display: -webkit-flex;
  flex-direction: column;
  .account {
    width: 100%;
    height: 100%;
    > div {
      background-color: #fff;
    }
    .avatar-info {
      padding: 0.5rem 0.35rem 0.7rem;
      display: flex;
      display: -webkit-flex;
      flex-flow: row nowrap;
      align-items: center;
      .avatar-img {
        width: 1.5rem;
        border: 0;
        border-radius: 50%;
        img {
          width: auto;
          height: auto;
          max-width: 100%;
          max-height: 100%;
          vertical-align: middle;
        }
      }
      .user-info {
        margin-left: 0.3rem;
        flex: 1;
        display: flex;
        display: -webkit-flex;
        flex-flow: row nowrap;
        align-items: center;
        div {
          flex: 1;
          font-size: .24rem;
          p {
            &:not(:nth-of-type(1)) {
              margin-top: 0.1rem;
            }
          }
        }
        img {
          margin-left: 0.3rem;
          width: 0.12rem;
          height: 0.22rem;
        }
      }
    }
    .change-pwd,
    .about-us {
      margin-top: 0.1rem;
      padding: 0.4rem;
      display: flex;
      display: -webkit-flex;
      flex-flow: row nowrap;
      img {
        width: 0.4rem;
        height: 0.4rem;
      }
      div {
        flex: 1;
        margin-left: 0.3rem;
        display: flex;
        display: -webkit-flex;
        flex-flow: row nowrap;
        align-items: center;
        p {
          flex: 1;
        }
        img {
          width: 0.12rem;
          height: 0.22rem;
        }
      }
    }
    .operate {
      width: 60%;
      margin: 20% auto 0;
      background-color: #f2f3f7;
      transform: translateY(-50%);
      button {
        width: 100%;
        height: 1rem;
        line-height: 1rem;
        border: 1px solid #ddd;
        border-radius: 0.2rem;
        color: #999;
        font-size: 16px;
      }
    }
  }
}
</style>
