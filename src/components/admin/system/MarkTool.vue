<template>
  <el-container>
    <el-container>
      <el-aside width="200px">透明水印图片</el-aside>
      <el-main>
        <div style="text-align: left">
          <el-form v-model="form" style="text-align: left" ref="dataForm">
            <el-form-item label="水印文字" :label-width="formLabelWidth" prop="word">
              <el-input v-model="form.word" autocomplete="on" placeholder="水印文字"></el-input>
            </el-form-item>
            <el-form-item label="文字大小" :label-width="formLabelWidth" prop="wordSize">
              <el-input v-model="form.wordSize" autocomplete="off" placeholder="文字大小"></el-input>
            </el-form-item>
            <el-form-item label="文字颜色" :label-width="formLabelWidth" prop="color">
              <el-color-picker v-model="form.color" :predefine="predefineColors"></el-color-picker>
            </el-form-item>
            <el-form-item label="文字旋转角度" :label-width="formLabelWidth" prop="degree">
              <el-input v-model="form.degree" autocomplete="off" placeholder="文字旋转角度，默认为0"></el-input>
            </el-form-item>
          </el-form>
          <el-button class="add-button" type="success" @click="onSubmit">生成透明水印图片</el-button>
        </div>
      </el-main>
      <el-main>
        <div style="text-align: center">
          <span class="demonstration" >水印图片</span>
          <el-image :src="src" style="width: 200px; height: 100px" :preview-src-list="srcList" ></el-image>
        </div>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>
  export default {
    name: 'EditForm',
    data() {
      return {
        src: 'http://120.55.169.142:8006/image/file/0.png',
        srcList: ['http://120.55.169.142:8006/image/file/0.png'],
        form: {
          word: '',
          wordSize: '50',
          color: '#000000',
          degree: '-45'
        },
        predefineColors: [
          '#ff4500',
          '#ff8c00',
          '#ffd700',
          '#90ee90',
          '#00ced1',
          '#1e90ff',
          '#c71585',
          '#000000',
          '#999',
          '#FFFFFF'
        ],
        formLabelWidth: '120px'
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
            this.src = resp.data.data
            this.srcList = [resp.data.data]
            this.$emit('onSubmit')
          }
        })
      }
    }
  }
</script>

<style scoped>
  .el-header {
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
  }

  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    text-align: center;
    line-height: 200px;
  }

  .el-main {
    background-color: #E9EEF3;
    color: #333;
    text-align: center;
    line-height: 160px;
  }

  body > .el-container {
    margin-bottom: 40px;
  }

  .el-container:nth-child(5) .el-aside,
  .el-container:nth-child(6) .el-aside {
    line-height: 260px;
  }

  .el-container:nth-child(7) .el-aside {
    line-height: 320px;
  }
  .add-button {
    margin: 18px 0 0 10px;
  }
</style>
