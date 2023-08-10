<template>
<div class="post-item">
  <div class="card-cover">
    <img :src="postInfo.coverUrl" alt="">
  </div>
  <div class="post-message">
    <div class="post-title">
        {{postInfo.title}}
    </div>
    <div class="post-descrption">
        {{postInfo.descript}}
    </div>
    <div class="post-data">
      <div class="count-read">
          {{postInfo.countRead}}
      </div>
      <div class="count-comment">
          {{postInfo.countComment}}
      </div>
    </div>
  </div>
</div>
</template>

<script>
export default {
  components: {},
  props: {
    // postInfo:{
     
    // }
  },
  data() {
    return {
      postInfo:{
         title:"这是第一篇文章",
         descript:"这是文章描述",
         content:"这是文章内容，支持富文本",
         coverUrl:"https://img0.baidu.com/it/u=2288019296,1718805156&fm=253&fmt=auto&app=138&f=JPEG",
         postCreateTime:"2023-08-10 12:12:12",
         postUpdateTime:"2023-08-10 13:12:12",
         countRead:1021,
         countComment:11,
      }
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
.post-item{
  width: 96%;
  height: 300px;
  margin: 10px auto;
  border-radius: 8px;
  border: 1px solid #ccc;
  overflow: hidden;
}
/* 卡片样式 */
.card-cover{
  height: 200px;
  width: 100%;
  overflow: hidden;
}
.card-cover img{
  widows: 100%;
  object-fit: cover;
}
.post-message{
  height: 80px;
  box-sizing: border-box;
  padding: 5px 10px;
}
</style>