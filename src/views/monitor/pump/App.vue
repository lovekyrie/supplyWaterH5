
<template>
  <div id="container">
    <main-header :title="title"></main-header>
    <div
      class="main"
      v-infinite-scroll="loadMore"
      infinite-scroll-disabled="loading"
      infinite-scroll-distance="10"
    >
      <list :list="list"></list>
      <p v-if="!total" class="noData">数据全部加载完</p>
    </div>
  </div>
</template>

<script>
import list from "@/components/monitorList";

export default {
  name: "monitor",
  data() {
    return {
      loading: false,
      pageNo: 1,
      pageSize: 10,
      total: 0,
      title: "水厂数据（4）",
      list: [],
      DATA_SHOW_LIST: [
        {
          key: "所在区域",
          nm: "region",
          value: ""
        },
        {
          key: "通讯状态",
          nm: "status",
          value: ""
        },
        {
          key: "进水压力",
          nm: "inPressure",
          value: ""
        },
        {
          key: "出水压力",
          nm: "outPressure",
          value: ""
        },
        {
          key: "设定压力",
          nm: "setPressure",
          value: ""
        },
        {
          key: "浊度",
          nm: "turbidity",
          value: ""
        },
        {
          key: "余氯",
          nm: "residualChlorine",
          value: ""
        },
        {
          key: "1号泵电流",
          nm: "pumpCurrent1",
          value: ""
        },
        {
          key: "2号泵电流",
          nm: "pumpCurrent2",
          value: ""
        },
        {
          key: "3号泵电流",
          nm: "pumpCurrent3",
          value: ""
        },
        {
          key: "4号泵电流",
          nm: "pumpCurrent4",
          value: ""
        },
        {
          key: "1号泵",
          nm: "pump1",
          value: ""
        },
        {
          key: "2号泵",
          nm: "pump2",
          value: ""
        },
        {
          key: "3号泵",
          nm: "pump3",
          value: ""
        },
        {
          key: "4号泵",
          nm: "pump4",
          value: ""
        },
        {
          key: "运行频率",
          nm: "operatingFrequency",
          value: ""
        },
        {
          key: "1号泵运行频率",
          nm: "operatingFrequency1",
          value: ""
        },
        {
          key: "2号泵运行频率",
          nm: "operatingFrequency2",
          value: ""
        },
        {
          key: "3号泵运行频率",
          nm: "operatingFrequency3",
          value: ""
        },
        {
          key: "4号泵运行频率",
          nm: "operatingFrequency4",
          value: ""
        },
        {
          key: "1号泵运行时间",
          nm: "operationHours1",
          value: ""
        },
        {
          key: "2号泵运行时间",
          nm: "operationHours2",
          value: ""
        },
        {
          key: "3号泵运行时间",
          nm: "operationHours3",
          value: ""
        },
        {
          key: "4号泵运行时间",
          nm: "operationHours4",
          value: ""
        },
        {
          key: "瞬间流量",
          nm: "instantaneousFlow",
          value: ""
        },
        {
          key: "累计流量",
          nm: "cumulativeFlow",
          value: ""
        },
        {
          key: "A相电压",
          nm: "voltage1",
          value: ""
        },
        {
          key: "B相电压",
          nm: "voltage2",
          value: ""
        },
        {
          key: "C相电压",
          nm: "voltage3",
          value: ""
        },
        {
          key: "A相电流",
          nm: "current1",
          value: ""
        },
        {
          key: "B相电流",
          nm: "current2",
          value: ""
        },
        {
          key: "C相电流",
          nm: "current3",
          value: ""
        }
      ]
    };
  },
  components: {
    list
  },
  created() {},
  mounted() {
    this.getList();
    this.list.forEach((item, index) => {
      let dataList = [];
      dataList[0] = item.allList[0];
      item.dataList = dataList;
      this.$set(this.list, index, item);
    });
  },
  methods: {
    async getList() {
      const qry = new this.Query();
      qry.buildPageClause(this.pageNo, this.pageSize);
      const param = qry.getParam();

      const res = await this.api.getSysMonitorLatestPage(param);
      const list = res.data.list;
      this.total = res.page.total;
      list.forEach(item => {
        this.DATA_SHOW_LIST.forEach(data => {
          data.value = item[data.nm];
        });
        item.list = JSON.parse(JSON.stringify(this.DATA_SHOW_LIST));
        item.dataList = item.list.slice(0, 4);
        item.list = item.list.slice(4);
      });
      this.list.push(...list);
      const len = this.list.length;
      this.title = `泵房监控（${len}）`;
      this.loading = false;
    },
    loadMore() {
      console.log("loadMore");
      if (this.list.length < this.total) {
        this.pageNo++;
        this.loading = true;
        this.getList();
      }
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
}
.main {
  flex: 1;
  overflow: auto;
  -webkit-overflow-scrolling: touch;
  .title {
    background: #fafcfe;
    height: 0.8rem;
    display: flex;
    display: -webkit-flex;
    align-items: center;
    border-bottom: 1px solid @borderColor;
    border-top: 1px solid @borderColor;
    color: #303030;
    font-weight: bold;
    img {
      width: 0.15rem;
      margin-left: 0.3rem;
      margin-right: 0.2rem;
    }
  }
  > section {
    overflow: hidden;
    background: #ffffff;
    border-bottom: 1px solid @borderColor;
    margin-bottom: 0.2rem;
    .title {
      width: 100%;
      margin-bottom: 0.5rem;
    }
    .item {
      width: 25%;
      float: left;
      display: flex;
      display: -webkit-flex;
      align-items: center;
      justify-content: center;
      flex-direction: column;
      margin-bottom: 0.5rem;
      .img {
        width: 0.7rem;
        height: 0.7rem;
        display: flex;
        display: -webkit-flex;
        margin-bottom: 0.2rem;
        img {
          margin: auto;
          width: auto;
          height: auto;
          max-height: 100%;
          max-width: 100%;
        }
      }
    }
  }
}
</style>

