<template>
  <div class="child">
        <div >
			<el-select v-model="select_value" placeholder="选集装箱" class="selection"  @change="el_select()">
			  <el-option
			    v-for="item in select_options"
			    :key="item.value"
			    :label="item.label"
			    :value="item.value">
			  </el-option>
			</el-select>

        <div id="pic_1" class="pic"></div>
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
    name:"Child1",
    data() {
      return {
		device_id:'',
		
		avg_200:'',
		max_200:'',
		min_200:'',
		
		time_end:'',
		time_start:'',
		time_mid:'',
		
        chartDom:null,
        myChart :null,
		
	    select_options:'',
		select_value: '',

        echart_data : {
          title: {
              text: '集装箱温度'
          },
          legend: {
              ddata: ['平均温度','最高温度','最低温度']
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
            },
			{
			   name:'最高温度',
				data:[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
			    type: 'line'
			},
			{
			   name:'最低温度',
				data:[0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0],
			    type: 'line'
			},	
			]
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
			    data:{"level":1}
			}).then((res)=>{
				this.device_list  = res.data.data.map((item) =>{
				　　　return item.device_id
				　});
				
				var device_options = ''
				device_options = this.device_list.map((item) =>{
				　　　return {value:item,lable:item}
				　});
				this.select_options = device_options
			})		
		},

		echarts_init() {
		   this.chartDom = document.getElementById('pic_1');
		   this.myChart = echarts.init(this.chartDom);
		   this.myChart.setOption(this.echart_data);
		  },

		el_select(){
			this.change();
			setInterval(this.change,"10000");	
		},
		  
		change(){	  
		 var celcius_200 = ''
		 var time_200 = ''
		 
		 this.axios({
		     method:"post",
		     url:"api/api/monitor/last200",
			 data:{"device_id":this.select_value}
		 }).then((res)=>{
		 	 var data_200 = res.data.data
		 	this.avg_200 = data_200.map((item) =>{
		 	　　　return item.avg
		 	　});
			this.max_200 = data_200.map((item) =>{
			　　　return item.max
			　});
			this.min_200 = data_200.map((item) =>{
			　　　return item.min
			　});
			this.time_end = this.get_hour_minute_second(data_200[0].ts)
			this.time_start = this.get_hour_minute_second(data_200[199].ts)
			this.time_mid = this.get_hour_minute_second(data_200[100].ts)
			
			this.avg_200.reverse()
			this.max_200.reverse()
			this.min_200.reverse()

		 	this.echart_data.series[0].data = this.avg_200
			this.echart_data.series[1].data = this.max_200
			this.echart_data.series[2].data = this.min_200
			
		 	this.myChart.setOption(this.echart_data);
		 })

		  },
		  

      }

  }
</script>

<style>
</style>
