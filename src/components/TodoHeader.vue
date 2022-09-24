<template>
  <header class="header">
    <h1>TodoList</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll" />
    <label for="toggle-all"></label>
    <!-- 键盘事件，回车输入 -->
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      @keydown.enter="downFn"
      v-model="task"
    />
  </header>
</template>

<script>
//新增任务
export default {
  data() {
    return {
      task: "",
    };
  },
  methods: {
    downFn() {
      // 当前任务添加到list数组里
      // 子传父技术
      this.$emit("create", this.task);
      this.task = "";
    },
  },
  computed: {
    isAll: {
      set(checked) {
        this.arr.forEach((obj) => (obj.isDone = checked));
      },
      get() {
        return this.arr.every((obj) => obj.isDone === true);
      },
    },
  },
  props: ["arr"],
};
</script>