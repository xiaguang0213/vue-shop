<template>
<div class="container">
  <div class="login">
      <img src="../../public/timg.jpg">
      <div>
        <el-form :rules="rules" :model="ruleForm" label-width="80px" size="small" ref="loginRef" class="form">
          <el-form-item label="用户名" prop="name">
            <el-input prefix-icon="iconfont el-icon-user" v-model="ruleForm.name"></el-input>
          </el-form-item>
          <el-form-item label="密码" prop="password">
            <el-input prefix-icon="iconfont el-icon-view" v-model="ruleForm.password" type="password"></el-input>
          </el-form-item>
          <el-form-item class="right">
            <el-button type="primary" @click="login">登录</el-button>
            <el-button type="info" @click="resetForm">重置</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
</div>
</template>
<script>
export default {
  data () {
    return {
      ruleForm: {
        name: 'admin',
        password: '123456'
      },
      rules: {
        name: [
          { required: true, message: '请输入用户名称', trigger: 'blur' },
          { min: 5, max: 8, message: '长度在 5 到 8 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 12, message: '长度在 6 到 12 个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    resetForm () {
      this.$refs.loginRef.resetFields()
    },
    login () {
      this.$refs.loginRef.validate(async (valid) => {
        if (valid === false) {
          return false
        } else {
          const { data: res } = await this.$http.post('login', { username: this.ruleForm.name, password: this.ruleForm.password })
          console.log(res)
          if (res.meta.status === 200) {
            // this.$message.success('登陆成功')
            window.sessionStorage.setItem('token', res.data.token)
            this.$router.push('/home')
          } else {
            // this.$message.error('登陆失败')
          }
        }
      })
    }
  }
}
</script>
<style>
  .container{
    height:100%;
    background-color: rgb(27, 76, 122);
    position: relative;
  }
  img{
    width: 100px;
    height: 100px;
    border-radius:50px;
    position: absolute;
    right: 150px;
    top: -50px;
  }
  .login{
    width:400px;
    height: 300px;
    background-color: rgb(243, 245, 247);
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
  }
  .form{
    margin-top: 100px;
    margin-right: 15px;
  }
  .right{
    padding-left: 180px;
  }
  .el-message{
    display: none !important;
  }
</style>
