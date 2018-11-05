<template>
    <div class="wrap">
        <el-container class="login_container">
            <el-card>
                <div slot="header" class="el-card-header">
                   <img src="/static/images/login-logo.png" alt="">
                   <h2 class="login-title">后台管理系统</h2>
                </div>
                <el-form :model="formValue" label-width="60px" :rules="rules">
                  <el-form-item 
                    label="账号" 
                    prop="username" 
                  >
                      <el-input v-model="formValue.userName" placeholder="输入用户名" clearable></el-input> 
                  </el-form-item>
                  <el-form-item 
                    label="密码"
                    prop="password"
                  >
                      <el-input v-model="formValue.passWord" placeholder="输入密码" type="password" clearable></el-input>
                  </el-form-item>
                  <el-button type="primary"  @click="login('formValue')">立即登陆</el-button>
                </el-form>
            </el-card>
        </el-container>
    </div>
</template>

<script>
import { isValidUsername } from '@/utils/validator'
export default {
  data() {
    // username 验证
    const validateUsername = (rule, value, callback) => {
      if (!isValidUsername(value)) {
        callback(new Error("请输入正确的用户名"));
      } else {
        callback();
      }
    };
    // pwd 验证
    const validatePwd = (rule, value, callback) => {
      if (value.length < 6) {
        callback(new Error("密码不能小于6位"));
      } else {
        callback();
      }
    };
    return {
      formValue: {
        userName: "",
        passWord: ""
      },
      rules: {
        username: [
          { required: true, message: "请输入账号", trigger: "blur" },
          { required: true, trigger: "blur", validator: validateUsername },
          { required: true, trigger: "change", validator: validateUsername }
        ],
        password: [
          { required: true, message: "请输入密码", trigger: "blur" },
          { required: true, trigger: "blur", validator: validatePwd },
          { required: true, trigger: "change", validator: validatePwd }
        ]
      }
    };
  }
};
</script>

<style lang="stylus" scoped>
.login_container {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: mix(#494166, #424b50) url('../../../static/images/login-bg.jpg') center no-repeat;
    background-size: cover;
    overflow: hidden;

    .el-card {
        position: absolute;
        top: 50%;
        left: 50%;
        margin: -300px 0 0 -200px;
        width: 400px;
        height: 450px;
        background: #fff;

        .el-card-header {
            margin: 0 auto;
            text-align: center;

            &>h2 {
                margin-top: 0;
            }
        }
    }

    .el-button {
        width: 100%;
    }
}
</style>
