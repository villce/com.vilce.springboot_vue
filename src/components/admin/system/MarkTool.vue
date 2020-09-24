<template>
  <div style="text-align: left">
    <el-form v-model="form" style="text-align: left" ref="dataForm">
      <el-form-item label="水印文字" :label-width="formLabelWidth" prop="word">
        <el-input v-model="form.word" autocomplete="on" placeholder="水印文字"></el-input>
      </el-form-item>
      <el-form-item label="文字大小" :label-width="formLabelWidth" prop="wordSize">
        <el-input v-model="form.wordSize" autocomplete="off" placeholder="文字大小"></el-input>
      </el-form-item>
      <el-form-item label="文字颜色" prop="color">
        <el-input v-model="form.color" autocomplete="off" placeholder="文字颜色：0-白，1-黑，2-灰，3-9为彩虹色"></el-input>
      </el-form-item>
      <el-form-item label="文字旋转角度" :label-width="formLabelWidth" prop="degree">
        <el-input v-model="form.degree" autocomplete="off" placeholder="文字旋转角度，默认为0"></el-input>
      </el-form-item>
    </el-form>
    <el-button class="add-button" type="success" @click="onSubmit">生成透明水印图片</el-button>
  </div>
</template>

<script>
  export default {
    name: 'MarkTool',
    data() {
      return {
        form: {
          word: '',
          wordSize: '',
          color: '',
          degree: ''
        },
        formLabelWidth: '10px'
      }
    },
    methods: {
      onSubmit() {
        this.$axios
          .post('/mark/new', {
            word: this.form.word,
            wordSize: this.form.wordSize,
            color: this.form.color,
            degree: this.form.degree
          }).then(resp => {
          if (resp && resp.data.status === 0) {
            this.$message({
              type: 'info',
              message: resp.data.message
            })
            this.$emit('onSubmit')
          }
        })
      }
    }
  }
</script>

<style scoped>
  .add-button {
    margin: 18px 0 0 10px;
  }
</style>
