<template>
<div class="page-content">
  <div class="page-left">
    <div v-for="(item) in postListData" :key="item.id" @click="goDetail(item.id)">
      <Table :postInfo="item"/>
    </div>
  </div>
  <div class="page-right">
    <RightText/>
    <RightClock bgcolor="#5ba585" clockStyle="ordinaryClock"/>
  </div>
</div>
</template>

<script>
export default {
  components: {},
  props: {},
  data() {
    return {
      postListData:[
        {
          id:1,
          title:"这是第一篇文章,测试文章标题过长会不会导致什么问题，如果会那就别太长",
         descript:"这是文章描述",
         content:"这是文章内容，支持富文本",
         coverUrl:"https://img0.baidu.com/it/u=2288019296,1718805156&fm=253&fmt=auto&app=138&f=JPEG",
         postCreateTime:"2023-08-10 12:12:12",
         postUpdateTime:"2023-08-10 13:12:12",
         countRead:1021,
         countComment:11,
        },
         {
           id:2,
         title:"这是第二篇文章",
         descript:"这是文章描述,文章描述应该会有很多的字，以至于可以在本栏目中分为两行，但是超过两行的内容会进行自动的省略，这样就可以避免文字过长超过盒模型的范围，但是目前来看感觉文字内容还不是很长，还有待提升，数据量不够大就得增加数据量来填补空缺，刚刚两行，不过刚才扩充范围，增加了一些文字内容，不知道现在还能否正确实现这个功能，文字真的能比以前容纳更多，就是需要这么多的文字容量 ，才能展示更多核心的内容",
         content:"这是文章内容，支持富文本",
         coverUrl:"https://img.zcool.cn/community/015cc95ee74425a801215aa0fcf745.jpg@1280w_1l_2o_100sh.jpg",
         postCreateTime:"2023-08-10 12:12:12",
         postUpdateTime:"2023-08-10 13:12:12",
         countRead:1021,
         countComment:11,
        }
      ]
    };
  },
  watch: {},
  computed: {},
  methods: {
    goDetail(postId){
      this.$router.push({ path:'/detail', query: { id: postId } })
    }
  },
  created() {},
  mounted() {}
};
</script>
<style scoped>

</style>