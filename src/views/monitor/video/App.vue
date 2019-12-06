

<template>
  <div id="container">
    <video-show @close="close" v-if="videoShow" :url="videoUrl"></video-show>
    <main-header :title="title"></main-header>
    <div class="menu">
      <div>
        <input type="text" v-model="cameraName" placeholder="请输入小区名称" />
        <mt-button @click="search" type="primary" size="small">搜索</mt-button>
      </div>
    </div>
    <div
      class="main"
      v-infinite-scroll="loadMore"
      infinite-scroll-disabled="loading"
      infinite-scroll-distance="10"
    >
      <list :list="list" @videoPlay="videoPlay" :canPlayer="canPlay"></list>
      <p v-if="!total" class="noData">数据全部加载完</p>
    </div>
  </div>
</template>

<script>
import list from "@/components/monitorList";
import videoShow from "@/components/videoShow";
export default {
  data() {
    return {
      videoUrl: "",
      loading: false,
      canPlay: true,
      pageNo: 1,
      pageSize: 10,
      total: 0,
      search: {
        zone: "",
        site: "",
        dataType: ""
      },
      videoShow: false,
      title: "水厂数据（4）",
      zoneList: [
        {
          label: "分区1",
          value: "zone1"
        },
        {
          label: "分区2",
          value: "zone2"
        },
        {
          label: "分区3",
          value: "zone3"
        }
      ],
      site: [
        {
          label: "站点1",
          value: "site1"
        },
        {
          label: "站点2",
          value: "site2"
        },
        {
          label: "站点3",
          value: "site3"
        }
      ],
      dataType: [
        {
          label: "数据1",
          value: "dataType1"
        },
        {
          label: "数据12",
          value: "dataType2"
        },
        {
          label: "数据13",
          value: "dataType3"
        }
      ],
      list: []
    };
  },
  components: {
    list,
    videoShow
  },
  watch: {
    search: {
      deep: true,
      handler: function(e) {
        this.loading = false;
        console.log(e);
      }
    }
  },
  created() {},
  mounted() {
    this.getList();
  },
  methods: {
    search() {
      this.pageNo = 1;
      this.list = [];
      this.getList();
    },
    async getList() {
      const qry = new this.Query();
      qry.buildPageClause(this.pageNo, this.pageSize);
      if (this.cameraName) {
        qry.buildWhereClause("cameraName", this.cameraName, "LK");
      }
      const param = qry.getParam();

      const res = await this.api.getSysPumpCameraPage(param);
      const list = res.data.list;
      this.total = res.page.total;

      this.list.push(...list);
      const len = this.list.length;
      this.title = `视频监控（${len}）`;
      this.loading = false;
    },
    loadMore() {
      console.log("loadMore");
      if (this.list.length < this.total) {
        this.pageNo++;
        this.loading = true;
        this.getList();
      }
    },
    close() {
      this.videoShow = false;
    },
    videoPlay(url) {
      this.videoUrl = url;
      this.videoShow = true;

      // console.log(url)
      // console.log(this.$refs.video)
      // this.$refs.video.setUrl(url)
    }
  }
};
</script>
<style lang="less" scoped>
@import "../../../assets/css/mobile.less";
#container {
  width: 100%;
  background: @bgColor;
  height: 100%;
  display: flex;
  display: -webkit-flex;
  flex-direction: column;
  .menu {
    width: 100%;
    background: #ffffff;
    display: flex;
    display: -webkit-flex;
    align-items: center;
    height: 0.8rem;
    margin-bottom: 0.2rem;
    padding: 0 0.5rem;
    box-sizing: border-box;
    > div {
      flex: 1;
      margin: 0 0.3rem;
      display: flex;
      display: -webkit-flex;
      flex-flow: row nowrap;
      input {
        padding-left: 0.4rem;
        flex: 1;
        border: 1px solid #ccc;
      }
      .mint-button {
        flex: 0 0 auto;
        background-color: @color;
      }
    }
  }
}
.main {
  flex: 1;
  overflow: auto;
  -webkit-overflow-scrolling: touch;
}
</style>

