<template>
  <div id="app">
    <pagination simple :current.sync="val" :total="400" @change="changePage"></pagination>
  </div>
</template>

<script>
  import Pagination from './components/base/pagination/'

  export default {
    data () {
      return {
        val: 1
      }
    },
    methods: {
      changePage(page, size) {
        console.info(page, size)
      }
    },
    components: {
      Pagination
    }
  }
</script>

<style>
  body {
    font-family: Helvetica, sans-serif;
  }
</style>
