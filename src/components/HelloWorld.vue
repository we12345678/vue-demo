<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    姓名：<input v-model="user.name"/>
    年龄:<input v-model="user.age"/>
    <button @click="submit">提交</button>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data () {
    return {
      user: {
        name: '张三',
        age: '18'
      }

    }
  },
  methods: {
    submit () {
      // console.log(this.name + ':' + this.age)
      this.name = 'TOM'
      // let vm = this
      this.age = '5'
      // this.$http.get('test/data.json').then(function (response) {
      //   vm.user = response.data
      this.$http.get('test/data.json').then(response => {
        this.user = response.data
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
