 <template>
 <div>
  <el-button plain style="float: left;" type="primary" size =small @click='createUser'>新建</el-button>
    <el-table
      :data="tableData.filter(data => !search || data.name.toLowerCase().includes(search.toLowerCase()))"
      style="width: 100%">
      <el-table-column
        prop="name"
        label="姓名"
        width="180">
      </el-table-column>
      <el-table-column
        prop="age"
        label="年龄"
        width="180">
      </el-table-column>
       <el-table-column
        prop="profession"
        label="职业"
        width="180">
      </el-table-column>
      <el-table-column  align="right" >
        <template slot="header" slot-scope="scope">
        <el-input
        style="width:300px"
          v-model="search"
          size="mini"
          placeholder="输入关键字搜索" />
      </template>
      <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.$index, scope.row)">删除</el-button>
      </template>
    </el-table-column>
    </el-table>
</div>
  </template>

<script>
export default {
  name: 'UserList',
  data () {
    return {
      tableData: [],
      search: ''
    }
  },
  created () {
    this.$http('http://localhost:8082/test/users/').then(response => {
      this.tableData = response.data
    })
  },
  methods: {
    createUser () {
      this.$router.push('user-input')
    },
    handleDelete (index, row) {
      console.log(row)
      this.$http.delete('http://localhost:8082/test/users/' + row.id).then(response => {
        alert('删除成功！')
        this.tableData.splice(index, 1)
      }, response => {
        alert('出问题啦！')
        this.$router.push('users')
      })
    },
    handleEdit (index, row) {
      console.log(this.tableData[index])
      this.$router.push({ name: 'user-input', params: { user: this.tableData[index] } })
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
