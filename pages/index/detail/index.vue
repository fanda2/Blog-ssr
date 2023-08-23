<template>
  <div class="page-content">
    <div class="page-left">
      <div class="back-btn" @click="goBack">&lt; 返回上一级</div>
      <div class="post-content">
        <div class="post-title">{{ postDetail.title }}</div>
        <!-- 文章数据展示，包含阅读量，评论数，发布时间，发布作者  {{ postDetail.createTime }}-->
        <div class="post-data">
          <ul class="ico-list">
            <li class="list-item">
              <div class="inner-item">
                <div class="item-ico">
                  <img src="../../../static/img/date.png" alt="发布日期" title="发布日期" />
                </div>
                <div class="item-text">{{postDetail.createTime}}</div>
              </div>
            </li>
              <li class="list-item">
              <div class="inner-item">
                <div class="item-ico">
                  <img src="../../../static/img/through.png" alt="阅读量" title="阅读量" />
                </div>
                <div class="item-text">{{postDetail.through}}</div>
              </div>
            </li>
              <li class="list-item">
              <div class="inner-item">
                <div class="item-ico">
                  <img src="../../../static/img/discuss.png" alt="讨论量" title="讨论量" />
                </div>
                <div class="item-text">{{postDetail.comment}}</div>
              </div>
            </li>
          </ul>
        </div>
        <!-- 文章标题下面的图标操作 -->
        <div class="post-coverUrl">
          <img :src="postDetail.coverUrl" alt="文章封面图">
        </div>
        <div class="divider-line">
          <div class="line left-line"></div>
          <div class="line-title">正 文</div>
          <div class="line right-line"></div>
        </div>
        <!-- 文章内容展示 -->
        <div class="post-content-box">
          {{postDetail.content}}
        </div>
      </div>
    </div>
    <div class="page-right">右边模块</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      detailId: 0,
      postDetail: {
        id: 1,
        coverUrl:
          "https://img0.baidu.com/it/u=4118059877,4022583619&fm=253&fmt=auto&app=138&f=JPEG",
        title: "这是文章的标题，经过设置限制访问数据",
        createTime: "2023-3-23",
        through:'112,00',
        comment:"212",
        content:"这是文章内容，后面会改为富文本的内容数据"
      },
    };
  },
  components: {},
  props: {},
  watch: {},
  computed: {},
  methods: {
    //点击返回上一级菜单页面
    goBack(){
      history.back();
    }
  },
  created() {},
  mounted() {
    // 获取到跳转ID
    this.detailId = this.$route.query.id;
  },
};
</script>
<style lang="less" scoped>
.page-content {
  width: 100%;
  height: 100%;
}
.page-left {
  background: rgb(241, 241, 241);
  box-sizing: border-box;
  padding: 5px;
  .back-btn {
    height: 40px;
    line-height: 40px;
    width: 100%;
    cursor: pointer;
    font-weight: 550;
  }
  .post-content {
    width: 96%;
    margin: 10px auto;
    .post-title {
      font-size: 28px;
      font-weight: 550;
    }
    .post-data {
      height: 30px;
      margin: 10px 0;
      font-size: 14px;
      color: #333;
      ul,
      li {
        list-style: none;
        margin: 0;
        padding: 0;
      }
      .ico-list {
        display: flex;
        height: 30px;
        line-height: 30px;
      }
      .list-item {
        display: inline-block;
        padding: 0 5px;
        // background: orangered;
        margin-right: 10px;
        .inner-item {
          display: flex;
          .item-ico {
             display: flex;
             width: 45px;
             justify-content: center;
             align-items: center;
            img{
              width: 24px;
              height: 24px;
            }
          }
          .item-text {
            line-height: 30px;
          }
        }
      }
    }
  }
  .divider-line {
    width: 100%;
    height: 60px;
    line-height: 60px;
    display: flex;
    justify-content: center;
    .line-title {
      min-width: 100px;
      text-align: center;
      width: 10%;
    }
    .line {
      width: 45%;
      height: 30px;
      border-bottom: 1px solid rgb(29, 29, 29);
    }
  }
  .post-coverUrl{
    width: 100%;
    margin: 10px 0;
    img{
      width: 100%;
      object-fit: cover;
    }
  }
}
.page-right {
  background: sandybrown;
}
</style>
