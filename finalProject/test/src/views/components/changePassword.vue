<template>
  <div>

    <el-dialog title="修改密码" :visible.sync="outerVisible" style="width:1000px; margin:0 auto">
      <el-form
        :rules="rules"
        :model="pwdList"
        style="width:400px;"
        status-icon
        ref="pwdList"
      >

        <el-form-item prop="oldPwd"  label="原密码" label-width='120px'  >
          <el-input v-model="pwdList.oldPwd"  placeholder="请输入原密码" show-password />
        </el-form-item>

        <el-form-item  prop="newPwd" label="新密码" label-width='120px' >
          <el-input v-model="pwdList.newPwd"  placeholder="新密码" show-password />
        </el-form-item>

        <el-form-item prop="newPwd2"  label="确认密码" label-width='120px' >
          <el-input v-model="pwdList.newPwd2"  placeholder="确认密码" show-password />
        </el-form-item>

      </el-form>

      <el-dialog
        width="30%"
        title="修改成功"
        :visible.sync="rebuldDialogVisible"
        append-to-body>

        <span>恭喜您，密码修改成功，下次登录生效！</span>
        <span slot="footer" class="dialog-footer">
      <el-button type="primary" @click="rebuldDialogVisible = false; outerVisible = false">确定</el-button>
    </span>
      </el-dialog>
      <div slot="footer" class="dialog-footer">
        <el-button @click="resetForm('pwdList')">重 置</el-button>
        <el-button type="primary" @click="innerVisible('pwdList')">确定修改</el-button>
      </div>
    </el-dialog>

  </div>
</template>

<script>
  const pwdListDefault = {
    oldPwd: null,
    newPwd: null,
    newPwd2: null
  }
  export default {
    name: 'changePassword',
    methods:{
      resetForm(pwdList) {
        if (this.$refs[pwdList]!==undefined) {
          this.$refs[pwdList].resetFields();
        }
      },
      innerVisible(){
        this.rebuldDialogVisible=true
      },
    },
    data() {
      var checkPwd = (rule, value, callback) => {
        if (value !== this.pwdList.newPwd) {
          callback(new Error('密码不一致'))
        } else {
          callback()
        }
      }
      return {
        rebuldDialogVisible: false,
        pwdList: Object.assign({}, pwdListDefault),
        rules: {
          oldPwd: [
            { required: true, message: '请输入旧密码', trigger: 'blur' }
          ],
          newPwd: [
            { required: true, message: '请输入新密码', trigger: 'blur' },
            { min: 8, message: '请至少输入8个字符', trigger: 'blur' }
          ],
          newPwd2: [
            { required: true, message: '请再次输入新密码', trigger: 'blur' },
            { validator: checkPwd, trigger: 'blur' }
          ]
        },
        outerVisible: false,
      };
    }
  }
</script>
