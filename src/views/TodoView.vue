<script setup>
import { ref } from "vue";
import { uid } from "uid";
import { Icon } from "@iconify/vue";
import TodoCreator from "../components/TodoCreator.vue";
import TodoItem from "../components/TodoItem.vue";

const todos = ref([]);

const create = (todo) => {
  todos.value.push({
    id: uid(),
    todo,
    isCompleted: false,
    isEditing: false,
  });
};

const toggleComplete = (position) => {
  todos.value[position].isCompleted = !todos.value[position].isCompleted;
};

const toggleEdit = (position) => {
  todos.value[position].isEditing = !todos.value[position].isEditing;
};

const updateTodo = (value, position) => {
  todos.value[position].todo = value;
};

const deleteTodo = (todo) => {
  todos.value = todos.value.filter((e) => e.id !== todo.id);
};
</script>

<template>
  <main>
    <h1>Create Todo</h1>
    <TodoCreator @create="create" />
    <ul class="todo-list" v-if="todos.length > 0">
      <template v-for="(todo, index) in todos" :key="todo.id">
        <TodoItem
          :index="index"
          :todo="todo"
          @toggle-complete="toggleComplete"
          @toggle-edit="toggleEdit"
          @update-todo="updateTodo"
          @delete-todo="deleteTodo"
        />
      </template>
    </ul>
    <p v-else class="todos-msg">
      <Icon icon="ph:smiley-sad" width="30" />
      <span>You have no todo's to complete! Add one!</span>
    </p>
  </main>
</template>

<style lang="scss" scoped>
main {
  display: flex;
  flex-direction: column;
  max-width: 500px;
  width: 100%;
  margin: 0 auto;
  padding: 40px 16px;

  h1 {
    margin-bottom: 16px;
    text-align: center;
  }

  .todo-list {
    display: flex;
    flex-direction: column;
    list-style: none;
    margin-top: 24px;
    gap: 20px;
  }

  .todos-msg {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
    margin-top: 24px;
  }
}
</style>
