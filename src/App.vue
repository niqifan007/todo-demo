<template>
  <section class="todoapp">
    <!-- 除了驼峰, 还可以使用-转换链接 -->
    <TodoHeader :arr="list" @create="createFn"></TodoHeader>
    <TodoMain :arr="showArr" @del="deleteFn"></TodoMain>
    <TodoFooter
      :farr="showArr"
      @changeType="typeFn"
      @clear="clearFun"
    ></TodoFooter>
  </section>
</template>

<script>
// 1.0 样式引入
import "./styles/base.css";
import "./styles/index.css";

import TodoHeader from "./components/TodoHeader";
import TodoMain from "./components/TodoMain";
import TodoFooter from "./components/TodoFooter";

export default {
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  data() {
    return {
      list: JSON.parse(localStorage.getItem("todoList")) || [],
      // 中转接收类型字符串
      getSel: "all", // 默认显示全部
    };
  },
  methods: {
    createFn(taskName) {
      //添加任务
      let id =
        this.list.length == 0 ? 100 : this.list[this.list.length - 1].id + 1;
      this.list.push({
        id: id,
        name: taskName,
        isDone: false,
      });
    },
    deleteFn(theId) {
      //删除任务
      let index = this.list.findIndex((obj) => obj.id === theId);
      this.list.splice(index, 1);
    },
    typeFn(str) {
      this.getSel = str;
    },
    clearFun() {
      this.list = this.list.filter((obj) => obj.isDone === false);
      //筛选出未完成的
    },
  },
  computed: {
    showArr() {
      if (this.getSel === "yes") {
        return this.list.filter((obj) => obj.isDone === true);
      } else if (this.getSel === "no") {
        return this.list.filter((obj) => obj.isDone === false);
      } else {
        return this.list; //全部显示
      }
    },
  },
  watch: {
    list: {
      deep: true,
      handler() {
        localStorage.setItem("todoList", JSON.stringify(this.list));
      },
    },
  },
};
</script>