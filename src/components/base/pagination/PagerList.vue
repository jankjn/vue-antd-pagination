<template>
  <div>
    <div v-if="maxPage <= 9">
      <pager v-for="i in maxPage" :root-prefix-cls="rootPrefixCls" :page="i+1" :active="i+1===current" :last="i+1===maxPage" @click="gotoPage(i+1)"></pager>
    </div>
    <div v-else>
      <pager v-if="current - 2 > 1" :root-prefix-cls="rootPrefixCls" :page="1" :active="1===current" :last="false" @click="gotoPage(1)"></pager>
      <li v-if="current - 2 > 2" title="previus 5 page" @click="gotoPage(current-5)" :class="`${rootPrefixCls}-jump-prev`"><a></a>
      </li>
      <pager v-for="i in range" :root-prefix-cls="rootPrefixCls" :page="i" :active="i===current" :last="i===maxPage" @click="gotoPage(i)"></pager>
      <li v-if="current + 2 < maxPage - 1" title="next 5 page" @click="gotoPage(current+5)" :class="`${rootPrefixCls}-jump-next`"><a></a>
      </li>
      <pager v-if="current + 2 < maxPage" :root-prefix-cls="rootPrefixCls" :page="maxPage" :active="maxPage===current" :last="true" @click="gotoPage(maxPage)"></pager>
    </div>
  </div>
</template>

<script>
  import Pager from './Pager.vue'

  export default {
    props: {
      maxPage: Number,
      current: Number,
      rootPrefixCls: String,
    },

    computed: {
      range() {
        if (this.current - 2 < 1) {
          return [1, 2, 3, 4, 5]
        } else if (this.current + 2 > this.maxPage) {
          const m = this.maxPage
          return [m-4, m-3, m-2, m-1, m]
        } else {
          const c = this.current
          return [c-2, c-1, c, c+1, c+2]
        }
      },
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
