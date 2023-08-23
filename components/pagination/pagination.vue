<template>
  <div class="my-page" v-if="total!==0">
    <!-- 总条数 -->
    <span class="my-page-total" v-if="showTotal">共{{ total }}条</span>
    <ul class="page-list">
      <!-- 上一页 -->
      <li
        :class="['page-list-item', currentPage <= 1 ? 'disbled' : '']"
        @click="handleBeforOrAfterClick('before')"
      >
        &lt;
      </li>
      <!-- 中间页码数据 -->
      <template v-for="(pageItem, index) in pageList">
        <!-- 向前5页 -->
        <li
          :class="['page-list-item', 'page-list-item-prev']"
          @click="handlePageItemClick(pageItem, 'prev')"
          :key="index"
          title="向前5页"
          v-if="pageItem == 'prev'"
          @mouseover="prevStatus = false"
          @mouseleave="prevStatus = true"
        >
          <i v-if="prevStatus"> ...</i>
          <i v-else>{{'<<'}}</i>
        </li>
        <!-- 正常页码 -->
        <li
          :class="['page-list-item', 'page-list-item-next']"
          @click="handlePageItemClick(pageItem, 'next')"
          :key="index"
          title="向后5页"
          v-else-if="pageItem == 'next'"
          @mouseenter="nextStatus = false"
          @mouseleave="nextStatus = true"
        >
          <i v-if="nextStatus"> ...</i>
          <i v-else>{{'>>'}}</i>
        </li>
        <!-- 向后五页 -->
        <li
          :class="['page-list-item', currentPage == pageItem ? 'active' : '']"
          @click="handlePageItemClick(pageItem)"
          :key="index"
          :title="pageItem"
          v-else
        >
          {{ pageItem }}
        </li>
      </template>
      <!-- 下一页 -->
      <li
        :class="[
          'page-list-item',
          currentPage >= totalPage && totalPage > 0 ? 'disbled' : '',
        ]"
        @click="handleBeforOrAfterClick('after')"
      >
        &gt;
      </li>
    </ul>
    <!-- 每页条数电梯 -->
    <div class="page-size-select" v-if="showSizer">
      <select @change="handlePageSizeChange">
        <option
          :value="pageSizeItem"
          v-for="pageSizeItem in pageSizeOpts"
          :key="pageSizeItem"
        >
          {{ pageSizeItem }}条/页
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    // 总页码条数
    total: {
      type: Number,
      default: 0,
    },
    // 当前页
    current: {
      type: Number,
      default: 1,
    },
    // 每页条数，默认10条
    pageSize: {
      type: Number,
      default: 10,
    },
    // 是否显示总条数
    showTotal: {
      type: Boolean,
      default: false,
    },
    // 每页大小
    showSizer: {
      type: Boolean,
      default: false,
    },
    // 页码条数下拉
    pageSizeOpts: {
      type: Array,
      default() {
        return [10, 20, 30, 40];
      },
    },
    //当总页数为0时隐藏组件
    hiidenTotal:{
      type:Boolean,
      default:false
    }
  },
  data() {
    return {
      // 当前页码
      currentPage: this.current || 1,
      // 当前每页条数
      currentPageSize: this.pageSize,
      // 是否显示向后5条的>>
      prevStatus: true,
      // 是否显示向前5条的<<
      nextStatus: true,
    };
  },
  computed: {
    // 根据总条数和每页条数计算得出总页数,记得向上取整
    totalPage() {
      return Math.ceil(this.total / this.currentPageSize);
    },
    // 动态根据当前页,重新组装分页列表数据
    pageList() {
      //情况1： 总页码数<5的直接返回
      if (this.totalPage <= 5) {
        return this.totalPage;
      }
      //情况2： 总页码数>5页，当时当前页码数<=3
      if (this.currentPage <= 3) {
        return [1, 2, 3, "next", this.totalPage];
      }
      // 情况3：总页数-当前页数<=3
      if (this.currentPage > 3 && this.totalPage - this.currentPage <= 2) {
        return [
          1,
          "prev",
          this.totalPage - 2,
          this.totalPage - 1,
          this.totalPage,
        ];
      }
      // 情况4：排除其他的，剩下的就是有向前和向后的操作点
      return [
        1,
        "prev",
        this.currentPage - 2,
        this.currentPage - 1,
        this.currentPage,
        this.currentPage + 1,
        this.currentPage + 2,
        "next",
        this.totalPage,
      ];
    },
  },
  methods: {
    // 页码项点击
    handlePageItemClick(item, type) {
      // 重置向上和向下翻五页
      this.prevStatus = true;
      this.nextStatus = true;
      switch (type) {
        // 向前5页
        case "prev":
          this.currentPage -= 5;
          if (this.currentPage < 1) {
            this.currentPage = 1;
          }
          break;
        // 向后5页
        case "next":
          this.currentPage += 5;
          if (this.currentPage > this.totalPage) {
            this.currentPage = this.totalPage;
          }
          break;
        default:
          // 默认常规页码点击
          if (this.currentPage == item) {
            return;
          }
          this.currentPage = item;
      }
      // 发布页码变更事件
      this.$emit("on-change", this.currentPage);
    },
    // 上一页和下一页点击
    handleBeforOrAfterClick(type) {
      switch (type) {
        case "before":
          this.currentPage--;
          if (this.currentPage < 1) {
            this.currentPage = 1;
            return;
          }
          break;
        case "after":
          this.currentPage++;
          if (this.currentPage > this.totalPage) {
            this.currentPage = this.totalPage;
            return;
          }
          break;
      }
      // 发布页码变更事件
      this.$emit("on-change", this.currentPage);
    },
    // 每页条数大小变化
    handlePageSizeChange(e) {
      // value是字符串，记得转成数字
      this.currentPageSize = Number(e.target.value);
      // 重置当前页码
      this.$emit("on-page-size-change", this.currentPageSize);
      this.currentPage = 1;
    },
  },
};
</script>

<style lang="less" scoped>
.my-page {
  font-family: Arial, Helvetica, sans-serif;
  display: flex;
  align-items: center;
  color: #333;
  .page-list {
    .page-list-item {
      display: inline-block;
      vertical-align: middle;
      -webkit-user-select: none;
      -moz-user-select: none;
      -ms-user-select: none;
      user-select: none;
      min-width: 32px;
      height: 32px;
      line-height: 30px;
      list-style: none;
      text-align: center;
      cursor: pointer;
      color: rgb(75, 75, 75);
      font-family: Arial;
      border: 1px solid #dcdee2;
      border-radius: 4px;
      transition: all 0.2s ease-in-out;
      margin-right: 6px;
      margin-left: 6px;
      &:hover {
        border-color: #2d8cf0;
        color: #2d8cf0;
      }
    }
    .active.page-list-item {
      border-color: #2d8cf0;
      color: #fff;
      background-color: #2d8cf0;
    }
    .disbled.page-list-item {
      cursor: not-allowed;
      background-color: #fff;
      color: #a6a7aa;
    }
    .disbled:hover {
      border-color: #dcdee2;
    }
  }
    .my-page-total{
      font-size: 14px;
    }
   .page-size-select{
      width: 100px;
      height: 32px;
      // background: chartreuse;
      display: flex;
      justify-content: center;
      align-items: center;
      select{
        width: 80px;
        height: 26px;
        border:none;
        outline: none;

      }
    }
}
</style>

