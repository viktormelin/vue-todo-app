<script setup lang="ts">
import { ref } from 'vue'
import { createId } from '@paralleldrive/cuid2'
import type { Todo } from './types'

const todos = ref<Todo[]>([])
const todoNameInput = ref('')

const addTodoItem = () => {
  if (todoNameInput.value.length > 0) {
    console.log('pushing to todo list')

    todos.value.push({
      id: createId(),
      name: todoNameInput.value,
      done: false
    })

    console.log(todos)
  }
}
</script>

<template>
  <main
    class="flex items-center justify-center flex-col h-screen w-screen bg-slate-800 text-slate-50"
  >
    <div
      class="h-[50vh] w-[30vw] bg-slate-700 shadow-md rounded-sm px-5 py-5 flex flex-col justify-between items-center"
    >
      <div class="flex flex-col w-full gap-2">
        <h1 class="text-xl font-bold mb-3">Todo App</h1>
        <div v-if="todos.length <= 0"><p>No todos left</p></div>
        <div v-for="item in todos" :key="item.id">
          <div class="flex justify-between items-center w-full bg-slate-500 p-1 pl-3 rounded-md">
            <p :class="`${item.done && 'line-through'}`">{{ item.name }}</p>
            <div>
              <input type="checkbox" :id="item.id" v-model="item.done" class="hidden peer" />
              <label
                :for="item.id"
                class="inline-flex items-center justify-between px-2 py-1 rounded-md cursor-pointer bg-blue-500 peer-checked:border-blue-600 peer-checked:bg-green-600 hover:bg-blue-600"
              >
                <div class="block">
                  <p class="text-md">Completed!</p>
                </div>
              </label>
            </div>
          </div>
        </div>
      </div>
      <form class="flex flex-col gap-2 w-full">
        <input
          type="text"
          v-model="todoNameInput"
          id="newTodoInput"
          placeholder="Label"
          class="w-full text-sm bg-slate-500 rounded-sm p-2 border-0 text-slate-50 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-blue-400"
        />
        <button
          v-on:click.prevent="addTodoItem"
          class="rounded-sm bg-blue-500 hover:bg-blue-600 cursor-pointer flex items-center justify-center p-1"
        >
          Add todo item
        </button>
      </form>
    </div>
  </main>
</template>

<style scoped></style>
