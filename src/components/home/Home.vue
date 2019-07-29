<template>
  <el-container>
  <el-header>Header
    <h1>我是home页的h1</h1>
  </el-header>
  <el-container>
    <el-aside width="200px">Aside</el-aside>
    <el-main>Main</el-main>
  </el-container>
</el-container>
</template>

<script>
export default {

}
</script>

<style scoped>
.el-container {
  height: 100%
}
.el-header {
  background: #b3c1cd;
}
.el-aside {
  background: #545c64;
}
.el-main {
  background: #eaeef1;
}
h1 {
  color: #000;
}
</style>
