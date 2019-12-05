// require ('assets/css/index.less');
require("assets/css/common.css");
// var VueTouch = require('vue-touch')
// require ('assets/css/reset.css');
// require ('assets/css/help.css');
// require ('assets/css/mobile.less');
// require ('assets/css/project.less');
import "assets/js/ScreenAdaptive.js";
import "assets/js/vconsole.js";
// import 'element-ui/lib/theme-default/index.css'
// import ElementUI from 'element-ui'

import "babel-polyfill"; // 解决 IE11 Promise对象未定义
import axios from "axios";
import "./vueFilter"; //全局过滤器F
import { until, reg, postImgUrl, app, hostUrl } from "assets/js/until";
import { msg, confirm, loading, dialog } from "hero";
import "assets/js/wconfig.js";
import "./iconfont"; //字体库
import "./wconfig.js";
// import $ from 'vue-touch'
import { Query } from "assets/js/query";
import { api } from "./api";

import { Lunar } from "assets/js/time";

//引入安卓 苹果
import "assets/js/Ios";
import "assets/js/WebViewJavascriptBridge";

import tab from "components/tab";
import myHeader from "components/myHeader";
import mainHeader from "components/mainHeader";

import { LoadingPlugin } from "vux";

// var VueTouch = require('vue-touch')
import MintUI from "mint-ui";
import "mint-ui/lib/style.css";
import infiniteScroll from "vue-infinite-scroll";

//视频
import VideoPlayer from "vue-video-player";
require("video.js/dist/video-js.css");
require("vue-video-player/src/custom-theme.css");

export default {
  install(Vue) {
    Vue.component("tab", tab);
    Vue.component("myHeader", myHeader);
    Vue.component("mainHeader", mainHeader);
    // Vue.use(YDUI)
    Vue.use(MintUI);
    Vue.use(msg);
    Vue.use(confirm);
    Vue.use(loading);
    Vue.use(dialog);
    Vue.use(infiniteScroll);
    Vue.prototype.axios = axios;
    Vue.prototype.until = new until();
    Vue.prototype.reg = new reg();
    Vue.prototype.app = new app();
    Vue.prototype.postImgUrl = postImgUrl;
    Vue.prototype.hostUrl = hostUrl;

    Vue.prototype.Query = Query;
    Vue.prototype.lunar = Lunar;
    Vue.prototype.api = new api();
    Vue.use(LoadingPlugin);
    // Vue.use(VueTouch, {name: 'v-touch'})
    Vue.prototype.$dialog = {
      // confirm: Confirm,
      // alert: Alert,
      // toast: Toast,
      // notify: Notify,
      // loading: Loading,
    };
  }
};
