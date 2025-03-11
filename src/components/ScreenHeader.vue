<template>
  <el-row class="screen-header-container text-white">
    <el-col :span="4" class="screen-header-item">
      <div class="login">登录</div>
    </el-col>
    <el-col :span="16" class="screen-header-item">
      <div class="title text-center screen-header-title">控制中心大屏</div>
    </el-col>
    <el-col :span="4" class="screen-header-item">
      <div class="system-info flex items-center">
        <div class="sys-time font-bold px-8">{{ currentTime }}</div>
        <div class="sys-date text-center px-8">
          <div>{{ currentWeekDay }}</div>
          <div>{{ currentDate }}</div>
        </div>
      </div>
    </el-col>
  </el-row>
</template>

<script>
import moment from 'moment';
import 'moment/locale/zh-cn'; // 导入中文语言包

export default {
  name: 'ScreenHeader',
  data() {
    return {
      timer: null,
      currentTime: '',
      currentDate: '',
      currentWeekDay: '',
    };
  },
  created() {
    // 设置语言为中文
    moment.locale('zh-cn');
    this.updateDateTime();
    // 启动定时器，每秒更新一次
    this.timer = setInterval(this.updateDateTime, 1000);
  },
  beforeDestroy() {
    // 组件销毁前清除定时器
    if (this.timer) {
      clearInterval(this.timer);
      this.timer = null;
    }
  },
  methods: {
    updateDateTime() {
      const now = moment();

      // 更新时间 HH:mm:ss
      this.currentTime = now.format('HH:mm:ss');

      // 更新星期
      this.currentWeekDay = now.format('dddd');

      // 更新日期 YYYY-MM-DD
      this.currentDate = now.format('YYYY-MM-DD');
    },
  },
};
</script>

<style lang="scss" scoped>
@import '../mixins.scss';

$margin-container: 46px;
$header-top-mg: 20px;
.screen-header-container {
  height: 102px;
  @include bg-image('@/assets/images/bigScreen/bg-screen-header');
  background-size: cover;
  background-position: center center;
  .screen-header-title {
    font-size: 43px;
    line-height: 94px;
    font-family: 'pangmenzuodaoti', sans-serif;
  }
  .screen-header-item {
    height: 102px;
  }
  .login {
    margin-left: $margin-container;
    margin-top: 2px;
    width: 205px;
    height: 80px;
    background: url('@/assets/images/bigScreen/bg-btn-login.png') no-repeat center center/cover;
    line-height: 80px;
    text-align: center;
    font-size: 18px;
    font-weight: 600;
    font-family: 'puhuiti', sans-serif;
    cursor: pointer;
  }
}
.system-info {
  //   display: flex;
  margin-right: $margin-container;
  margin-top: $header-top-mg;
  font-family: 'puhuiti', sans-serif;
  .sys-time {
    border-right: 1px solid #fff;
    font-size: 32px;
  }
}
</style>
