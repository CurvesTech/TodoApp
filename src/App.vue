<template>
  <div>
    <TopBar></TopBar>
    <TodoApp></TodoApp>
    <Footer></Footer>
  </div>
</template>

<script>
import TopBar from './components/TopBar.vue';
import TodoApp from './components/TodoApp.vue';
import Footer from './components/Footer.vue';

export default {
  name: 'App',
  components: {
    TopBar,
    TodoApp,
    Footer
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Anton&family=Source+Sans+Pro:wght@300&display=swap');
  * {
    margin: 0;
    padding: 0;
  }

  body {
    font-family: 'Source Sans Pro', sans-serif;
  }
</style>
