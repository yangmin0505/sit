<template>
	<section class="chart-container">
		<el-row>

			<el-col :span="20">
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
import splitPane from 'vue-splitpane'

import echarts from 'echarts'

	export default {
		data() {
			return {
				chartColumn: null,
				chartPie: null,
				sysUserAvatar: ''
			}
		},

		methods: {
			drawColumnChart() {
				this.chartColumn = echarts.init(document.getElementById('chartColumn'));
				this.chartColumn.setOption({
					title: {
						text: '基础雷达图'
					},
					tooltip: {},
					legend: {
						data: ['预算分配（Allocated Budget）', '实际开销（Actual Spending）']
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
								name: '销售（sales）',
								max: 6500
							},
							{
								name: '管理（Administration）',
								max: 16000
							},
							{
								name: '信息技术（Information Techology）',
								max: 30000
							},
							{
								name: '客服（Customer Support）',
								max: 38000
							},
							{
								name: '研发（Development）',
								max: 52000
							},
							{
								name: '市场（Marketing）',
								max: 25000
							}
						]
					},
					series: [{
						name: '预算 vs 开销（Budget vs spending）',
						type: 'radar',
						// areaStyle: {normal: {}},
						data: [{
								value: [4300, 10000, 28000, 35000, 50000, 19000],
								name: '预算分配（Allocated Budget）'
							},
							{
								value: [5000, 14000, 28000, 31000, 42000, 21000],
								name: '实际开销（Actual Spending）'
							}
						]
					}]
				});
			},
			drawPieChart() {
				this.chartPie = echarts.init(document.getElementById('chartPie'));
				this.chartPie.setOption({
					 tooltip: {
        trigger: 'item',
        formatter: "{a} <br/>{b}: {c} ({d}%)"
    },
    legend: {
        orient: 'vertical',
        x: 'left',
        data:['没报工号','没介绍公司','没用敬词您','误导客户','报价不正规','未赞美/认同客户','游说过程中使用禁用语','未说最后结束语']
    },
    series: [
        {
            name:'访问来源',
            type:'pie',
            selectedMode: 'single',
            radius: [0, '30%'],

            label: {
                normal: {
                    position: 'inner'
                }
            },
            labelLine: {
                normal: {
                    show: false
                }
            },
            data:[
                {value:1548, name:'班级排名15'}
            ]
        },
        {
            name:'扣分原因',
            type:'pie',
            radius: ['40%', '55%'],
            label: {
                normal: {
                    formatter: '{a|{a}}{abg|}\n{hr|}\n  {b|{b}：}{c}  {per|{d}%}  ',
                    backgroundColor: '#eee',
                    borderColor: '#aaa',
                    borderWidth: 1,
                    borderRadius: 4,
                    // shadowBlur:3,
                    // shadowOffsetX: 2,
                    // shadowOffsetY: 2,
                    // shadowColor: '#999',
                    // padding: [0, 7],
                    rich: {
                        a: {
                            color: '#999',
                            lineHeight: 22,
                            align: 'center'
                        },
                        // abg: {
                        //     backgroundColor: '#333',
                        //     width: '100%',
                        //     align: 'right',
                        //     height: 22,
                        //     borderRadius: [4, 4, 0, 0]
                        // },
                        hr: {
                            borderColor: '#aaa',
                            width: '100%',
                            borderWidth: 0.5,
                            height: 0
                        },
                        b: {
                            fontSize: 16,
                            lineHeight: 33
                        },
                        per: {
                            color: '#eee',
                            backgroundColor: '#334455',
                            padding: [2, 4],
                            borderRadius: 2
                        }
                    }
                }
            },
            data:[
                {value:2, name:'没报工号'},
                {value:6, name:'没介绍公司'},
                {value:2, name:'没用敬词您'},
                {value:4, name:'误导客户'},
                {value:3, name:'报价不正规'},
                {value:1, name:'未赞美/认同客户'},
                {value:5, name:'游说过程中使用禁用语'},
                {value:1, name:'未说最后结束语'}
            ]
        }
    ]
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

<style  scoped>
  .components-container {
    position: relative;
    height: 100vh;
  }

  .left-container {
    background-color: #F38181;
    height: 100%;
  }

  .right-container {
    background-color: #FCE38A;
    height: 200px;
  }

  .top-container {
    background-color: #FCE38A;
    width: 100%;
    height: 100%;
  }

  .bottom-container {
    width: 100%;
    background-color: #95E1D3;
    height: 100%;
  }
</style>
