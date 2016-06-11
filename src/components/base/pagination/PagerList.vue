<template>
      <pager v-for="i in maxPage" :root-prefix-cls="rootPrefixCls" :page="i+1" :active="i+1===current" :last="i+1===maxPage" @click="gotoPage(i+1)"></pager>
</template>

<script>
  import Pager from './Pager.vue'

  export default {
    props: {
      maxPage: Number,
      current: Number,
      rootPrefixCls: String,
    },

    methods: {
      gotoPage(p) {
        this.$emit('goto', p)
      }
    },

    components: {
      Pager
    }
  }
</script>
