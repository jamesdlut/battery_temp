<template>
  <div class="child">

        <div class="grid-content bg-purple-light">
			<el-select v-model="select_value" placeholder="选传感器" class="selection"  @change="el_select()">
			  <el-option
			    v-for="item in select_options"
			    :key="item.value"
			    :label="item.label"
			    :value="item.value">
			  </el-option>
			</el-select>
		
        <div id="pic_4" class="pic"></div>
		
		<p class="time_end">{{time_end}}</p>
		<p class="time_start">{{time_start}}</p>
		<p class="time_mid">{{time_mid}}</p>
		
        </div>

  </div>
</template>



<script>
  import Vue from 'vue'
  import * as echarts from 'echarts';
  import axios from 'axios'
  import VueAxios from "vue-axios";
  Vue.use(VueAxios, axios)
  
  export default {
    name:"Child4",
    data() {
      return {
		  
		time_end:'',
		time_start:'',
		time_mid:'',

        chartDom_4:null,
        myChart_4 :null,
		
		select_options:'',
		select_value: '',

        echart_4_data : {
          title: {
              text: '传感器温度'
          },
          legend: {
              data: ['平均温度']
          },
            xAxis: {
                type: 'category',
				data:['', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '', '']
				},
            yAxis: {
                type: 'value'
            },
            series: [{
               name:'平均温度',
				data:[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
				type: 'line'
            }]
        },//option
      }
    },
    mounted() {
	  this.init_el_option()
      this.echarts_init()
    },
    methods: {
		get_hour_minute_second(value){
			var dateee = new Date(value).toJSON();
			var date = new Date(+new Date(dateee)+8*3600*1000).toISOString().replace(/T/g,' ').replace(/\.[\d]{3}Z/,'');
			return date.split(' ')[1]		
		},
		
		init_el_option(){
			this.axios({
				method:"post",
				url:"api/api/device/list",
				data:{"level":4}
			}).then((res)=>{
				this.device_list  = res.data.data.map((item) =>{
				　　　return item.device_id
				　});
				var device_options = ''
				device_options = this.device_list.map((item) =>{
				　　　return {value:item.toLowerCase(),lable:item.toLowerCase()}
				　});
				this.select_options = device_options
			})			
		},

      echarts_init() {
		   this.chartDom_4 = document.getElementById('pic_4');
		   this.myChart_4 = echarts.init(this.chartDom_4);
		   this.myChart_4.setOption(this.echart_4_data);
      },
	  
	  el_select(){	
			this.change();
			setInterval(this.change,"1000");	
	  }, 
	  
	  change(){
		   var celcius_200 = ''  
		   this.axios({
			   method:"post",
			   url:"api/api/monitor/last200",
			   data:{"device_id":this.select_value}
		   }).then((res)=>{
			 var data_200 = res.data.data
			 celcius_200 = data_200.map((item) =>{
			　　　return item.celcius
			　});
			this.time_end = this.get_hour_minute_second(data_200[0].ts)
			this.time_start = this.get_hour_minute_second(data_200[199].ts)
			this.time_mid = this.get_hour_minute_second(data_200[100].ts)
			celcius_200.reverse()
			this.echart_4_data.series[0].data = celcius_200
			this.myChart_4.setOption(this.echart_4_data);
		   })
	    },

      }

  }
</script>

<style>

.selection{
  margin-left: 50px;
  margin-right: 10px;
  //margin-bottom: -10px;
}
.pic {
  //margin-top: -20px;
  //margin-bottom:-30px;
  width: 100%;
  height: 230px;
}
.time_end{
	margin-top: -60px;
	margin-right: -450px;
	font-size:5px
}
.time_start{
	margin-top: -20px;
	margin-left: -450px;
	font-size:5px
}
.time_mid{
	margin-top: -20px;
	//margin-left: -450px;
	font-size:5px
}
</style>
