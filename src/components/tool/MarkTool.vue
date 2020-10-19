<template>
  <el-tabs>
    <el-tab-pane label="透明水印图片" name="first">
      <el-row :gutter="20">
        <el-col :span="6">
          <div style="text-align: left">
            <el-form v-model="form" style="text-align: left" ref="dataForm">
              <el-form-item label="水印数量" :label-width="formLabelWidth" prop="markNum">
                <el-cascader
                  v-model="form.markNum"
                  :options="numOptions"
                  @change="handleMarkNumChange" placeholder="请选择水印数量"></el-cascader>
              </el-form-item>
              <el-form-item label="水印文字" :label-width="formLabelWidth" prop="word">
                <el-input
                  type="textarea"
                  :rows="2"
                  maxlength="20"
                  show-word-limit
                  placeholder="请输入水印文字"
                  v-model="form.word">
                </el-input>
              </el-form-item>
              <el-form-item label="文字大小" :label-width="formLabelWidth" prop="wordSize">
                <el-select v-model="form.wordSize" placeholder="请选择文字大小">
                  <el-option
                    v-for="item in wordSizeOptions"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
              </el-form-item>
              <el-form-item label="文字颜色" :label-width="formLabelWidth" prop="color">
                <el-color-picker v-model="form.color" :predefine="predefineColors"></el-color-picker>
              </el-form-item>
              <el-form-item label="文字旋转角度" :label-width="formLabelWidth" prop="degree">
                <el-select v-model="form.degree" placeholder="请选择旋转角度">
                  <el-option
                    v-for="item in degreeOptions"
                    :key="item.value"
                    :label="item.label"
                    :value="item.value">
                  </el-option>
                </el-select>
              </el-form-item>
            </el-form>
            <el-button class="add-button" type="success" @click="markNew">生成透明水印图片</el-button>
          </div>
        </el-col>
        <el-col :span="6">
          <div style="text-align: left">
            <span class="demonstration">水印图片</span>
            <el-image :src="src" style="width: 400px; height: 200px" :preview-src-list="srcList"></el-image>
          </div>
        </el-col>
      </el-row>
    </el-tab-pane>
    <el-tab-pane label="图片添加文字水印" name="second">
      图片添加文字水印
    </el-tab-pane>
  </el-tabs>
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
          wordSize: '',
          color: '#000000',
          degree: '',
          markNum: {
            single: true,
            position: 3
          }
        },
        numOptions: [{
          value: true,
          label: '单个',
          children: [{
            value: 0,
            label: '左上'
          }, {
            value: 1,
            label: '右上'
          }, {
            value: 2,
            label: '左下'
          }, {
            value: 3,
            label: '右下'
          }, {
            value: 4,
            label: '中间'
          }]
        }, {
          value: false,
          label: '铺满'
        }],
        degreeOptions: [{
          value: 0,
          label: '0°',
        }, {
          value: 1,
          label: '45°'
        },{
          value: 2,
          label: '-45°'
        },{
          value: 3,
          label: '90°'
        },{
          value: 4,
          label: '-90°'
        }],
        wordSizeOptions: [{
          value: 50,
          label: '小号',
        }, {
          value: 75,
          label: '中号'
        },{
          value: 100,
          label: '大号'
        }],
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
      handleMarkNumChange(value) {
        this.form.markNum.single = value[0]
        this.form.markNum.position = value[1]
        console.info(this.form.markNum)
      },
      markNew() {
        this.$axios
          .post('/mark/new', {
            word: this.form.word,
            wordSize: this.form.wordSize,
            color: this.form.color,
            degree: this.form.degree,
            single: this.form.markNum.single,
            position: this.form.markNum.position
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
  .add-button {
    margin: 18px 0 0 10px;
  }
</style>
