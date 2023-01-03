<template>
  <section class="todoapp">
    <TodoHeader/>
    <TodoMain :list="list"/>
    <TodoFooter/>
  </section>
</template>

<script>
// 引入组件
import TodoHeader from "@/components/TodoHeader.vue";
import TodoMain from "@/components/TodoMain.vue";
import TodoFooter from "@/components/TodoFooter.vue";

export default {
  // 注册组件
  components: {TodoFooter, TodoMain, TodoHeader},
  data() {
    return {
      list: [
        {id: 1, name: '吃饭', isDone: true},
        {id: 2, name: '睡觉', isDone: false},
        {id: 3, name: '打豆豆', isDone: true}
      ]
    }
  },
}
</script>

<style></style>
