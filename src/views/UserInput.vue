<template>
    <div>
        <el-form ref="form" :model="user" label-width="80px"  @submit.prevent="showData" >
          <el-form-item label="姓名" align="left">
            <el-input   v-model="user.name"></el-input>
          </el-form-item>
          <el-form-item label="年龄" align="left">
            <el-input v-model="user.age"></el-input>
          </el-form-item>
           <el-form-item label="职业" align="left">
            <el-input v-model="user.profession" ></el-input>
          </el-form-item>
        </el-form>
        <el-button type="primary" size =small @click="submitForm(user)">提交</el-button>
        <el-button type="danger" size =small @click='back'>返回</el-button>
    </div>
</template>
<script>
export default {
  name: 'UserInput',
  data () {
    return {
      user: {
        name: '',
        age: '',
        profession: ''
      }
    }
  },
  created () {
    if (this.$route.params.user) { this.user = this.$route.params.user }
  },
  methods: {
    submitForm () {
      this.$http.post(('http://localhost:8082/test/user/'), this.user).then(response => {
        alert('提交成功！')
        this.$router.push('users')
      }, response => {
        alert('出问题啦！')
        this.$router.push('users')
      })
    },
    back () {
      this.$router.push('users')
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
