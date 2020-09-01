<template>
<body id='poster'>
  <el-form class="login-container" label-position="left" abel-width="0px">
    <h3 class="login_title">系统登录</h3>
    <el-form-item>
      用户名:<el-input type="text" auto-complete="off" v-model="loginForm.username" placeholder="请输入用户名"/></el-input>
    </el-form-item>
      <br><br>
      <el-form-item>
      密码： <el-input type="password" auto-complete="off" v-model="loginForm.password" placeholder="请输入密码"/></el-input>
      <br><br>
      </el-form-item>
      <el-button type="primary" style="width: 100%;background: #505458;border: none" v-on:click="login">登录</el-button>
  </el-form>
  </body>
</template>

<script>
  export default {
    name: 'Login',
    data () {
      return {
        loginForm: {
          username: 'admin',
          password: '1234567'
        },
        responseResult: []
      }
    },
    methods: {
      login () {  
        var _this = this 
        console.log(this.$store.state)
        this.$axios
          .post('/login', {
            username: this.loginForm.username,
            password: this.loginForm.password
          })
          .then(successResponse => {
            if (successResponse.data.code === 200) {
              debugger
              _this.$store.commit('login',_this.loginForm)
              var path = this.$route.query.redirect
              this.$router.replace({path: path === '/' || path === undefined ? '/index' : path})
              //this.$router.replace({path: '/index'})
            }
          })
          .catch(failResponse => {
          })
      }
    }
  }
</script>
<style>
  .login-container {
    border-radius: 15px;
    background-clip: padding-box;
    margin: 90px auto;
    width: 350px;
    padding: 35px 35px 15px 35px;
    background: #fff;
    border: 1px solid #eaeaea;
    box-shadow: 0 0 25px #cac6c6;
  }
  
  .login_title {
    margin: 0px auto 40px auto;
    text-align: center;
    color: #505458;
  }

   #poster {
    background:url("../assets/login.jpg") no-repeat;
    background-position: center;
    height: 100%;
    width: 100%;
    background-size: cover;
    position: fixed;
  }
  body{
    margin: 0px;
  }

</style>

