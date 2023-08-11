<template>
  <div class="clock-box">
    <div class="clock-content">
      <div class="inner-clock-content">
  
      </div>
    </div>
    <div class="clock-number"></div>
    <div class="motto"></div>
  </div>
</template>

<script>
export default {
  components: {},
  props: {},
  data() {
    return {};
  },
  watch: {},
  computed: {},
  methods: {},
  created() {},
  mounted() {},
};
</script>
<style scoped>
/* 时钟组件全部 */
.clock-box {
  width: 100%;
  height: 300px;
  margin-top: 10px;
  border-radius: 8px;
  background: #ccc;
  padding: 10px;
  box-sizing: border-box;
}
/* 时钟内容主体部分 */
.clock-content {
  width: 100%;
  height: 120px;
  display: flex;
  justify-content: center;
  align-items: center;
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
.clock-number {
  width: 100%;
  height: 60px;
}

/* 根据时间展示不同标语 */
.motto {
  width: 100%;
  height: 100px;
  background: pink;
}
</style>