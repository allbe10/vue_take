<template>
  <div>
    <img class="bg" src="@/assets/img/bg.jpg">
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" class="login-form">
      <h1 class="h1">外卖系统注册</h1>
                                                      <el-form-item v-if="tableName=='defaultuser'" label="用户名" prop="defaultuserusername">
        <el-input v-model="ruleForm.username" placeholder="用户名"></el-input>
      </el-form-item>
                        <el-form-item v-if="tableName=='defaultuser'" label="密码" prop="defaultusermima">
        <el-input v-model="ruleForm.mima" placeholder="密码"></el-input>
      </el-form-item>
                        <el-form-item v-if="tableName=='defaultuser'" label="姓名" prop="defaultusername">
        <el-input v-model="ruleForm.name" placeholder="姓名"></el-input>
      </el-form-item>
                                          <el-form-item v-if="tableName=='defaultuser'" label="年龄" prop="defaultuserage">
        <el-input v-model="ruleForm.age" placeholder="年龄"></el-input>
      </el-form-item>
                        <el-form-item v-if="tableName=='defaultuser'" label="电话" prop="defaultuserphone">
        <el-input v-model="ruleForm.phone" placeholder="电话"></el-input>
      </el-form-item>
                                          <el-form-item v-if="tableName=='defaultuser'" label="邮箱" prop="defaultuseremail">
        <el-input v-model="ruleForm.email" placeholder="邮箱"></el-input>
      </el-form-item>
                        <el-form-item v-if="tableName=='defaultuser'" label="余额" prop="defaultusermoney">
        <el-input v-model="ruleForm.money" placeholder="余额"></el-input>
      </el-form-item>
                                                                                                                  <el-button @click="login()" class="btn-login" type="primary">注册</el-button>
    </el-form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      ruleForm: {
              },
      tableName:"",
      rules: {}
    };
  },
  mounted(){
    let table = this.$storage.get("loginTable");
    this.tableName = table;
  },
  methods: {
    // 获取uuid
    getUUID () {
      return new Date().getTime();
    },
    // 注册
    login() {
                                                      if((!this.ruleForm.username) && `defaultuser` == this.tableName){
        this.$message.error(`用户名不能为空`);
        return
      }
                                                            if((!this.ruleForm.mima) && `defaultuser` == this.tableName){
        this.$message.error(`密码不能为空`);
        return
      }
                                                                                                                                                                  if(`defaultuser` == this.tableName && this.ruleForm.age&&(!this.$validate.isIntNumer(this.ruleForm.age))){
        this.$message.error(`年龄应输入整数`);
        return
      }
                                                                                                                                                                                                                  if(`defaultuser` == this.tableName && this.ruleForm.money&&(!this.$validate.isNumber(this.ruleForm.money))){
        this.$message.error(`余额应输入数字`);
        return
      }
                                                                                                                                          this.$refs["ruleForm"].validate(valid => {
        if (valid) {
          this.$http({
            url: `${this.tableName}/register`,
            method: "post",
            data:this.ruleForm
          }).then(({ data }) => {
            if (data && data.code === 0) {
              this.$router.replace({ path: "/login" });
            } else {
              this.$message.error(data.msg);
            }
          });
        }
      });
    }
  }
};
</script>
<style lang="scss" scoped>
</style>
