<template>
<div class="text-centent">
  <div class="text">
    <span>Fanda Blog</span>
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
  methods: {},
  created() {},
  mounted() {}
};
</script>
 <style scoped>
    .text-centent{
      margin-top: 10px;
      height: 70px;
      line-height: 70px;
      font-weight: bold;
      text-align: center;
      background-color: #333;
      filter: contrast(20);
      border-radius: 8px;
    }
    .text{
      font-size: 40px;
      color: #fff;
      animation: showup 3s forwards;
    }
    @keyframes showup{
      0%{
        letter-spacing: -50px;
        filter: blur(10px)
      }
      100%{
        letter-spacing: 5px;
        filter: blur(2px);
      }
    }

  </style>