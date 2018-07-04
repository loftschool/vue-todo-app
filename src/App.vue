<template lang="pug">
  .container
    router-view
</template>

<script>
import todo from './components/todo';

export default {
  name: 'app',
  components: {
    todo
  },
  data () {
    return {
    }
  }
}
</script>

<style lang="scss">
  body {
    font-family: "Helvetica Neue", Helvetica, sans-serif;
    font-size: 16px;
    line-height: 1.42;
    -webkit-font-smoothing: antialiased;
    font-weight: 300;
    background: #f5f5f5;
  }

  .container {
    width: 600px;
    margin: 0 auto;
  }

  ul {
    margin: 0;
    padding: 0;

    li {
      list-style: none;
    }
  }

  * {
    box-sizing: border-box;
  }
</style>
