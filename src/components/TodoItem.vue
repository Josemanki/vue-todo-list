<script setup lang="ts">
// Props better as objects like these because a type can be defined for them
// Array would be `defineProps(['todo'])` which with TS could probably be less hassle for

import { Icon } from '@iconify/vue'

// same benefits?
defineProps({
  todo: {
    type: Object,
    required: true
  },
  index: {
    type: Number,
    required: true
  }
})
defineEmits(['toggle-complete', 'edit-todo', 'update-todo', 'delete-todo'])
</script>

<template>
  <li>
    <input type="checkbox" :checked="todo.isCompleted" @input="$emit('toggle-complete', index)" />
    <div class="todo">
      <input
        v-if="todo.isEditing"
        type="text"
        :value="todo.todo"
        @input="$emit('update-todo', ($event.target as HTMLInputElement).value, index)"
      />
      <span v-else :class="{ 'completed-todo': todo.isCompleted }">{{ todo.todo }}</span>
    </div>
    <div class="todo-actions">
      <Icon
        v-if="todo.isEditing"
        class="icon check-icon"
        icon="ph:check-circle"
        color="#41b080"
        width="1.5rem"
        @click="$emit('edit-todo', index)"
      />
      <Icon
        v-else
        class="icon edit-icon"
        icon="ph:pencil-fill"
        color="#41b080"
        width="1.5rem"
        @click="$emit('edit-todo', index)"
      />
      <Icon
        class="icon trash-icon"
        icon="ph:trash"
        color="#f95e5e"
        width="1.5rem"
        @click="$emit('delete-todo', todo.id)"
      />
    </div>
  </li>
</template>

<style lang="scss" scoped>
li {
  display: flex;
  align-items: center;
  gap: 0.8rem;

  &:hover {
    .todo-actions {
      opacity: 1;
    }
  }

  input[type='text'] {
    width: 100%;
    padding: 0.3rem;
    border: none;
    background-color: var(--bg-color);
    border: 2px solid var(--primary-color);

    &:focus {
      outline: none;
    }
  }

  input[type='checkbox'] {
    appearance: none;
    width: 1.2rem;
    height: 1.2rem;
    background-color: #fff;
    border-radius: 50%;

    &:checked {
      background-color: var(--green);
    }
  }

  .todo {
    flex: 1;

    .completed-todo {
      text-decoration: line-through;
    }
  }

  .todo-actions {
    display: flex;
    gap: 0.3rem;
    opacity: 0;
    transition: 150ms ease-in-out;

    .icon {
      cursor: pointer;
    }
  }
}
</style>
