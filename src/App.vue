<template>
  <section class="todoapp">
    <TodoHeader @add="add" />
    <TodoMain
      @toggleAll="toggleAll"
      :type="type"
      :list="list"
      @del="del"
      @changeIsDone="changeIsDone"
    />
    <!--只有list列表有内容的时候才展示footer组件-->
    <TodoFooter
      :type="type"
      @clearDone="clearDone"
      @filterType="filterType"
      :list="list"
      v-if="list.length"
    />
  </section>
</template>

<script>
// 引入组件
import TodoHeader from "@/components/TodoHeader.vue";
import TodoMain from "@/components/TodoMain.vue";
import TodoFooter from "@/components/TodoFooter.vue";

export default {
  // 注册组件
  components: { TodoFooter, TodoMain, TodoHeader },
  data() {
    return {
      type: "all", // 把子组件footer里面的变量提升到了父组件App.vue
      list: JSON.parse(localStorage.getItem("todo")) || [],
    };
  },
  watch: {
    list: {
      handler(newList) {
        // 已经可以拿到变化之后的最新的值，存储到本地存储
        localStorage.setItem("todo", JSON.stringify(newList));
      },
      deep: true, // 开启深度监听
    },
  },
  methods: {
    /**
     * 点击全选按钮，切换所有子项的状态
     * @param {Boolean} status  全选框最新的状态
     */
    toggleAll(status) {
      this.list.forEach((item) => {
        item.isDone = status;
      });
    },
    filterType(type) {
      // 子组件不能直接修改父组件传递过来的基本值
      this.type = type;
    },
    /**
     * 清除已经完成的list项
     * @param {MouseEvent} e
     */
    clearDone(e) {
      // 清除已经完成的项，filter方法
      this.list = this.list.filter((item) => !item.isDone);
    },
    /**
     * 删除todo
     * @param {String} id - 即将删除的数据的id
     * @returns {void}
     */
    del(id) {
      this.list = this.list.filter((item) => item.id !== id);
    },
    /**
     * todo的添加逻辑
     * @param name
     */
    add(name) {
      console.log(name);
      // 开始添加的逻辑
      //   如果用户有没有填写name，进行弹框提示，return代码
      if (!name) {
        alert("请输入内容");
        return;
      }

      //   证明用户填写内容了
      this.list.unshift({
        id: Date.now(),
        name,
        isDone: false,
      });
    },
    changeIsDone(id) {
      //   拿到切换状态的id了
      //   遍历数字，找到id对应的这一项，然后切换他的状态
      this.list.forEach((item) => {
        if (item.id === id) {
          //   直接把当前数据的isDone属性取反
          item.isDone = !item.isDone;
        }
      });
    },
  },
};
</script>

<style></style>
