<template>
  <div id="wrapper">
    <img src="../assets/img/logo.png">
    <span>&nbsp;&nbsp;Todo App</span>
  </div>
</template>

<script>
export default {

}
</script>

<style>
  #wrapper {
    min-height: 120px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: yellow;
    box-shadow: rgba(0, 0, 0, 0.35) 0px 1px 10px;
  }

  #wrapper img {
    height: 70px;
  }

  #wrapper span {
    font-size: 26px;
    color: rgb(211, 77, 0);
    text-transform: uppercase;
    font-family: 'Anton', sans-serif;
  }
</style>