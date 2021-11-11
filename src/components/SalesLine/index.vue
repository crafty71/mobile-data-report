<template>
  <div class="sales-line">
    <div class="sales-line-inner">
      <vue-echarts :options="options" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: Object
  },
  data() {
    return {
      options: {}
    }
  },
  watch: {
    data() {
      this.update()
      console.log(this.data)
    }
  },
  methods: {
    update() {
      if (this.data) {
        const _data = this.data.saleLine
        const axis = _data.axis
        const data1 = _data.data1
        const data2 = _data.data2
        const data3 = _data.data3
        this.options = {
          title: {
            text: '分时访问&成交趋势图',
            textStyle: {
              color: '#fff'
            },
            left: 10,
            top: 10
          },
          tooltip: {
            trigger: 'axis'
          },
          grid: {
            left: '3%',
            right: '5%',
            bottom: '3%',
            containLabel: true
          },
          xAxis: {
            type: 'category',
            boundaryGap: false,
            data: axis,
            axisLabel: {
              color: 'rgba(255,255,255,.3)'
            },
            axisLine: {
              show: false
            }
          },
          yAxis: {
            type: 'value',
            axisLabel: {
              color: 'rgba(255,255,255,.3)'
            },
            splitLine: {
              lineStyle: {
                color: 'rgba(255,255,255,.1)'
              }
            }
          },
          series: [
            {
              name: '访问量',
              type: 'line',
              smooth: true,
              itemStyle: {
                opacity: 0,
                color: 'rgb(0, 163, 233)'
              },
              data: data1
            },
            {
              name: '成交量',
              type: 'line',
              smooth: true,
              itemStyle: {
                opacity: 0,
                color: 'yellow'
              },
              data: data2
            },
            {
              name: 'KPI',
              type: 'line',
              smooth: true,
              itemStyle: {
                opacity: 0,
                color: 'red'
              },
              data: data3
            }
          ]
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.sales-line {
  position: absolute;
  top: 950px;
  left: 0;
  z-index: 10;
  width: 100%;
  height: 500px;
  padding: 25px 25px 0;
  box-sizing: border-box;

  .sales-line-inner {
    width: 100%;
    height: 100%;
    background: rgba(255, 255, 255, 0.05);
  }
}
</style>
