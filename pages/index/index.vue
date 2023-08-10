<template>
<div class="page-content">
  <div class="page-left">
    <Table/>
  </div>
  <div class="page-right">
    <RightText/>
  </div>
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
 /* .page-left{
   background: rebeccapurple;
   height: 200px;
 }
 .page-right{
   background: pink;
   height: 200px;
 } */
</style>