<template>
  <main>
    <div class="container">
      <h1>欢迎使用TodoList App</h1>
      <todo-add :tid="todos.length" @add-todo="addTodo" />
      <todo-filter :selected="filter" @change-filter="filter = $event" />
      <todo-list :todos="filteredTodos" />
    </div>
  </main>
</template>

<script>
import TodoAdd from "./components/TodoAdd";
import TodoFilter from "./components/TodoFilter";
import TodoList from "./components/TodoList";
import useTodos from "@/composables/useTodos.js";
import useFilteredTodos from "@/composables/useFilteredTodos.js";

export default {
  name: 'App',
  components: { TodoAdd, TodoFilter, TodoList },
  setup() {
    const { todos, addTodo } = useTodos();
    const { filter, filteredTodos } = useFilteredTodos(todos);
    
    return {
      todos,
      addTodo,
      filter,
      filteredTodos,
    };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Helvetica, "PingFang SC", "Microsoft Yahei", sans-serif; /* 字体设置 */
}

/* 整个页面 */
main {
  width: 100vw;
  min-height: 100vh; 
  /* grid布局，设置应用主界面居中 */
  display: grid;
  align-items: center;
  justify-items: center;
  background: rgb(203, 210, 240);
}

/* todo主界面 */
.container {
  width: 60%;
  max-width: 400px;
  box-shadow: 0px 0px 24px rgba(0, 0, 0, 0.15); /* 设置阴影 */
  border-radius: 24px; /* 设置圆角半径 */
  padding: 48px 28px; /* 设置内间距 */
  background-color: rgb(245, 246, 252);
}

/* 主界面标题 */
h1 {
  margin: 24px 0;
  font-size: 28px;
  color: #414874;
}
</style>
