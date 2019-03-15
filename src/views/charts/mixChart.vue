<template>
	<section class="chart-container">
		<el-row>
			
			<el-col :span="20">
				<div id="chartPie" style="width:100%; height:400px;"></div>
			</el-col>
		</el-row>
	</section>
</template>

<script>
import Chart from '@/components/Charts/mixChart'

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
				
			},
			drawPieChart() {
				this.chartPie = echarts.init(document.getElementById('chartPie'));
				this.chartPie.setOption({
					title: {
						text: '能力分析图'
					},
					tooltip: {},
					legend: {
						orient: 'vertical',
						left: 'right',
						data: ['个人能力（Personal Ability）', '班级能力（Class Ability）']
						
					},
					radar: {
						// shape: 'circle',
						name: {
							textStyle: {
								color: '#fff',
								backgroundColor: '#999',
								borderRadius: 3,
								padding: [3, 5]
							}
						},
						indicator: [{
								name: '分析能力（analytical Ability）',
								max: 100
							},
							{
								name: '沟通能力（communication skills）',
								max: 100
							},
							{
								name: '适应能力（Adapt Ability）',
								max: 100
							},
							{
								name: '洞察能力（insight）',
								max: 100
							},
							{
								name: '专业能力（Competence）',
								max: 100
							},
							{
								name: '学习能力（Learning Ability）',
								max: 100
							}
						]
					},
					series: [{
						name: '个人 vs 班级（Personal vs Class）',
						type: 'radar',
						// areaStyle: {normal: {}},
						data: [{
								value: [89, 78, 98, 84, 90, 75],
								name: '个人能力（Personal Ability）',
								label: {
								normal: {
									show: true,
									position: 'top'
								}
							}
							},
							{
								value: [80, 86, 78, 87, 69, 95],
								name: '班级能力（Class Ability）',
								label: {
								normal: {
									show: true,
									position: 'bottom'
								}
							}
							}
						]
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
/*.chart-container{
  position: relative;
  width: 100%;
  height: calc(100vh - 84px);
}*/
.chart-container {
		width: 100%;
		float: left;
	}
	/*.chart div {
        height: 400px;
        float: left;
    }*/
	
	.el-col {
		padding: 30px 20px;
	}
</style>

