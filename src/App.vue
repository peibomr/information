<template>
  <div id="app">
    <div id="nav">
    </div>
    <router-view/>
  </div>
</template>

<script>
  export default{
    components:{
    }
  }
</script>

<style lang="less">
body,html{
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}
p, h1, h2, h3, h4, h5, h6 {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.el-form-item__label{
  text-align: right !important;
}
</style>
