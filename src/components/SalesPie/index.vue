<template>
  <div class="sales-pie">
    <div class="sales-pie-inner">
      <div class="pie-item">
        <div class="pie-item-inner">
          <vue-echarts :options="options1" />
        </div>
      </div>
      <div class="pie-item">
        <div class="pie-item-inner">
          <vue-echarts :options="options2" />
        </div>
      </div>
      <div class="pie-item">
        <div class="pie-item-inner">
          <vue-echarts :options="options3" />
        </div>
      </div>
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
      options1: {},
      options2: {},
      options3: {}
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
        const _data = this.data.salePie
        const data1 = _data[0]
        const data2 = _data[1]
        const data3 = _data[2]
        const createOptions = (title, value, values) => {
          return {
            title: [
              {
                text: title,
                textStyle: {
                  color: 'rgba(255,255,255,.3)',
                  fontSize: 12
                },
                top: 3
              },
              {
                text: value,
                textStyle: {
                  color: 'rgba(255,255,255)',
                  fontSize: 16,
                  fontWeight: 500
                },
                top: '43%',
                left: '32%'
              }
            ],
            tooltip: {
              trigger: 'item',
              formatter: '{a} <br/>{b}: {c} ({d}%)'
            },
            series: [
              {
                name: title,
                type: 'pie',
                radius: ['65%', '80%'],
                avoidLabelOverlap: false,
                label: {
                  show: false,
                  position: 'center'
                },
                emphasis: {
                  label: {
                    show: true,
                    fontSize: '30',
                    fontWeight: 'bold'
                  }
                },
                labelLine: {
                  show: false
                },
                data: [
                  {
                    value: values[0],
                    name: '数据',
                    itemStyle: {
                      color: 'rgb(0, 140, 217)'
                    }
                  },
                  {
                    value: values[1],
                    name: '数据',
                    itemStyle: {
                      color: 'rgb(35, 69, 145)'
                    }
                  }
                ]
              }
            ]
          }
        }
        this.options1 = createOptions(data1.name, data1.total, data1.data)
        this.options2 = createOptions(data2.name, data2.total, data2.data)
        this.options3 = createOptions(data3.name, data3.total, data3.data)
      }
    }
  },
  mounted() {}
}
</script>

<style lang="scss" scoped>
.sales-pie {
  position: absolute;
  top: 1450px;
  left: 0;
  z-index: 10;
  width: 100%;
  height: 400px;
  padding: 25px 12.5px 0;
  box-sizing: border-box;

  .sales-pie-inner {
    display: flex;
    width: 100%;
    height: 100%;

    .pie-item {
      flex: 0 0 33.33%;
      width: 33.33%;
      height: 100%;
      padding: 0 12.5px;
      box-sizing: border-box;

      .pie-item-inner {
        width: 100%;
        height: 100%;
        background: rgba(255, 255, 255, 0.05);
      }
    }
  }
}
</style>
