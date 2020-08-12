<template>
  <div id="app">
    <Header></Header>
    <Main></Main>
    <Number></Number>
  </div>
</template>

<script>
import Header from '@/components/Header'
import Number from '@/components/Number'
import Main from '@/components/Main'

export default {
  name: 'app',
  components: {
    Header,
    Number,
    Main
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Roboto', sans-serif;
}

*,
*::after,
*::before,
*:focus,
*:hover,
*:active {
  outline: none;
}

body {
  background-color: #18191a;
}
</style>
