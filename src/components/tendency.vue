<template>
    <div class="line1">
        <div id="line1" class="" style="width: 90%;height:450px;"></div>
    </div>
</template>

<script>
    import echarts from 'echarts/lib/echarts';
    // 引入柱状图
    import 'echarts/lib/chart/bar';
    import 'echarts/lib/chart/line';
    import 'echarts/lib/component/title';
    import 'echarts/lib/component/legend';
    import 'echarts/lib/component/toolbox';
    import 'echarts/lib/component/markPoint';
    import 'echarts/lib/component/tooltip';
    export default {
        mounted(){
            this.myChart = echarts.init(document.getElementById('line1'));
            this.initData();
        },
        props: ['sevenDate', 'sevenDay'],
        methods: {
            initData(){
                const colors = ['#9ccbee', '#50cbee', '#20A0FF'];
                const option = {
                    color: colors,
                    title: {
                        text: '走势图',
                        subtext: '数据实时更新'
                    },
                    tooltip: {
                        trigger: 'axis',
                        axisPointer: {
                            type: 'cross'
                        }, 
                    },
                    legend: {
                        data:['新注册用户', '新增订单', '新增管理员']
                    },
                    toolbox: {
                        itemGap: 16,
                        show: true,
                        feature: {
                            // dataZoom: {
                            //     yAxisIndex: 'false'
                            // },
                            dataView: {readOnly: false},
                            magicType: {type: ['line', 'bar', 'stack', 'tiled']},
                            restore: {},
                        }
                    },
                    xAxis:  {
                        type: 'category',
                        boundaryGap: false,
                        data: this.sevenDay
                    },
                    yAxis: [
                        {
                          type: 'value',
                          name: '用户',
                          min: 0,
                          max: 200,
                        //   position: 'left',
                          axisLine: {
                              lineStyle: {
                                  color: '#999'
                              }
                          },
                          axisLabel: {
                              formatter: '{value}个'
                          }
                        },
                        {
                          type: 'value',
                          name: '订单',
                          min: 0,
                          max: 200,
                        //   position: 'right',
                          axisLine: {
                              lineStyle: {
                                  color: '#999'
                              }
                          },
                          axisLabel: {
                              formatter: '{value}'
                          }
                        },
                    ],
                    series: [
                        {
                            name:'新注册用户',
                            type:'line',
                            data:this.sevenDate[0],
                            yAxisIndex: 1,
                            markPoint: {
                                data: [
                                    {type: 'max', name: '最大值'},
                                    {type: 'min', name: '最小值'}
                                    
                                ]
                            },
                        },
                        {
                            name:'新增订单',
                            type:'line',
                            data:this.sevenDate[1],
                            yAxisIndex: 1,
                            markPoint: {
                                data: [
                                    {type: 'max', name: '大值'},
                                    {type: 'min', name: '小值'}
                                ]
                            },
                        },
                        {
                            name:'新增管理员',
                            type:'line',
                            data:this.sevenDate[2],
                            yAxisIndex: 1,
                            markPoint: {
                                data: [
                                    {type: 'max', name: '最大值'},
                                    {type: 'min', name: '最小值'}
                                ]
                            },
                        }
                    ]
              };
                this.myChart.setOption(option);
            }
        },
        watch: {
            sevenDate: function (){
                this.initData()
            },
            sevenDay: function (){
                this.initData()
            }
        }
    }
</script>

<style lang="less">
	@import '../style/mixin';
    .line1{
        display: flex;
        justify-content: center;
    }
</style>
