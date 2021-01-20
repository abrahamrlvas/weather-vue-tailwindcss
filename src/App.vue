<template>
  <div id="app">
    <Form/>
  </div>
</template>

<script>
import Form from './components/Form.vue';

export default {
  name: 'App',
  components: {
    Form
  }
}
</script>

<style>
body{
  margin: 0; 
  padding: 0;
  text-align: center;
  background-color: #182a3f;
  min-height: 100%;
  color: white;
}
</style>
