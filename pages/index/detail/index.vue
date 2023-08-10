<template>
  <div class="container">详情页</div>
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
    this.detailId=this.$route.query.id;
  },
};
</script>
<style scoped></style>
