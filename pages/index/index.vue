<template>
<div class="container">
  首页内容
  <div class="content-box" @click="goDetail"></div>
</div>
</template>

<script>
export default {
  components: {},
  props: {},
  data() {
    return {
    };
  },
  watch: {},
  computed: {},
  methods: {
    goDetail(){
      this.$router.push({ path:'/detail', query: { id: 123 } })
    }
  },
  created() {},
  mounted() {}
};
</script>
<style scoped>
.content-box{
  width: 200px;
  height: 200px;
  background: orange;
}
</style>