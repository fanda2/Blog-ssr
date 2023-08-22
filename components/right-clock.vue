<template>
  <div class="clock-box">
    <!-- 不同时钟 -->
    <div v-if="clockStyle == 'ordinaryClock'" class="ordinary-clock">
      <!-- 时钟 -->
      <div class="clock" :style="styleVar">
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
    <div v-if="clockStyle == 'digitalClock'" class="digital-clock">
      <div class="clock">
        <div class="digit hours">
          <div v-for="(item,index) in 7" :key="index" :class="{'segment':true,'on':digitSegments[oneNum].indexOf(index+1)!==-1 }"></div>
        </div>

        <div class="digit hours">
          <!-- <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div> -->
          <div v-for="(item,index) in 7" :key="index" :class="{'segment':true,'on':digitSegments[twoNum].indexOf(index+1)!==-1}"></div>
        </div>

        <div class="separator"></div>

        <div class="digit minutes">
          <!-- <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div> -->
          <div v-for="(item,index) in 7" :key="index" :class="{'segment':true,'on':digitSegments[threeNum].indexOf(index+1)!==-1}"></div>
        </div>

        <div class="digit minutes">
          <!-- <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div> -->
          <div v-for="(item,index) in 7" :key="index" :class="{'segment':true,'on':digitSegments[fourNum].indexOf(index+1)!==-1 }"></div>
        </div>

        <div class="separator"></div>

        <div class="digit seconds">
          <!-- <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div> -->
          <div v-for="(item,index) in 7" :key="index" :class="{'segment':true,'on':digitSegments[fiveNum].indexOf(index+1)!==-1 }"></div>
        </div>

        <div class="digit seconds">
          <!-- <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div>
          <div class="segment"></div> -->
          <div v-for="(item,index) in 7" :key="index" :class="{'segment':true,'on':digitSegments[sixNum].indexOf(index+1)!==-1 }"></div>
        </div>
      </div>
    </div>
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
    <div class="motto">时光荏苒，珍惜眼前活在当下，过好现在的每一天</div>
  </div>
</template>

<script>
import { getLunar } from "chinese-lunar-calendar";
export default {
  components: {},
  props: {
    //时钟类型展示，有数字时钟digitalClock 和 ordinaryClock
    clockStyle: {
      // default: "ordinaryClock",
      default: "digitalClock",
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
      monthIcoUrl: "",

      //展示年月日
      showDate: "",
      showChineseDate: "",

      //用于LED时间显示的数组，每个数组代表展示的数字
      digitSegments: [
        [1, 2, 3, 4, 5, 6],
        [2, 3],
        [1, 2, 7, 5, 4],
        [1, 2, 7, 3, 4],
        [6, 7, 2, 3],
        [1, 6, 7, 3, 4],
        [1, 6, 5, 4, 3, 7],
        [1, 2, 3],
        [1, 2, 3, 4, 5, 6, 7],
        [1, 2, 7, 3, 6],
      ],
      //数组
      oneNum:0,
      twoNum:0,
      threeNum:0,
      fourNum:0,
      fiveNum:0,
      sixNum:0,
    };
  },
  watch: {
    day(newVal, oldVal) {
      this.monthIcoUrl = `http://wew.fjtbkyc.net/images/date${newVal}.png`;
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

      if (this.clockStyle === "ordinaryClock") {
        document.getElementsByClassName("hourhand")[0].style.transform =
          "rotate(" + (this.hour / 24) * 360 + "deg)";
        document.getElementsByClassName("minhand")[0].style.transform =
          "rotate(" + (this.minute / 60) * 360 + "deg)";
        document.getElementsByClassName("sechand")[0].style.transform =
          "rotate(" + (this.second / 60) * 360 + "deg)";
      }else{
        this.setNumber();
      }
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

    //计算显示数字
    setNumber(){
      this.oneNum=Math.floor(this.hour/10);
      this.twoNum=this.hour%10;
      this.threeNum=Math.floor(this.minute/10);
      this.fourNum=this.minute%10;
      this.fiveNum=Math.floor(this.second/10);
      this.sixNum=this.second%10;
    }
  },
  created() {},
  mounted() {
    this.currentTime();
    // 定时校准
    this.timer = setInterval(this.currentTime, 1000);
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
  height: 160px;
  display: flex;
  align-items: center;
  .clock {
    height: 120px;
    width: 100%;
    text-align: center;
  }

  .digit {
    width: 30px;
    height: 70px;
    margin: 0 3px;
    position: relative;
    display: inline-block;
  }

  .digit .segment {
    background: #376350;
    border-radius: 4px;
    position: absolute;
    opacity: 0.15;
    transition: opacity 0.2s;
    -webkit-transition: opacity 0.2s;
    -ms-transition: opacity 0.2s;
    -moz-transition: opacity 0.2s;
    -o-transition: opacity 0.2s;
  }

  .digit .segment.on,
  .separator {
    opacity: 1;
    box-shadow: 0 0 5px rgb(91, 165, 133, 0.04);
    transition: opacity 0s;
    -webkit-transition: opacity 0s;
    -ms-transition: opacity 0s;
    -moz-transition: opacity 0s;
    -o-transition: opacity 0s;
  }

  .separator {
    width: 10px;
    height: 10px;
    background: #376350;
    border-radius: 50%;
    display: inline-block;
    position: relative;
    top: -30px;
  }

  .digit .segment:nth-child(1) {
    top: 4px;
    left: 5px;
    right: 5px;
    height: 6px;
  }

  .digit .segment:nth-child(2) {
    top: 10px;
    right: 0px;
    width: 6px;
    height: 75px;
    height: calc(50% - 10px);
  }

  .digit .segment:nth-child(3) {
    bottom: 8px;
    right: 0px;
    width: 6px;
    height: 75px;
    height: calc(50% - 10px);
  }

  .digit .segment:nth-child(4) {
    bottom: 4px;
    right: 6px;
    height: 6px;
    left: 5px;
  }

  .digit .segment:nth-child(5) {
    bottom: 8px;
    left: 0px;
    width: 6px;
    height: 75px;
    height: calc(50% - 10px);
  }

  .digit .segment:nth-child(6) {
    top: 10px;
    left: 0px;
    width: 6px;
    height: 75px;
    height: calc(50% - 10px);
  }

  .digit .segment:nth-child(7) {
    bottom: 95px;
    bottom: calc(50% - 5px);
    right: 6px;
    left: 6px;
    height: 6px;
  }
}

/* 根据时间展示不同标语 */
.motto {
  width: 100%;
  height: 100px;
  background: #9dc9b6;
  border-radius: 6px;
  padding: 5px;
  box-sizing: border-box;
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
.calendar {
  display: flex;
  justify-content: space-between;
  height: 50px;
  font-size: 14px;
  color: #333;
  .calendar-left {
    width: 55%;
    line-height: 50px;
    display: flex;
    .ico-box {
      width: 40px;
      height: 50px;
      display: flex;
      justify-content: center;
      align-items: center;
      img {
        width: 30px;
        height: 30px;
      }
    }
  }
  .calendar-right {
    width: 40%;
    line-height: 50px;
  }
}
</style>