<template>
<!-- todo 列表 -->
    <div class="todo-list">
      <!-- todo 项目，外层容器用于显示背景、圆角边框 -->
      <TodoListItem v-for="(n, index) in 10" :key="n"></TodoListItem>   
    </div>
</template>

<script>
import TodoListItem from "./TodoListItem.vue"
export default{
    name: "TodoList",
    components: { TodoListItem }
}
</script>

<style>
.todo-list {
  display: grid;
  row-gap: 14px;
}
</style>

