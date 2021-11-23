<template>
  <div class="login_container">
    <div class="login_box">
      <!-- 头像区域 -->
      <div class="avatat_box">
        <img src="../../assets/logo.png" alt="" />
      </div>
      <!-- 登录表单区域 -->
      <el-form
        ref="loginFormRef"
        label-width="0px"
        class="login_form"
        :model="LoginForm"
        :rules="LoginFormRules"
      >
        <!-- 用户名 -->
        <el-form-item prop="username">
          <el-input
            prefix-icon="el-icon-user"
            v-model="LoginForm.username"
          ></el-input>
        </el-form-item>
        <!-- 密码 -->
        <el-form-item prop="password">
          <el-input
            prefix-icon="el-icon-lock"
            v-model="LoginForm.password"
            type="password"
          ></el-input>
        </el-form-item>
        <!-- 按钮区 -->
        <el-form-item class="btns">
          <el-button type="primary" round @click="login">登录</el-button>
          <el-button type="info" round @click="resetLoginForm">重置</el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  components: {},
  data () {
    return {
      LoginForm: {
        username: 'admin',
        password: '123456'
      },
      LoginFormRules: {
        /* 验证用户名是否合法 */
        username: [
          {
            required: true,
            message: '请输入登录名称',
            trigger: 'blur'
          },
          {
            min: 3,
            max: 6,
            message: '长度需要3-10个字符',
            trigger: 'blur'
          }
        ],
        /* 验证密码是否合法 */
        password: [
          {
            required: true,
            message: '请输入登录密码'
          },
          {
            min: 6,
            max: 15,
            message: '长度需要6-15个字符',
            trigger: 'blur'
          }
        ]
      }
    }
  },
  methods: {
    /* 点击重置按钮，重置登录表单 */
    resetLoginForm () {
      this.$nextTick(() => {
        this.$refs.loginFormRef.resetFields()
      })
      this.$refs.loginFormRef.resetFields()
    },
    /* 点击登录按钮，登录 */
    login () {
      this.$refs.loginFormRef.validate(valid => {
        if (valid) {
          this.$message.success('登录成功')
          window.sessionStorage.setItem('token', 'temp')
          return this.$router.push('/home')
        } if (!valid) {
          return this.$message.error('登录失败')
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
.login_container {
  background-color: #2b4b6b;
  height: 100%;
}
.login_box {
  width: 450px;
  height: 300px;
  background-color: #fff;
  border-radius: 3px;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
.avatat_box {
  height: 130px;
  width: 130px;
  border: 1px solid #eee;
  border-radius: 50%;
  padding: 10px;
  box-shadow: v0 0 10 #ddd;
  position: absolute;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  img {
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background-color: #eee;
  }
}
.btns {
  display: flex;
  justify-content: flex-end;
}
.login_form {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}
</style>
