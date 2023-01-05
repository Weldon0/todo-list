<template>
  <!-- 头部部分 -->
  <header class="header">
    <h1>todos</h1>
    <input
      class="new-todo"
      placeholder="请输入任务名称"
      autofocus
      v-model.trim="name"
      @keyup.enter="submit"
    />
  </header>
</template>

<script>
// 先把input输入框的数据绑定到data里面
// 按下回车键的时候可以获取到用户输入的内容

export default {
  data() {
    return {
      name: "",
    };
  },
  methods: {
    submit() {
      // 触发父组件的自定义事件add
      this.$emit("add", this.name);
      // 已经把内容提交了，输入框就可以置空了
      this.name = "";
    },
  },
};
</script>
