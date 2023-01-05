<template>
  <!-- 底部部分 -->
  <footer class="footer">
    <span class="todo-count">
      <strong>
        {{ leftCount }}
      </strong>
      剩余
    </span>
    <ul class="filters">
      <li>
        <a
          :class="{ selected: type === 'all' }"
          href="#/"
          @click="filterType('all')"
          >全部</a
        >
      </li>
      <li>
        <a
          :class="{ selected: type === 'active' }"
          href="#/active"
          @click="filterType('active')"
          >进行中</a
        >
      </li>
      <li>
        <a
          :class="{ selected: type === 'completed' }"
          href="#/completed"
          @click="filterType('completed')"
          >已完成</a
        >
      </li>
    </ul>
    <button v-show="isShowClearDone" class="clear-completed" @click="clearDone">
      清除已完成
    </button>
  </footer>
</template>
<script>
/**
 * 需求1：只有有了待办的列表项的时候才展示footer，如果没有列表项不用展示footer
 *
 * 1、data里面定义一个type类型，默认为all，默认名字为【全部】的按钮
 * 2、三个按钮全部添加点击事件，当按钮的点击事件触发的时候，会把type类型进行修改 all  active completed
 * 3、三个按钮添加动态class，只有type类型等于自己需要的当前类型的时候，selected类名才会生效，高亮效果才会出现
 */
export default {
  props: {
    // 【所有的列表项数据，从父组件传递过来的】
    list: {
      type: Array,
      required: true,
    },
    type: {
      type: String, // 指定父组件传递过来的type属性的类型
    },
  },
  computed: {
    leftCount() {
      // 可以获取到所有未完成的数量
      return this.list.filter((item) => item.isDone === false).length;
    },
    // 【是否展示清楚已完成的按钮】
    // 【什么时候需要展示清除已完成的按钮?】
    // 【list里面只要有一个数据的isDone属性为true，就需要展示按钮】
    isShowClearDone() {
      // 使用some方法进行数据的判断
      return this.list.some((item) => item.isDone);
    },
  },
  methods: {
    clearDone() {
      //   触发父组件的清除方法
      this.$emit("clearDone");
    },
    filterType(type) {
      // 子组件不能直接修改父组件传递过来的基本值
      // this.type = type;
      this.$emit("filterType", type);
    },
  },
  data() {
    return {
      // type: "all", // 默认选中所有
    };
  },
};
</script>
