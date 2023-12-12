<script setup>
import { Icon } from "@iconify/vue";

const props = defineProps({
  todo: {
    type: Object,
    required: true,
    default: () => {},
  },
  index: {
    type: Number,
    required: true,
    default: 0,
  },
});

const emit = defineEmits([
  "toggle-complete",
  "toggle-edit",
  "update-todo",
  "delete-todo",
]);

const toggleComplete = () => {
  emit("toggle-complete", props.index);
};

const toggleEdit = () => {
  emit("toggle-edit", props.index);
};

const updateTodo = (event) => {
  emit("update-todo", event.target.value, props.index);
};

const deleteTodo = () => {
  emit("delete-todo", props.todo);
};
</script>

<template>
  <li>
    <input
      type="checkbox"
      :checked="todo.isCompleted"
      @input="toggleComplete"
    />
    <div class="todo">
      <input
        v-if="todo.isEditing"
        type="text"
        ref="input"
        :value="todo.todo"
        @input="updateTodo"
        v-on:keydown.enter="toggleEdit"
      />
      <span v-else :class="{ 'completed-todo': todo.isCompleted }">
        {{ todo.todo }}
      </span>
    </div>
    <div class="todo-actions">
      <Icon
        v-if="todo.isEditing"
        icon="ph:check-circle"
        class="icon check-icon"
        color="41b080"
        width="22"
        @click="toggleEdit"
      />
      <Icon
        v-else
        icon="ph:pencil-fill"
        class="icon edit-icon"
        color="41b080"
        width="22"
        @click="toggleEdit"
      />
      <Icon
        icon="ph:trash"
        class="icon trash-icon"
        color="f95e5e"
        width="22"
        @click="deleteTodo"
      />
    </div>
  </li>
</template>

<style lang="scss" scoped>
li {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 16px 10px;
  background-color: #f1f1f1;
  box-shadow: 0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);

  &:hover {
    .todo-actions {
      opacity: 1;
    }
  }

  input[type="checkbox"] {
    appearance: none;
    width: 20px;
    height: 20px;
    background-color: #fff;
    border-radius: 50%;
    box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
    cursor: pointer;

    &:checked {
      background-color: #41b080;
    }
  }

  .todo {
    flex: 1;

    input[type="text"] {
      width: 100%;
      padding: 2px 6px;
      border: 2px solid #41b080;
    }

    .completed-todo {
      text-decoration: line-through;
    }
  }

  .todo-actions {
    display: flex;
    gap: 6px;
    opacity: 0;
    transition: 150ms ease-in-out;
    .icon {
      cursor: pointer;
    }
  }
}
</style>
