<template>
  <div id="app">
    <div class="copyright">&copy; Copyright 2018 Private enterprise "Web Friends"<br /><a href="https://www.webfriends.by">www.webfriends.by</a></div>
    <pagination>Page #1</pagination>
    <pagination-controls></pagination-controls>

  </div>
</template>

<script>
import Pagination from './components/Pagination'

export default {
  name: 'App',
  components: {
    Pagination
  }
}
</script>

<style lang="scss">
  .copyright {
    padding: 30px 0 20px 0;
    text-align: center;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    font-size: 18px;
    opacity: 0.6;

    a {
      color: #02C8F3;

      &:visited {
        color: #02C8F3;
      }
    }
  }
</style>
