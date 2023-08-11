<template>
  <div class="page-content">
    <div class="page-left">
      左边内容
    </div>
    <div class="page-right">
      右边模块
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      detailId:0,
    }
  },
  components: {},
  props: {},
  data() {
    return {};
  },
  watch: {},
  computed: {},
  methods: {},
  created() {},
  mounted() {
    // 获取到跳转ID
    this.detailId=this.$route.query.id;
  },
};
</script>
<style scoped></style>
