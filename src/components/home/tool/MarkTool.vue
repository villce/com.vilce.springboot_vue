<template>
  <el-container>
    <el-header
      style="height: 80px;background-color: #6a737d">
      <a href="/index">
        <el-avatar :size="70" :src="userIcon" width="55px" style="float: left;margin-top: 5px"></el-avatar>
      </a>
      <div style="font-size: 30px;margin-top: 15px;color: #d9ecff">水印工具</div>
    </el-header>
    <el-tabs el-tabs type="border-card">
      <el-tab-pane v-show="true">
        <span slot="label"><i class="el-icon-edit-outline"></i> 透明水印图片</span>
        <NewWaterMark></NewWaterMark>
      </el-tab-pane>
      <el-tab-pane>
        <span slot="label"><i class="el-icon-picture-outline"></i> 图片添加文字水印</span>
        <ImgWaterMark></ImgWaterMark>
      </el-tab-pane>
      <el-tab-pane>
        <span slot="label"><i class="el-icon-picture"></i> 图片添加图片水印</span>
        <ImgMarkImg></ImgMarkImg>
      </el-tab-pane>
    </el-tabs>
  </el-container>
</template>

<script>
  import NewWaterMark from './NewWaterMark'
  import ImgWaterMark from './ImgWaterMark'
  import ImgMarkImg from './ImgMarkImg'
  export default {
    name: 'EditForm',
    components: {NewWaterMark, ImgWaterMark, ImgMarkImg},
    data() {
      return{
        userIcon: 'https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png',
      }
    },
    mounted() {
      this.currentUser();
    },
    methods: {
      currentUser() {
        var _this = this;
        this.$axios.get('/login/currentUser').then(resp => {
          if (resp && resp.data.status === 0) {
            _this.userIcon = resp.data.data.icon;
            _this.username = resp.data.data.username;
          }
        })
      },
    }
  }
</script>
