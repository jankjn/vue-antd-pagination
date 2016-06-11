<template>
<Pagination
  :prefix-cls="className"
  :current="current"
  :total="total"
  :page-size="pageSize"
  :on-change="onChange"
  :simple="simple"></Pagination>
</template>

<script>
import Pagination from '../base/pagination'
import { defaultProps } from '../../utils'

export default {
  props: defaultProps({
    current: 1, // 当前页数
    total: 0, // 数据总数
    pageSize: 10, // 每页条数
    onChange: () => {}, // 页码改变的回调，参数是改变后的页码
    className: 'ant-pagination', // 当为「mini」时，是小尺寸分页
    simple: Boolean // 当添加该属性时，显示为简单分页
  }),

  components: { Pagination }
}


</script>
