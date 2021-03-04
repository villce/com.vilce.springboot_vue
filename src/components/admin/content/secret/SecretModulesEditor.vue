<template>
  <el-dialog
    title="修改用户信息"
    :visible.sync="dialogFormVisible">
    <el-form v-model="modules" style="text-align: left" ref="dataForm">
      <el-form-item label="模块标题" label-width="120px" prop="modulesTitle">
        <el-input v-model="modules.modulesTitle" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="模块日期" label-width="120px" prop="password">
        <el-button type="warning" @click="resetPassword(modules.username)">重置密码</el-button>
      </el-form-item>
      <el-form-item label="模块图片" label-width="120px" prop="name">
        <el-input v-model="modules.imgUrlList" autocomplete="off"></el-input>
        <img-upload @onUpload="uploadImg" ref="imgUpload"></img-upload>
      </el-form-item>
    </el-form>
    <div slot="footer" class="dialog-footer">
      <el-button @click="dialogFormVisible = false">取 消</el-button>
      <el-button type="primary" @click="onSubmit(modules)">确 定</el-button>
    </div>
  </el-dialog>
</template>

<script>
  export default {
    name: "SecretModulesEditor",
    data() {
      return {
        modules: {}
      }
    },
    mounted() {
    },
    methods: {
      onSubmit(modules) {
        this.$axios.post("/secret/editModules", {
          id: modules.id,
          modulesDate: modules.modulesDate,
          modulesTitle: modules.modulesTitle,
          imgUrlList: modules.imgUrlList
        }).then(resp => {
          if (resp && resp.data.status === 0) {
            this.$message({
              type: 'info',
              message: resp.data.message
            })
          }
        })
      }
    }
  }
</script>

<style scoped>
</style>
