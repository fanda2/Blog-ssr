<template>
  <!-- 文章列表组件 -->
  <div class="post-item">
    <div class="item-left">
      <div class="img-box">
        <img :src="postInfo.coverUrl" alt="" />
      </div>
    </div>
    <div class="item-right">
      <div class="post-message">
        <div class="post-title">
          {{ postInfo.title }}
        </div>
        <div class="post-descrption">
          {{ postInfo.descript }}
        </div>
        <div class="post-data">
          <div class="count-read">
            <img src="../static/img/read.png" alt="阅读量" />
            <div title="阅读量">{{ postInfo.countRead }}</div>
          </div>
          <div class="count-comment">
            <img src="../static/img/comment.png" alt="评论数" />
            <div title="评论数">{{ postInfo.countComment }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  props: {
    // 文章信息对象
    postInfo: {
      type: Object,
      default: () => {},
    },
  },
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
<style lang="less" scoped>
.post-item {
  width: 96%;
  height: 180px;
  margin: 20px auto;
  border-radius: 8px;
  border: 1px solid #ccc;
  overflow: hidden;
  display: flex;
  cursor: pointer;
}
.post-item .item-left {
  width: 30%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
.post-item .item-right {
  width: 66%;
  height: 100%;
}
// 左边封面部分
.item-left .img-box {
  width: 96%;
  margin: 0 auto;
  height: 160px;
  background: rgb(255, 149, 107);
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
  img {
    height: 100%;
    object-fit: cover;
  }
}

// 右边信息部分
.post-message {
  height: 160px;
  box-sizing: border-box;
  padding: 5px 10px;
  .post-title {
    height: 40px;
    line-height: 40px;
    font-size: 24px;
    font-weight: 550;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .post-descrption {
    height: 100px;
    font-size: 14px;
    width: 100%;
    text-overflow: ellipsis;
    overflow: hidden;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 5;
    line-height: 20px;
  }
  .post-data {
    display: flex;
    .count-read,
    .count-comment {
      padding-top: 6px;
      width: 100px;
      height: 25px;
      line-height: 25px;
      text-align: center;
      display: flex;
      color: #666;
    }
  }
}
.count-read > div,
.count-comment > div {
  padding-left: 10px;
}
.post-data img {
  width: 25px;
  height: 25px;
}
</style>