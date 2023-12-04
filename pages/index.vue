<template>
    <h1>To-do App</h1>
  <form @submit.prevent="addTask()">
    <label>New todo </label>
    <input v-model="newTask" name="newTask"  />
    <button @click="addTask()">Add to-do</button>
  </form>
  <h3>To-do List</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="index">

        <Task
        :task="task" 
        :doneTodo="()=>toggleTask(task)" 
        :removeTodo="()=>removeTask(index)"
        />
    </li>
  </ul>
  <h4 v-if="tasks.length === 0">Empty list.</h4>
  </template>

<script setup lang="ts">
import { ref } from 'vue'
const newTask = ref('')
const defaultData = [
  {
    done: true,
    content: 'Write a blog post'
  },
  {
    done: false,
    content: 'Listen a podcast'
  }
]
const tasksData = defaultData
const tasks = ref(tasksData)
function addTask() {
  if (newTask.value) {
    tasks.value.push({
      done: false,
      content: newTask.value
    })
    newTask.value = ''
  }
  saveData()
}
function toggleTask(task) {
  task.done = !task.done
  saveData()
}
function removeTask(index) {
  tasks.value.splice(index, 1)
  saveData()    
}
function saveData() {
  $cookies.set('tasks', tasks.value)
}
useHead({
  title: 'To-do App',
})
</script>

<style lang="scss">
$border: 1px solid;
$size1: 6px;
$size2: 12px;
$size3: 18px;
$size4: 24px;
$size5: 48px;
$backgroundColor: #ffffff;
$textColor: #000;
$primaryColor: #12c9ff;
$secondTextColor: #1f2023;
body {
  margin: 0;
  padding: 0;
  background-color: $backgroundColor;
  color: $textColor;
  #__nuxt {
    margin-left: auto;
    margin-right: auto;
    padding: 20px;
    form {
      display: flex;
      flex-direction: column;
      width: 100%;
      label {
        font-size: 14px;
        font-weight: bold;
      }
      input,
      button {
        height: $size5;
        box-shadow: none;
        outline: none;
        padding-left: $size2;
        padding-right: $size2;
        border-radius: $size1;
        font-size: 18px;
        margin-top: $size1;
        margin-bottom: $size2;
      }
      input {
        background-color: transparent;
        border: $border;
        color: inherit;
      }
    }
    button {
      cursor: pointer;
      background-color: $primaryColor;
      border: 1px solid $primaryColor;
      color: $secondTextColor;
      font-weight: bold;
      outline: none;
      border-radius: $size1;
    }
    h3 {
      font-size: 22px;
      border-bottom: $border;
      padding-bottom: $size1;
      
    }
    ul {
      padding: 10px;
      margin-top: 1%;
    }
    h4 {
      text-align: center;
      opacity: 0.5;
      margin: 0;
    }
  }
}
</style>
