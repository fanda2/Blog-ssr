<template>
<div class="container">
  首页内容
  <nuxt-link to="/:detail">
    <div class="content-box"></div>
  </nuxt-link>
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
  methods: {},
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