<template>
  <div id="main"></div>
</template>

<script>
import * as echarts from 'echarts'
export default {
  data() {
    return {}
  },

  created() {},
  mounted() {
    this.initEcharts()
  },
  methods: {
    initEcharts() {
      // 基于准备好的dom，初始化echarts实例
      var myChart = echarts.init(document.getElementById('main')) // 操作了dom 通过mounted调用
      // 绘制图表
      const radarOption = {
        color: ['#67F9D8', '#56A3F1'],
        backgroundColor: 'skyblue',
        title: {
          text: '雷达图',
          textStyle: {
            color: '#eee'
          }
        },
        legend: {
          bottom: 5,
          data: ['lis', 'pole'],

          itemGap: 20,
          textStyle: {
            color: 'purple',
            fontSize: 14
          },
          selectedMode: 'single'
        },

        radar: {
          // shape: 'circle',
          indicator: [
            { name: 'Sales', max: 100 },
            { name: 'Administration', max: 100 },
            { name: 'Information Technology', max: 100 },
            { name: 'Customer Support', max: 100 },
            { name: 'Development', max: 100 },
            { name: 'Marketing', max: 100 }
          ],
          axisName: {
            color: 'blue'
          },
          axisLine: {
            lineStyle: {
              color: 'orange'
            }
          }
        },
        series: [
          {
            name: 'Budget vs spending',
            type: 'radar',
            data: [
              {
                value: [40, 50, 60, 60, 80, 90],
                name: 'lis'
              },
              {
                value: [60, 95, 60, 95, 60, 95],
                name: 'pole'
              }
            ]
          }
        ]
      }
      myChart.setOption(radarOption)
    }
  }
}
</script>

<style scoped lang="scss">
#main {
  height: 500px;
  width: 100%;
}
</style>
