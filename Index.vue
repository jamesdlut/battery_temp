<template>
  <div class="dashboard-container">
      <h2 class="ttitle">储能电池温度采集系统</h2>
      <el-row >
        <el-col :span="12"><Child1></Child1></el-col>
        <el-col :span="12"><Child2></Child2></el-col>
      </el-row>
      <el-row>
        <el-col :span="12"><Child3></Child3></el-col>
        <el-col :span="12"><Child4></Child4></el-col>
      </el-row>
  </div>
</template>

<script>
import Child1 from "./Child1.vue"
import Child2 from "./Child2.vue"
import Child3 from "./Child3.vue"
import Child4 from "./Child4.vue"

export default {
    name:"Index",
    components:{
      Child1,Child2,Child3,Child4
    },
  }
</script>

<style>
.ttitle{
  margin-top: -20px;
}
.el-row {
    margin-bottom: 20px;
  }
</style>
