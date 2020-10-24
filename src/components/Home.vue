<template>
  <div style="height:100%;width:100%" class="home">
    <el-row type="flex" justify="center">
      <el-col :span="15" class="user">
        <div class="block">
          <el-avatar :size="70" :src="circleUrl" @click.native="handleAdmin"></el-avatar>
        </div>
      </el-col>
    </el-row>
    <br>
    <el-row :gutter="10" type="flex" justify="center">
      <el-col :span="4" class="center-card">
        <el-card shadow="always" @click.native="handleJotter">
          <img src="../assets/img/hzw/name/3.jpg" class="image">
          <div style="padding: 10px;">
            <span>博客</span>
          </div>
        </el-card>
      </el-col>
      <el-col :span="4" class="center-card">
        <el-card shadow="always" @click.native="handleTool">
          <img src="../assets/img/hzw/name/4.jpg" class="image">
          <div style="padding: 10px;">
            <span>工具</span>
          </div>
        </el-card>
      </el-col>
      <el-col :span="4" class="center-card">
        <el-card shadow="always">
          <img src="../assets/img/hzw/name/5.jpg" class="image">
          <div style="padding: 10px;">
            <span>待定</span>
          </div>
        </el-card>
      </el-col>
    </el-row>
    <br>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        circleUrl: 'https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png',
      }
    },
    methods: {
      handleJotter() {
        console.info("博客");
        this.$router.replace({path: '/jotter'});
      },
      handleTool() {
        this.$router.replace({path: '/tool'});
      },
      handleAdmin() {
        this.$router.replace({path: '/admin'});
      }
    }
  }
</script>

<style>
  body {
    margin: 0;
    padding: 0;
  }

  .home {
    background: url("../assets/img/hzw/noFace/1.jpg");
    position: fixed;
    width: 100%;
    height: 100%;
    background-size: 100% 100%;
  }

  .image {
    width: 100%;
    display: block;
  }

  .user {
    margin-bottom: 80px;
    margin-top: 80px;
  }

  .center-card {
    font-weight: bold;
    font-size: large;
  }
</style>
