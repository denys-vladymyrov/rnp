<template>
  <section class="flex flex-col max-w-xs p-6 items-start text-left">
    <label for="startInput">Enter arithmetic expression</label>
    <input type="text" id="startInput" class="form-input px-2 py-1" v-model="expression">
  </section>
</template>

<script>
  export default {
    name: 'App',
    data() {
      return {
        expression: '',
      }
    },
  }
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
