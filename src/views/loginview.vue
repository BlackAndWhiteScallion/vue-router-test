<template>
    <div id="app">
      <div id="admin">
        <div class="pos" v-loading="loading">
          <h1 class="adminh1">用户登录</h1>
          <el-form
            :model="ruleForm"
            status-icon
            :rules="rules"
            ref="ruleForm"
            label-width="100px"
            class="demo-ruleForm"
          >
            <el-form-item label="用户名：" prop="pass">
              <el-input
                prefix-icon="el-icon-user"
                style="width: 250px"
                type="text"
                v-model="ruleForm.pass"
                autocomplete="off"
              ></el-input>
            </el-form-item>
            <el-form-item label="密 码：" prop="checkPass">
              <el-input
                prefix-icon="el-icon-menu"
                style="width: 250px"
                show-password
                type="password"
                v-model="ruleForm.checkPass"
                autocomplete="off"
              ></el-input>
            </el-form-item>
            <el-form-item>
              <el-button type="primary" @click="submitForm('ruleForm')"
                >提交</el-button
              >
            </el-form-item>
          </el-form>
        </div>
      </div>
    </div>
  </template>
   
  <script>
  export default {
    name: "app",
    data() {
      var validatePass = (rule, value, callback) => {
        if (value === "") {
          callback(new Error("请输入用户信息"));
        } else {
          if (this.ruleForm.checkPass !== "") {
            this.$refs.ruleForm.validateField("checkPass");
          }
          callback();
        }
      };
      var validatePass2 = (rule, value, callback) => {
        if (value === "") {
          callback(new Error("请输入密码"));
        } else if (value.length < 8 || value.length > 13) {
          callback(new Error("长度必须在8-12之内!"));
        } else {
          callback();
        }
      };
      return {
        loading: false,
        ruleForm: {
          pass: "",
          checkPass: "",
        },
        rules: {
          pass: [{ validator: validatePass, trigger: "blur" }],
          checkPass: [{ validator: validatePass2, trigger: "blur" }],
        },
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            this.loading = true;
            setTimeout(() => {
              this.loading = false;
            }, 2000);
          } else {
            console.log("error submit!!");
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      },
    },
  };
  </script>
   
  <style scoped>
  * {
    padding: 0;
    margin: 0;
  }
  body {
    background-color: rgb(135, 206, 235);
  }
  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
  }
  #admin {
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -200px;
    margin-left: -250px;
    width: 500px;
    height: 400px;
    background: #fff;
    border-radius: 10%;
    box-shadow: 8px 10px 10px rgb(177, 223, 242);
  }
  .adminh1 {
    margin: 20px 0;
    text-shadow: 10px 13px 3px rgb(207, 207, 207);
    text-align: center;
  }
  .pos {
    width: 450px;
    height: 350px;
    position: absolute;
    top: 25px;
    left: 25px;
  }
  </style>