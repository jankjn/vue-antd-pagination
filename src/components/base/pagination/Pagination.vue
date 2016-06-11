<template>
  <div>
    <ul :class="[prefixCls, className, (simple ? prefixCls+'-simple' : ''), ( !simple && mini ? 'mini' : '')]" unselectable>
      <span v-if="showTotal" class="ant-pagination-total-text">共 80 条</span>
      <li
        title="Previous Page"
        @click="prev"
        :class="(hasPrev ? '' : `${prefixCls}-disabled `) + prefixCls + '-prev'">
        <a></a>
      </li>

      <div v-if="simple" :title="'Page ' + current + ' of ' + maxPage" :class="`${prefixCls}-simple-pager`">
        <input type="text"
        v-model="currentInput"
        number
        @change.stop="handleChange(+$event.target.value)">
        <span :class="`${prefixCls}-slash`">/</span>
        {{ maxPage }}
      </div>
      <div v-else>
        <pager-list :max-page="maxPage" :current="current" :root-prefix-cls="prefixCls" @goto="handleChange"></pager-list>
      </div>

      <li title="Next Page"
        @click="next"
        :class="(hasNext ? '' : `${prefixCls}-disabled `) + `${prefixCls}-next`">
        <a></a>
      </li>
    </ul>
  </div>
</template>

<script>
  import PagerList from './PagerList.vue'

  export default {
    props: {
      current: {
        default: 1,
        type: Number,
        twoWay: true,
      },
      total: {
        default: 0,
        type: Number,
      },
      simple: {
        default: false,
        type: Boolean
      },
      pageSize: {
        default: 10,
        type: Number,
      },
      className: {
        default: '',
        type: String,
      },
      prefixCls: {
        default: 'ant-pagination',
        type: String,
      },
      showTotal: {
        default: false,
        type: Boolean,
      },
      mini: {
        default: false,
        type: Boolean,
      },
    },

    data () {
      return {
        currentInput: this.current
      }
    },

    computed: {
      hasPrev() {
        return this.current > 1
      },

      hasNext() {
        return this.current < this.calcMaxPage()
      },

      maxPage() {
        return this.calcMaxPage()
      }
    },

    methods: {
      calcMaxPage (pageSize) {
        if (typeof pageSize === 'undefined') {
          pageSize = this.pageSize
        }

        return Math.ceil(this.total / pageSize)
      },

      validatePage (page) {
        return typeof page === 'number' && page >= 1 && page !== this.current
      },

      handleChange (page) {
        let _page = page

        if (_page < 1) {
          _page = 1
        }

        if (this.validatePage(_page)) {
          if (_page > this.maxPage) {
            _page = this.maxPage
          }

          this.current = _page
          this.currentInput = this.current
          this.$emit('change', _page, this.pageSize)

          return _page
        }

        return this.current
      },

      prev() {
        if (this.hasPrev) {
          this.handleChange(this.current - 1)
        }
      },

      next() {
        if (this.hasNext) {
          this.handleChange(this.current + 1)
        }
      },
    },
    components: {
      PagerList,
    },
  }

</script>
