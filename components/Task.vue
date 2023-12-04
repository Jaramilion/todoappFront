

<template>

    <span :class="{ done: task.done }" @click="doneTodo()">{{ task.content }}</span>
    <button  @click="removeTodo()">Remove</button>

</template>

<script setup lang="ts">

    const props = defineProps({
        task: {
            done: Boolean,
            content: String
        },
        doneTodo: Function,
        removeTodo: Function
    })
</script>

<style lang="scss">
$border: 1px solid;
$size1: 6px;
$size2: 12px;
$size4: 24px;
body {
  #__nuxt {
    max-width: 600px;
      li {
        display: flex;
        justify-content: space-between;
        align-items: center;
        border: $border;
        padding: $size2 $size4;
        border-radius: $size1;
        margin-bottom: $size2;
        span {
          cursor: pointer;
        }
        .done {
          text-decoration: line-through;
        }
        button {
          font-size: $size2;
          padding: $size1;
        }
      }
    
  }
}
</style>