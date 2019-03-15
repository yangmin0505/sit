<template>
	<section class="chart-container">
		<el-row>
			<el-col :span="18">
				<div id="chartColumn" style="width:100%; height:400px;"></div>
			</el-col>

		</el-row>
		<el-row>
			<el-col :span="14">
				<div id="chartPie" style="width:100%; height:400px;"></div>
			</el-col>
		</el-row>
	</section>
</template>

<script>
import Dropzone from '@/components/Dropzone'
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
					title: {
						text: '个人与班级平均成绩',
						subtext: ''
					},
					tooltip: {
						trigger: 'axis',
						axisPointer: {
							type: 'cross',
							label: {
								backgroundColor: '#283b56'
							}
						}
					},
					legend: {
						data: ['班级平均成绩', '个人成绩']
					},
					toolbox: {
						show: true,
						feature: {
							dataView: {
								readOnly: false
							},
							restore: {},
							saveAsImage: {}
						}
					},
					dataZoom: {
						show: false,
						start: 0,
						end: 100
					},
					xAxis: [{
							type: 'category',
							boundaryGap: true,
							data: (function() {
								var now = new Date();
								var res = [];
								var len = 10;
								while(len--) {
									res.unshift(now.toLocaleTimeString().replace(/^\D*/, ''));
									now = new Date(now - 2000);
								}
								return res;
							})()
						},
						{
							type: 'category',
							boundaryGap: true,
							data: (function() {
								var res = [];
								var len = 10;
								while(len--) {
									res.push(10 - len - 1);
								}
								return res;
							})()
						}
					],
					yAxis: [{
							type: 'value',
							scale: false,
							name: '预购量',
							max: 100,
							min: 0,
							boundaryGap: [0.2, 0.2]
						},
						{
							type: 'value',
							scale: true,
							name: '价格',
							max: 100,
							min: 0,
							boundaryGap: [0.2, 0.2]
						}
					],
					series: [{
							name: '个人成绩',
							type: 'bar',
							barWidth: 40,
							label: {
								normal: {
									show: true,
									position: 'top'
								}
							},
							xAxisIndex: 1,
							yAxisIndex: 1,
							/*data: (function() {
								var res = [];
								var len = 10;
								while(len--) {
									res.push(Math.round(Math.random() * 1000));
								}
								return res;
							})()*/
							data: [80, 77, 92, 78, 85, 95, 97, 86, 69, 98]
						},
						{
							name: '班级平均成绩',
							type: 'line',
							label: {
								normal: {
									show: true,
									position: 'bottom'
								}
							},

							/*data: (function() {
								var res = [];
								var len = 0;
								while(len < 10) {
									res.push((Math.random() * 10 + 5).toFixed(1) - 0);
									len++;
								}
								return res;
							})()*/

							data: [78, 89, 90, 68, 85, 89, 80, 76, 85, 73, 78]
						}
					]
				});
				/*app.count = 11;
				setInterval(function() {
					axisData = (new Date()).toLocaleTimeString().replace(/^\D, '');

					var data0 = option.series[0].data;
					var data1 = option.series[1].data;
					data0.shift();
					data0.push(Math.round(Math.random() * 1000));
					data1.shift();
					data1.push((Math.random() * 10 + 5).toFixed(1) - 0);

					option.xAxis[0].data.shift();
					option.xAxis[0].data.push(axisData);
					option.xAxis[1].data.shift();
					option.xAxis[1].data.push(app.count++);

					myChart.setOption(option);
				}, 2100);*/
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

