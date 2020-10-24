<template>
  <el-row>
      <el-card class="box-card" shadow="always">
        <div slot="header" class="clearfix" >
          <span>vilce</span>
        </div>
        <div class="el-card__body mid" style="margin-left: -18px">
          <div class="text item" style="text-align: left; margin-top: -18px">
            <i class="el-icon-s-home"></i>
            <span @click="handleHome">首页</span>
          </div>
          <div class="text item" style="text-align: left">
            <i class="el-icon-s-cooperation"></i>
            <span>水印工具</span>
          </div>
          <div class="text item" style="text-align: left">
            <i class="el-icon-user-solid"></i>
            <span>管理中心</span>
          </div>
          <div class="text item" style="text-align: left; margin-bottom: -18px">
            <i class="el-icon-search"></i>
            <span>搜索</span>
          </div>
        </div>
      </el-card>
      <IndexHome></IndexHome>
  </el-row>
</template>

<script>
  import IndexHome from './IndexHome'
  export default {
    name: 'IndexMenu',
    components: {IndexHome}
  }
</script>

<style>
  .text {
    font-size: 14px;
  }

  .item {
    margin-bottom: 10px;
  }

  .clearfix:before,
  .clearfix:after {
    display: table;
    content: "";
  }
  .clearfix:after {
    clear: both
  }

  .box-card {
    width: 200px;
  }

  .el-card__header {
    background-color: #1F1F1F;
    font-size: 28px;
    color: #eaeaea;
  }
</style>
