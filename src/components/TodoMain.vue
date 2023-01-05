<template>
  <!-- 主体部分 -->
  <section class="main">
    <input id="toggle-all" class="toggle-all" type="checkbox"/>
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <!-- 当任务已完成，可以给 li 加上 completed 类，会让元素加上删除线 -->
      <li :class="{completed: item.isDone}" v-for="item in list" :key="item.id">
        <div class="view">
          <input class="toggle" type="checkbox" :checked="item.isDone" @change="changeIsDone(item.id)"/>
          <label>{{ item.name }}</label>
          <button class="destroy" @click="del(item.id)"></button>
        </div>
      </li>
      <!--      <li>-->
      <!--        <div class="view">-->
      <!--          <input class="toggle" type="checkbox"/>-->
      <!--          <label>行万里路</label>-->
      <!--          <button class="destroy"></button>-->
      <!--        </div>-->
      <!--      </li>-->
    </ul>
  </section>
</template>

<script>
export default {
  props: {
    list: {
      type: Array,
      required: true, // 必填项
    }
  },
  methods: {
    del(id) {
      this.$emit('del', id)
    },
    changeIsDone(id) {
      // console.log(id)
      // 通知父组件自己修改数据
    //   子组件应该怎么触发方法
      this.$emit('changeIsDone', id)
    }
  },
}
</script>

