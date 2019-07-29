<template>
<!--
  el-form 表单组件
  el-form-item 表单元素
  model : 表单数据对象
  rules : 校验规则
  ref : 获取组件
  label : 标题
  prop : 校验用的
 -->
 <el-row type='flex' justify="center" align="middle">
    <el-col :span='8'>
      <el-form
        :model="loginForm"
        :rules="rules"
        ref="loginForm"
        >
        <el-form-item
          label="用户名"
          prop="username">
          <el-input v-model="loginForm.username"></el-input>
        </el-form-item>

        <el-form-item
          label="密码"
          prop="password">
          <el-input v-model="loginForm.password"></el-input>
          </el-form-item>
            <!-- 登录部分 -->
          <el-form-item>
          <el-button type="success" @click='startLogin'>登录</el-button>
          <el-button @click='resetForm'>重置</el-button>
        </el-form-item>
      <h1>我是login页的h1</h1>
      </el-form>
    </el-col>
 </el-row>

</template>

<script>
// eslint-disable

import axios from 'axios'
export default {
  data () {
    return {
      loginForm: {
        username: 'admin',
        password: '123456'
      },
      rules: {
        username: [
          // required: true 表示必填 给个*，false则没有*
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输密码', trigger: 'blur' },
          { min: 5, max: 10, message: '长度在 5 到 10 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  //  开始登录
  methods: {
    startLogin () {
      // 校验
      this.$refs.loginForm.validate((valid) => {
        if (!valid) {
          //  return console.log('校验失败');
          this.$message({
            message: '校验失败',
            type: 'error',
            duration: 1000
          })
          return
        }
        //  console.log('校验成功,开始去登录了')
        // this.$message({
        //     message : '校验成功,开始去登录了',
        //     type:'success',
        //     duration:1000
        //   })
        // axios.post(url,data,config)
        axios.post('http://localhost:8888/api/private/v1/login', this.loginForm).then(res => {
          console.log(res)
          if (res.data.meta.status === 200) {
            this.$message({
              message: '登录成功',
              type: 'success',
              duration: 1000
            })
            // 跳转到home页,编程式导航
            this.$router.push('/home')
          } else {
            this.$message({
              message: '登录失败',
              type: 'error',
              duration: 1000
            })
          }
        })
      })
    },
    // 重置  数据恢复到初始值
    resetForm () {
      this.$refs.loginForm.resetFields()
    }
  }
}
</script>

<style scoped>

  /* 行 */
  .el-row {
    height:100%;
    background:#2d434c
  }

  .el-form {
    background: #fff;
    border-radius:15px;
    padding: 20px 30px;
  }
  h1 {
    color:red;
  }
</style>
