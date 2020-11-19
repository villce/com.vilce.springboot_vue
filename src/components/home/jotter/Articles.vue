<template>
  <div style="height:100%;width:100%">
    <el-row type="flex" justify="center">
      <el-col :span="3" style="margin-top: -18px">
        <el-card class="articles-title" shadow="always">
          <div slot="header" class="clearfix">
            <span>vilce</span>
          </div>
          <div class="el-card__body mid" style="margin-left: -18px">
            <el-row class="text" style="text-align: left; margin-top: -18px" @click.native="articleHome">
              <i class="el-icon-s-home"></i>
              <span>博客首页</span>
            </el-row>
            <el-row class="text" style="text-align: left" @click.native="articleType">
              <i class="el-icon-menu"></i>
              <span>分类</span>
            </el-row>
            <el-row class="text" style="text-align: left" @click.native="articleArchive">
              <i class="el-icon-s-order"></i>
              <span>归档</span>
            </el-row>
            <el-row class="text" style="text-align: left" @click.native="articleLabel">
              <i class="el-icon-s-flag"></i>
              <span>标签</span>
            </el-row>
            <el-row class="text" style="text-align: left; margin-bottom: -18px" @click.native="searchArticle">
              <i class="el-icon-search"></i>
              <span>搜索</span>
            </el-row>
          </div>
        </el-card>
      </el-col>
      <ArticlesIndex></ArticlesIndex>
    </el-row>
  </div>
</template>

<script>
  import ArticlesIndex from "./ArticlesIndex"

  export default {
    name: 'Articles',
    components: {ArticlesIndex},
    data() {
      return {}
    },
    mounted() {
    },
    methods: {
      articleHome() {
        console.info("前往首页")
      },
      articleType() {
        console.info("获取文章分类")
      },
      articleArchive() {
        console.info("文章归档")
      },
      articleLabel() {
        console.info("文章标签")
      },
      searchArticle() {
        console.info("搜索文章")
      }
    }
  }
</script>

<style>
  .text {
    font-size: 14px;
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

  .el-card__header {
    background-color: #1F1F1F;
    font-size: 28px;
    color: #eaeaea;
  }

  .el-row:hover {
    color: #409EFF;
  }
</style>
