<script setup>
import { onMounted, reactive, ref } from "vue";

const emit = defineEmits(["create"]);

const state = reactive({
  todo: "",
  invalid: false,
  errorMessage: "",
});

const create = () => {
  state.invalid = false;
  if (state.todo !== "") {
    emit("create", state.todo);
    state.todo = "";
    return;
  }
  state.invalid = true;
  state.errorMessage = "Todo value cannot be empty!";
};

const input = ref(null);

onMounted(() => {
  input.value.focus();
});
</script>

<template>
  <div class="input-wrap" :class="{ 'input-err': state.invalid }">
    <input
      type="text"
      ref="input"
      v-model="state.todo"
      v-on:keydown.enter="create"
    />
    <button @click="create">Create</button>
  </div>
  <p class="error-message" v-if="state.invalid">{{ state.errorMessage }}</p>
</template>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid #41b080;

  &.input-err {
    border-color: red;
  }

  &:focus-within {
    box-shadow: 0 -4px 6px -1px rgb(0 0 0 / 0.1),
      0 -2px 4px -2px rgb(0 0 0 / 0.1);
  }

  input {
    width: 100%;
    padding: 8px 6px;
    border: none;

    &:focus {
      outline: none;
    }
  }

  button {
    padding: 8px 16px;
    border: none;
  }
}

.error-message {
  margin-top: 6px;
  font-size: 12px;
  text-align: center;
  color: red;
}
</style>
