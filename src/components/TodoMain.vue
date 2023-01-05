<template>
  <!-- 主体部分 -->
  <section class="main">
    <input
      id="toggle-all"
      class="toggle-all"
      type="checkbox"
      v-model="isCheckAll"
    />
    <label for="toggle-all">Mark all as complete</label>
    <ul class="todo-list">
      <!-- 当任务已完成，可以给 li 加上 completed 类，会让元素加上删除线 -->
      <li
        :class="{ completed: item.isDone }"
        v-for="item in showList"
        :key="item.id"
      >
        <div class="view">
          <input
            class="toggle"
            type="checkbox"
            :checked="item.isDone"
            @change="changeIsDone(item.id)"
          />
          <label>{{ item.name }}</label>
          <button class="destroy" @click="del(item.id)"></button>
        </div>
      </li>
    </ul>
  </section>
</template>
<script>
export default {
  props: {
    list: {
      type: Array,
      required: true, // 必填项
    },
    type: String, // all  active  completed
  },
  computed: {
    showList() {
      if (this.type === "active") {
        // 获取未完成的数据
        // isDone为false
        return this.list.filter((item) => !item.isDone);
      } else if (this.type === "completed") {
        // 已完成的数据
        // isDone 为true
        return this.list.filter((item) => item.isDone);
      }
      // 如果上面两个条件都没有匹配到，证明是all，返回所有数据
      return this.list;
    },
    isCheckAll: {
      get() {
        // 判断是不是所有的数据全部都被选中
        // 每一项的isDone属性为true
        return this.list.every((item) => item.isDone);
      },
      /**
       * 修改isCheckAll属性触发的方法
       * @param {Boolean} newValue 全选框切换之后的最新的值
       */
      set(newValue) {
        // 触发父组件用于修改的toggleAll方法
        this.$emit("toggleAll", newValue);
      },
    },
  },
  methods: {
    del(id) {
      this.$emit("del", id);
    },
    changeIsDone(id) {
      // console.log(id)
      // 通知父组件自己修改数据
      //   子组件应该怎么触发方法
      this.$emit("changeIsDone", id);
    },
  },
};
</script>
