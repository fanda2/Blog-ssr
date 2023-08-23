<template>
   <div class="container">
     <!-- 导航栏 -->
    <div class="header-box">
      <div class="inner-header wrap1">
        <div class="logo-left">
          <img src="../static/img/logo.png" alt="logo">
        </div>
         <div class="right-menu">
          <ul class="menu-clumn">
            <li><nuxt-link class="link-btn" to="/">主页</nuxt-link></li>
             <li><nuxt-link class="link-btn" to="/file">归档</nuxt-link></li>
            <li><nuxt-link class="link-btn" to="/tool">工具</nuxt-link></li>
            <li><nuxt-link class="link-btn" to="/about">关于</nuxt-link></li>
          </ul>
          <div class="logo-box">登录</div>
         </div>     
      </div>
    </div>
    <!-- 主体页面部分 -->
    <div class="main-box">
      <div class="inner-main wrap1">
        <nuxt-child></nuxt-child>
      </div>
    </div>
    <!-- 底部footer -->
    <div class="footer-box">
      <div class="inner-footer wrap1">
        <p>copyRight &copy; fanda</p>
        <p>2003All</p>
        <p>本站使用vue+nuxt.js实现服务端渲染</p>
      </div>
    </div>
   </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data(){
    return{

    }
  },
  mounted(){

  },
  created(){

  },
  methods:{

  }
}
</script>
<style scoped>
/* 顶部菜单 */
.header-box{
  width: 100%;
  height: 60px;
  background: #333;
}
.inner-header{
  display: flex;
  height: 60px;
  justify-content: space-between;
}
.logo-left{
  width: 200px;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
}
.logo-left img{
  height: 80%;
  object-fit: cover;
}

.right-menu{
  /* width: 400px; */
  height: 60px;
  display: flex;
  justify-content: center;
  color: white;
}
.right-menu .logo-box{
  height: 60px;
  line-height: 60px;
  padding: 0 40px;
  cursor: pointer;
}
.right-menu ul,.right-menu li{
  list-style: none;
}
.right-menu ul{
  display: flex;
}
.right-menu li{
  display: block;
  padding: 0 20px;
  height: 60px;
  line-height: 60px;
}
/* 主题内容 */
.main-box{
  width: 100%;
  min-height: calc(100vh - 120px);
  background: rgb(241, 241, 241);
}

/* 底部内容 */
.footer-box{
  height: 60px;
  width: 100%;
  background: #333;
  border-top: 1px solid #ccc;
  color: #fff;
  font-size: 12px;
}
.footer-box p{
  text-align:center;
  padding: 2px 10px;
}

.link-btn{
  color: #fff;
  text-decoration: none;
}
</style>
