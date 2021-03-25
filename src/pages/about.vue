<template>

  <center>
    <img src="logo-gis-changchun-info-vue.png" alt="" style="margin-top: 50px;width: 80px;">
    <h1 style="font-family:华文新魏 ;font-weight:normal ;font-size: 26px;">开源地图脚手架</h1>
    <el-row type="flex" class="row-bg bg-lucency " justify="center">
      <el-col :span="6"><div class="grid-content bg-lucency">
        <h3 style="font-family:黑体 ;font-weight: 100;font-size: 20px;">开源声明</h3>
        <div class="text-center">
          <p>Environment & UI：<a href="https://cn.vuejs.org/">vue</a> + <a href="http://element-cn.eleme.io/#/zh-CN">element</a> + <a href="https://leafletjs.com/">leaflet</a></p>
          <p>Frame：<a href="https://github.com/mengdu/vue-element-admin-tpl">vue-element-admin-tpl</a></p>
          <p>Document：<a href="https://github.com/dong-jianbin/mapboot">MapBoot</a></p>
        </div>
      </div></el-col>


      <el-col :span="8"><div class="grid-content bg-lucency">
        <iframe width='300' height='220' frameborder='0' scrolling='no' marginheight='0' marginwidth='0' src='http://localhost:8088/gis-master-map'></iframe>'
      </div></el-col>

      <el-col :span="6"><div class="grid-content bg-lucency">
        <h3 style="font-family:黑体 ;font-weight: 100;font-size: 20px;">联系我们</h3>
        <div class="text-center">
          <p>GitHub：<a href="https://github.com/dong-jianbin/mapboot">MapBoot</a></p>
          <p>E-mail：<a href="mailto:dongjb@asiainfo.com">dongjb@asiainfo.com</a></p>
          <p>Address：哈尔滨市南岗区民益街78号联通大厦2103室</p>
        </div>
      </div></el-col>

    </el-row>

  </center>
</template>

<script>
    export default {
      name: 'about'
    }
</script>

<style scoped>
  .test{
    height: 40px;
    background: #ccc;
    margin-bottom: 15px;
  }
  .el-col {
    border-radius: 4px;
  }
  .bg-purple-dark {
    background: #99a9bf;
  }
  .bg-purple {
    background: #d3dce6;
  }
  .bg-purple-light {
    background: #e5e9f2;
  }
  .grid-content {
    border-radius: 4px;
    min-height: 36px;
  }
  .row-bg {
    padding: 10px 0;
    background-color: #f9fafc;
  }
  .bg-lucency {
    background: transparent;
  }
</style>
