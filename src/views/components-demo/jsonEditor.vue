<template>
	<section class="chart-container">
		<el-row>

			<el-col :span="9">
				<div id="chartPie" style="width:100%; height:400px;"></div>
			</el-col>
			<el-col :span="15">
				<div id="chartColumn" style="width:100%; height:400px;"></div>
			</el-col>
			<el-col :span="24">
				<a href="http://echarts.baidu.com/examples.html" target="_blank" style="float: right; ">more>></a>
			</el-col>
		</el-row>
	</section>
</template>

<script>
import JsonEditor from '@/components/JsonEditor'
import echarts from 'echarts'

	export default {
		data() {
			return {
				chartColumn: null,
				chartPie: null
			}
		},

		methods: {
			drawColumnChart() {
				this.chartColumn = echarts.init(document.getElementById('chartColumn'));
				this.chartColumn.setOption({
					/*color: ['#B22222','#FF4500', '#228B22'],*/
					tooltip: {
						trigger: 'axis',
						axisPointer: {
							type: 'shadow'
						}
					},
					title: {
						text: '每日拨打量'
					},
					xAxis: {
						data: ["2019/2/11", "2019/2/12", "2019/2/13", "2019/2/14", "2019/2/15", "2019/2/16", "2019/2/17"]
					},
					yAxis: {},
					series: [{
						name: '每日拨打量',
						type: 'bar',
						barWidth : 40,
						label: {
							normal: {
								show: true,
								position: 'top'
							}
						},
						areaStyle: {
							normal: {}
						},
						itemStyle: {
							normal: {
								color: function(params) {

									var index_color = params.value;

									if(index_color<80) {
										return '#B22222';
									} else if(index_color<89){
										return '#FF4500';
									}else{
										return '#228B22';
									}

								}
							}
						},

						data: [80, 77, 92, 78, 85, 95, 97]
					}]
				});
			},
			drawPieChart() {
				this.chartPie = echarts.init(document.getElementById('chartPie'));
				this.chartPie.setOption({
					title: {
						text: '宋静',
						subtext: '问题分析',
						x: 'center'
					},
					tooltip: {
						trigger: 'item',
						formatter: "{a} <br/>{b} : {c} ({d}%)"
					},
					legend: {
						orient: 'vertical',
						left: 'left',
						data: ['没报工号', '没介绍公司', '没用敬词您', '误导客户', '报价不正规']
					},
					series: [{
						name: '访问来源',
						type: 'pie',
						radius: '55%',
						center: ['50%', '60%'],
						data: [{
								value: 335,
								name: '没报工号'
							},
							{
								value: 310,
								name: '态度冷淡 '
							},
							{
								value: 234,
								name: '不耐烦'
							},
							{
								value: 135,
								name: '误导客户'
							},
							{
								value: 175,
								name: '报价不正规'
							}
						],
						itemStyle: {
							emphasis: {
								shadowBlur: 10,
								shadowOffsetX: 0,
								shadowColor: 'rgba(0, 0, 0, 0.5)'
							}
						}
					}]
				});
			},
			drawCharts() {
				this.drawColumnChart()
				this.drawPieChart()
			},
		},

		mounted: function() {
			this.drawCharts()
		},
		updated: function() {
			this.drawCharts()
		}
	}
</script>

<style scoped>
.editor-container{
  position: relative;
  height: 100%;
}
</style>

