<template>
  <div class="container">
    <div class="header"></div>
    <div class="main">
      这是主体部分内容
    </div>
    <div class="footer">
      <Footer />
    </div>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
};
</script>

<style>
.container{
  position: relative;
}
/* 顶部导航栏 */
.header {
  width: 100%;
  height: 60px;
  background: rgb(215, 255, 255);
}

/* 主题内容 */
.main {
  min-height: calc(100%-140px);
  background: rgb(236, 236, 236,0.5);
}

/* 底部内容 */
.footer {
  width: 100%;
  height: 60px;
}
</style>
