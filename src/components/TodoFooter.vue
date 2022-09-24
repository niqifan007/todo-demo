<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>{{ count }}</strong></span
    >
    <ul class="filters" @click="fn">
      <li>
        <a
          :class="{ selected: isSel === 'all' }"
          href="javascript:;"
          @click="isSel = 'all'"
          >全部</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isSel === 'no' }"
          href="javascript:;"
          @click="isSel = 'no'"
          >未完成</a
        >
      </li>
      <li>
        <a
          :class="{ selected: isSel === 'yes' }"
          href="javascript:;"
          @click="isSel = 'yes'"
          >已完成</a
        >
      </li>
    </ul>
    <!-- 清除已完成 -->
    <button class="clear-completed" @click="clearFn">清除已完成</button>
  </footer>
</template>

<script>
export default {
  //数量统计
  props: ["farr"],
  //计算属性统计个数
  computed: {
    count() {
      return this.farr.length;
    },
  },
  //   变量isSel
  data() {
    return {
      isSel: "all", // 全部：'all' 已完成：'yes' 未完成： 'no'
    };
  },
  methods:{
    fn(){ //切换筛选的条件
        // 把类型字符串传给app.vue
        this.$emit("changeType",this.isSel)
    },
    clearFn(){ //清空已完成任务
    //触发app.vue里面的clearFun方法
        this.$emit("clear")
    }
  }
};
</script>