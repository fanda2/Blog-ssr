<template>
  <div class="clock-box">
    <!-- 不同时钟 -->
    <div class="ordinary-clock">
      <!-- 时钟 -->
      <div v-if="clockStyle == 'ordinaryClock'" class="clock" :style="styleVar">
        <!-- 内圈 -->
        <div class="innerBorder">
          <!-- 时钟刻度 -->
          <div class="scale mark1"></div>
          <div class="scale mark2"></div>
          <div class="scale mark3"></div>
          <div class="scale mark4"></div>
          <div class="scale mark5"></div>
          <div class="scale mark6"></div>
          <div class="scale mark7"></div>
          <div class="scale mark8"></div>
        </div>
        <!-- 内圈波浪 -->
        <div class="wave"></div>
        <!-- 时针、分针、秒针 -->
        <div class="hands hourhand"></div>
        <div class="hands minhand"></div>
        <div class="hands sechand"></div>
      </div>
    </div>
    <!-- 数字时钟 -->
    <div v-if="clockStyle == 'digitalClock'" class="digital-clock"></div>
    <!-- 日历信息展示 展示阳历和阴历-->
    <div class="calendar">
      <div class="calendar-left">
        <div class="ico-box">
          <img :src="monthIcoUrl" alt="月份图标" />
          <!-- <img src="http://wew.fjtbkyc.net/images/date1.png" alt=""> -->
        </div>
        <div class="date-box">{{ showDate }}</div>
      </div>
      <div class="calendar-right">
        {{ showChineseDate }}
      </div>
    </div>
    <!-- 根据时间展示的标语 -->
    <div class="motto"></div>
  </div>
</template>

<script>
import { getLunar } from "chinese-lunar-calendar";
export default {
  components: {},
  props: {
    //时钟类型展示，有数字时钟digitalClock 和 ordinaryClock
    clockStyle: {
      default: "ordinaryClock",
    },
    //时钟背景大小
    bgsize: {
      type: Number,
      default: 140,
    },
    bgcolor: {
      type: String,
      default: "#D1CCC0",
    },
  },
  data() {
    return {
      // 用于计录时间的定时器
      timer: "",
      hour: 0, //小时
      minute: 0, //分钟
      second: 0, //秒

      // 年月日
      year: 0,
      month: 0,
      day: 0,

      //图标数据
      monthIcoList: [
        "http://wew.fjtbkyc.net/images/date1.png",
        "http://wew.fjtbkyc.net/images/date2.png",
        "http://wew.fjtbkyc.net/images/date3.png",
        "http://wew.fjtbkyc.net/images/date4.png",
        "http://wew.fjtbkyc.net/images/date5.png",
        "http://wew.fjtbkyc.net/images/date6.png",
        "http://wew.fjtbkyc.net/images/date7.png",
        "http://wew.fjtbkyc.net/images/date8.png",
        "http://wew.fjtbkyc.net/images/date9.png",
        "http://wew.fjtbkyc.net/images/date10.png",
        "http://wew.fjtbkyc.net/images/date11.png",
        "http://wew.fjtbkyc.net/images/date12.png",
        "http://wew.fjtbkyc.net/images/date13.png",
        "http://wew.fjtbkyc.net/images/date14.png",
        "http://wew.fjtbkyc.net/images/date15.png",
        "http://wew.fjtbkyc.net/images/date16.png",
        "http://wew.fjtbkyc.net/images/date17.png",
        "http://wew.fjtbkyc.net/images/date18.png",
        "http://wew.fjtbkyc.net/images/date19.png",
        "http://wew.fjtbkyc.net/images/date20.png",
        "http://wew.fjtbkyc.net/images/date21.png",
        "http://wew.fjtbkyc.net/images/date22.png",
        "http://wew.fjtbkyc.net/images/date23.png",
        "http://wew.fjtbkyc.net/images/date24.png",
        "http://wew.fjtbkyc.net/images/date25.png",
        "http://wew.fjtbkyc.net/images/date26.png",
        "http://wew.fjtbkyc.net/images/date27.png",
        "http://wew.fjtbkyc.net/images/date28.png",
        "http://wew.fjtbkyc.net/images/date29.png",
        "http://wew.fjtbkyc.net/images/date30.png",
        "http://wew.fjtbkyc.net/images/date31.png",
      ],
      monthIcoUrl: "",

      //展示年月日
      showDate: "",
      showChineseDate: "",
    };
  },
  watch: {
    day(newVal, oldVal) {
      this.monthIcoUrl = this.monthIcoList[newVal - 1];
    },
  },
  computed: {
    styleVar() {
      return {
        "--clock-size": this.bgsize + "px",
        "--clock-bgcolor": this.bgcolor,
        "--length-log2E": (this.bgsize - 10) / 2 / Math.LOG2E + "px",
      };
    },
  },
  methods: {
    // 校准时钟指针方法
    currentTime: function () {
      let date = new Date();
      this.hour = date.getHours();
      this.minute = date.getMinutes();
      this.second = date.getSeconds();

      this.year = date.getFullYear();
      this.month = date.getMonth() + 1;
      this.day = date.getDate();

      document.getElementsByClassName("hourhand")[0].style.transform =
        "rotate(" + (this.hour / 24) * 360 + "deg)";
      document.getElementsByClassName("minhand")[0].style.transform =
        "rotate(" + (this.minute / 60) * 360 + "deg)";
      document.getElementsByClassName("sechand")[0].style.transform =
        "rotate(" + (this.second / 60) * 360 + "deg)";
    },

    //用户获取当前时间的农历计算，
    getCurrentDate() {
      let currentMonth = this.month < 10 ? "0" + this.month : this.month;
      let currentDay = this.day < 10 ? "0" + this.day : this.day;
      this.showDate =
        this.year + "年" + currentMonth + "月" + currentDay + "日";
      let chineseDate = getLunar(this.year, this.month, this.day);
      this.showChineseDate = chineseDate.lunarYear + " " + chineseDate.dateStr;
    },
  },
  created() {},
  mounted() {
    this.currentTime();
    // 定时校准
    setInterval(this.currentTime, 1000);
    this.getCurrentDate();
  },
  //页面销毁时清空定时器
  destroyed() {
    clearInterval(this.timer);
  },
};
</script>
<style lang="less" scoped>
/* 时钟组件全部 */
.clock-box {
  width: 100%;
  height: 330px;
  margin-top: 10px;
  border-radius: 8px;
  background: #bddbce;
  padding: 10px;
  box-sizing: border-box;
}
/* 时钟内容主体部分 */
.ordinary-clock {
  width: 100%;
  background: #9dc9b6;
  border-radius: 6px;
  padding: 10px 0;
  display: flex;
  justify-content: center;
}
.inner-clock-content {
  width: 120px;
  height: 120px;
  display: flex;
  border-radius: 50%;
  justify-content: center;
  align-items: center;
  border: 1px solid #333;
  background: #fff;
}

/* 数字展示时钟 */
.digital-clock {
  width: 100%;
  height: 60px;
}

/* 根据时间展示不同标语 */
.motto {
  width: 100%;
  height: 100px;
  background: pink;
}

/* 普通时钟设置样式 */
/* 外部大小和阴影 */
.clock {
  width: var(--clock-size);
  height: var(--clock-size);
  border-radius: 50%;
  box-shadow: 5px 5px 10px var(--clock-bgcolor), -4px -4px 8px #fff;
  position: relative;
}
/* 内阴影 */
.innerBorder {
  /* calc加var计算 */
  width: calc(var(--clock-size) - 10px);
  height: calc(var(--clock-size) - 10px);
  position: relative;
  left: 5px;
  top: 5px;
  box-shadow: -3px -3px 6px #fff inset, 3px 3px 6px var(--clock-bgcolor) inset;
  border-radius: 50%;
}
/* 时钟刻度 */
.scale {
  width: 2px;
  height: 8px;
  position: absolute;
  box-shadow: 1px 1px 1px #9d958f inset,
    -1px -1px 1px var(--clock-bgcolor) inset;
  border-radius: 1px;
}
/* 设置小刻度位置 */
.mark1 {
  left: calc(50% - 1px);
  top: 2px;
}
.mark2 {
  transform: rotate(45deg);
  left: calc(50% + var(--length-log2E));
  top: calc(50% - var(--length-log2E));
}
.mark3 {
  transform: rotate(90deg);
  left: calc(100% - 7px);
  top: calc(50% - 3px);
}
.mark4 {
  transform: rotate(135deg);
  left: calc(50% + var(--length-log2E) - 5px);
  top: calc(50% + var(--length-log2E) - 5px);
}
.mark5 {
  left: calc(50% - 1px);
  bottom: 2px;
}
.mark6 {
  transform: rotate(45deg);
  left: calc(50% - var(--length-log2E) + 5px);
  top: calc(50% + var(--length-log2E) - 5px);
}
.mark7 {
  transform: rotate(90deg);
  left: 2px;
  top: calc(50% - 3px);
}
.mark8 {
  transform: rotate(135deg);
  left: calc(50% - var(--length-log2E));
  top: calc(50% - var(--length-log2E));
}
/* 中间波浪 */
.wave {
  width: 30%;
  height: 30%;
  position: absolute;
  left: 35%;
  top: 35%;
  box-shadow: 3px 3px 9px var(--clock-bgcolor), -3px -3px 9px #fff;
  border-radius: 50%;
  filter: blur(1px); /* 模糊处理 */
  animation: wavemove 4s infinite linear;
}
@keyframes wavemove {
  0% {
    transform: scale(0.5);
  }
  50% {
    transform: scale(1);
    opacity: 1;
  }
  100% {
    transform: scale(1.7);
    opacity: 0;
  }
}
/*************************** 时针、分针、秒针 ****************************/
.hands {
  position: absolute;
  transform-origin: bottom;
  border-radius: 10px;
  z-index: 300;
  bottom: 50%;
  left: calc(50% - 1px);
}
.sechand {
  width: 2px;
  height: 42%;
  background-image: linear-gradient(#cd69c9, #1ca6f3);
}
.minhand {
  width: 4px;
  height: 33%;
  background-color: #9ba5aa;
  left: calc(50% - 2px);
}
.hourhand {
  width: 6px;
  height: 21%;
  background-color: #bec8e4;
  left: calc(50% - 3px);
}

/* 日历展示样式 */
.calendar{
  display: flex;
  justify-content: space-between;
  height: 50px;
  font-size: 14px;
  color: #333;
  .calendar-left{
    width: 55%;
    line-height: 50px;
    display: flex;
    .ico-box{
      width: 40px;
      height: 50px;
      display: flex;
      justify-content: center;
      align-items: center;
      img{
        width: 30px;
        height: 30px;
      }
    }
  }
  .calendar-right{
     width: 40%;
     line-height: 50px;
  }
}
</style>