<template>
  <div class="account">
    <div class="operate">
      <button @click="quit">退出</button>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
  data() {
    return {};
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
.account {
  .operate {
    width: 60%;
    margin: 50% auto;
    transform: translateY(-50%);
    button {
      width: 100%;
      height: 1rem;
      line-height: 1rem;
      border: 0;
      border-radius: 0.2rem;
      background-color: #01aef0;
      color: #fff;
      font-size: 16px;
    }
  }
}
</style>
