<script setup lang="ts">
import { reactive, defineEmits } from 'vue'

const todoState = reactive({
  todo: '',
  invalid: false,
  errorMessage: ''
})

const emit = defineEmits(['create-todo'])

const createTodo = (e: Event) => {
  e.preventDefault()
  todoState.invalid = false
  if (todoState.todo) {
    emit('create-todo', todoState.todo)
    todoState.todo = ''
    return
  }
  todoState.invalid = true
  todoState.errorMessage = 'Todo value cannot be empty'
}
</script>

<template>
  <p v-show="todoState.invalid" class="error-message">{{ todoState.errorMessage }}</p>
  <form
    @submit="(e) => createTodo(e)"
    class="input-wrap"
    :class="{ 'input-error': todoState.invalid }"
  >
    <input type="text" name="todo-creator" id="todo-creator" v-model="todoState.todo" />
    <button @click="(e) => createTodo(e)">Create</button>
  </form>
</template>

<style lang="scss" scoped>
.input-wrap {
  display: flex;
  transition: 250ms ease;
  border: 2px solid var(--primary-color);

  &.input-error {
    box-shadow: 0px 0px 8px 2px red;
  }

  input {
    width: 100%;
    padding: 0.5rem;
    border: none;
    background-color: var(--bg-color);

    &:focus {
      outline: none;
    }
  }

  button {
    padding: 0.5rem;
    border: none;
    background-color: var(--primary-color);
    color: var(--bg-color);
    cursor: pointer;
  }
}

.error-message {
  margin-bottom: 0.4rem;
  font-size: 0.8rem;
  text-align: center;
  color: red;
}
</style>
