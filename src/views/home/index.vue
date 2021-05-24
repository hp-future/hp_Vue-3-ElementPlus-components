<template>
  <div id="home-container">
    <Table
        :tableData="tableData"
        :tableHeader="tableHeader"
        :border="true"
        @rowClickHandle="rowClick"
        @sortChangeHandle="sortChange"
    >
      <template #operation>
        <i class="operation-btn el-icon-edit"></i>
        <i class="operation-btn el-icon-delete"></i>
      </template>
      <template #haha>
        <el-button type="success">按钮</el-button>
      </template>
      <template #time-header>
        <span>时间</span>
        <i class="el-icon-top"></i>
      </template>
    </Table>
  </div>
</template>

<script>
import { reactive } from 'vue'

import Table from '../../components/table'

export default {
  name: "index",
  components: {
    Table
  },
  setup(){
    let tableData = reactive([])
    let tableHeader = reactive([])

    tableData = [
      { name: '123', sex: '男', age: 18, time: 1 },
      { name: '456', sex: '男', age: 18, time: 2 },
      { name: '789', sex: '男', age: 18, time: 3 },
    ]
    tableHeader = [
      { type: 'selection', width: '80' },
      { type: 'index', label: '序号', width: '100' },
      { prop: 'name', label: '姓名' },
      { prop: 'sex', label: '性别' },
      { prop: 'haha', label: '哈哈' },
      { prop: 'age', label: '年龄' },
      { prop: 'time', label: '时间', sortable: true },
      { prop: 'operation', label: '操作' },
    ]

    const sortChange = ({ column, prop, order }) => {
      console.log(column, prop, order)
    }

    return {
      tableData,
      tableHeader,
      rowClick,
      sortChange
    }
  }
}

const rowClick = (row, column, event) => {
  console.log(row, column, event)
}

</script>

<style scoped lang="scss">
#home-container {
  height: 100%;
  background-color: pink;
  .operation-btn {
    margin: 0 10px;
    cursor: pointer;
    font-size: 18px;
    font-weight: 400;
    &.el-icon-delete {
      color: red;
    }
    &.el-icon-edit {
      color: #409EFF;
    }
    &:hover {
      font-weight: bold;
    }
  }
}
</style>
