<template>
  <div :style="`height:calc(90vh)`">

    <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" style="margin-bottom: 20px"
             background-color="#545c64"
             text-color="#fff"
             active-text-color="#ffd04b">
      <el-menu-item index="1">日程安排</el-menu-item>
    </el-menu>
    <template>
      <el-table
        :data=getTableData
        :max-height="`calc(80vh)`"
        :height="`calc(80vh)`"
        border
        :style="`width: 100%`">
        <el-table-column
          prop="createDate"
          label="创建日期"
          sortable
          width="180">
        </el-table-column>
        <el-table-column
          prop="name"
          label="姓名"
          sortable
          width="80">
        </el-table-column>
        <el-table-column
          prop="startTime"
          sortable
          label="开始时间"
          width="180">
        </el-table-column>
        <el-table-column
          prop="endTime"
          sortable
          label="结束时间"
          width="180">
        </el-table-column>
        <el-table-column
          prop="taskDescription"
          sortable
          label="任务描述">
        </el-table-column>
        <el-table-column
          prop="isComplete"
          sortable
          label="完成情况">
        </el-table-column>
      </el-table>
    </template>
    <div class="block" style="float:right">
      <el-pagination
        @current-change="changePage"
        layout="prev, pager, next"
        :page-size="10"
        :total="tableData.length">
      </el-pagination>
    </div>

  </div>
</template>

<script>
  export default {
    name: 'App',

    mounted () {
      this.$ajax.get('/static/data' + '.json')
        .then(response => {
          response.data.forEach((item, index) => {

            this.tableData.push(item)
          })

          console.log(this.tableData)
        })
    },

    computed: {
      getTableData () {

        var showDataRangeMax = this.currentPage * 10
        var showDataRangeMin = (this.currentPage - 1) * 10
        var showData = new Array()
        this.tableData.forEach((item, index) => {
          if (index >= showDataRangeMin && index < showDataRangeMax) {
            showData.push(item)
          }
        })

        return showData
      }
    },

    data () {
      return {
        currentPage: 1,
        activeIndex: '1',
        tableData: []
      }
    },

    methods: {
      changePage (page) {

        this.currentPage = page
      }
    }

  }


</script>

<style>

</style>
