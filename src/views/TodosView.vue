<script setup lang="ts">
import TodoCreator from '@/components/TodoCreator.vue'
import TodoItem from '@/components/TodoItem.vue'
import ConfettiExplosion from 'vue-confetti-explosion'
import { Icon } from '@iconify/vue'
import { uid } from 'uid'
import { computed, ref, watch } from 'vue'

// Small hack to not have to type the lib :)
const Confetti = ConfettiExplosion as any

interface Todo {
  id: string
  todo: string
  isCompleted: boolean
  isEditing: boolean
}

const todoList = ref<Todo[]>([])

const setTodoListLocalStorage = () => {
  localStorage.setItem('todoList', JSON.stringify(todoList.value))
}

watch(todoList, setTodoListLocalStorage, { deep: true })

const todoCompleted = computed(() => todoList.value.every((todo) => todo.isCompleted))

const getTodoListLocalStorage = () => {
  todoList.value = JSON.parse(localStorage.getItem('todoList') || '[]')
}

getTodoListLocalStorage()

const createTodo = (todo: string) => {
  todoList.value.push({
    id: uid(),
    todo,
    isCompleted: false,
    isEditing: false
  })
}

const toggleTodoComplete = (index: number) => {
  todoList.value[index].isCompleted = !todoList.value[index].isCompleted
}

const toggleEditTodo = (index: number) => {
  todoList.value[index].isEditing = !todoList.value[index].isEditing
}

const updateTodo = (todoText: string, index: number) => {
  todoList.value[index].todo = todoText
}

const deleteTodo = (todoId: string) => {
  todoList.value = todoList.value.filter((todo) => todoId !== todo.id)
}
</script>

<template>
  <main>
    <div class="wrapper">
      <h2>Create Todo</h2>
      <TodoCreator @create-todo="createTodo" />
      <ul class="todos">
        <li v-if="!todoList.length" class="empty-text">
          <Icon icon="noto-v1:sad-but-relieved-face" color="#41b080" width="1.5rem" />
          You have no todos yet! Add one!
        </li>
        <TodoItem
          v-for="(todo, index) in todoList"
          v-bind:key="todo.id"
          :todo="todo"
          :index="index"
          @toggle-complete="toggleTodoComplete"
          @edit-todo="toggleEditTodo"
          @update-todo="updateTodo"
          @delete-todo="deleteTodo"
        />
      </ul>
      <p class="todos-completed" v-if="todoCompleted && todoList.length > 0">
        <Icon icon="noto-v1:party-popper" />
        <span>You have completed all your todos!</span>
        <span class="confetti-wrapper"><Confetti /></span>
      </p>
    </div>
  </main>
</template>

<style lang="scss" scoped>
main {
  height: calc(100vh - 70px);
  width: 100%;
  overflow: hidden;

  .wrapper {
    display: flex;
    padding: 3rem 1rem;
    flex-direction: column;
    max-width: 500px;
    height: 100%;
    margin: 0 auto;
  }

  h2 {
    margin-bottom: 1rem;
    text-align: center;
  }

  .empty-text {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 0.5rem;
  }

  .todos {
    padding: 1rem 0.5rem;
    background-color: var(--bg-color-alt);
    border-radius: 0 0 8px 8px;
    max-height: 55vh;
    overflow-y: scroll;
  }

  .todos-completed {
    text-align: center;
    margin-top: 0.8rem;
  }
}
</style>
