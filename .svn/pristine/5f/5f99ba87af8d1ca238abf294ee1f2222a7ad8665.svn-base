import { until } from "./until";
const untilApi = new until();
class api {
  //登录
  getSysLogin(data) {
    return new Promise((resolve, reject) => {
      untilApi.get("/general/access/login", data).then(res => {
        resolve(res);
      });
    });
  }
  //泵房列表
  getSysMonitorLatestPage(data) {
    return new Promise((resolve, reject) => {
      untilApi.get("/gs/monitorLatest/page", data).then(res => {
        if (res.code === 200) {
          resolve(res);
        }
      });
    });
  }
  //视频监控
  getSysPumpCameraPage(data) {
    return new Promise((resolve, reject) => {
      untilApi.get("/gs/pumpCamera/page", data).then(res => {
        if (res.code === 200) {
          resolve(res);
        }
      });
    });
  }
}

export { api };
