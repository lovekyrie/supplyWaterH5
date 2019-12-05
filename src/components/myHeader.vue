<style lang="less" scoped>
    @import "../assets/css/mobile.less";
    .header{
        width: 100%;
        display: flex;
        display: -webkit-flex;
        height: 1rem;
        align-items: center;
        background: #1177B9;
        padding: 0 0.3rem;
        box-sizing: border-box;
        >img{
            width: auto;
            height: 0.4rem;
            &:last-of-type{
            }
        }
        .search{
            flex: 1;
            background: rgba(255,255,255,0.3);
            border-radius: 0.25rem;
            height: 0.5rem;
            display: flex;
            display: -webkit-flex;
            align-items: center;
            padding: 0 0.2rem;
            margin: 0 0.3rem;
            color: #ffffff;
            >img{
                width: 0.3rem;
                margin-right: 0.1rem;
            }
        }
    }
</style>

<template>
    <div class="header">
        <img :src="logo"/>
        <div class="search">
            <img :src="search"/>
            搜索泵房名称
        </div>
        <img :src="ma" @click="toMa"/>
    </div>
</template>

<script>
    import logo from './img/logo.png'
    import search from './img/search.png'
    import ma from './img/ma.png'

  export default {

    data() {
      return {
          logo,
          search,
          ma
      }
    },
    mounted() {
    },
    methods: {
        toMa(){
            this.app.InterfaceName('h5_scanning', {})
                .then(res => {
                    console.log(res)
                    // res = JSON.parse(res);
                    // if(res.status=='200'){
                    //
                    // }else {
                    //
                    // }

                }, err => {
                    this.$toast({
                        message: err,
                        iconClass: 'mint-toast-icon mintui mintui-field-warning'
                    });
                });
        }
    }
  }
</script>