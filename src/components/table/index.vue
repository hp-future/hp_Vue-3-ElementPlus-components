<template>
  <el-table
      :data="tableData"
      style="width: 100%"
      height="100%"
      :border="border"
      @row-click="rowClick"
      id="custom__table"
      :default-sort = "{prop: 'name', order: 'descending'}"
      @sort-change="sortChange"
  >
    <el-table-column
        v-for="(item, index) in tableHeader"
        :key="index"
        :type="item.type"
        :align="item.align || 'center'"
        :width="item.width"
        :sortable="item.sortable || false"
        :prop="item.prop"
    >
      <template #header>
        <slot :name="item.prop + '-header'">
          <span>{{ item.label }}</span>
        </slot>
      </template>
      <template #default="{ row }" v-if="!item.type">
        <slot :name="item.prop" >
          <span>{{ row[item.prop] }}</span>
        </slot>
      </template>
    </el-table-column>
  </el-table>
</template>

<script>
import {  } from 'vue'

export default {
  name: "index",
  props: {
    tableData: {
      type: Array,
      default: () => []
    },
    tableHeader: {
      type: Array,
      default: () => []
    },
    border: {
      type: Boolean,
      default: false
    }
  },
  setup(props, { emit }) {

    /**
     * 单击表格某一行
     * @param row 行数据
     * @param column 列信息
     * @param event 事件对象
     */
    const rowClick = (row, column, event) => emit('rowClickHandle', row, column, event)

    const sortChange = ({ column, prop, order }) => emit('sortChangeHandle', { column, prop, order })

    return {
      rowClick,
      sortChange
    }
  }
}
</script>

<style lang="scss">
#custom__table {
  .caret-wrapper {
    display: none;
  }
}
</style>
