<template>
  <div class="sales-radar">
    <div class="sales-radar-inner">
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
      console.log(this.data)
      this.update()
    }
  },
  methods: {
    update() {
      if (this.data) {
        const { salesRadar } = this.data
        console.log(salesRadar)
        const { data, indicator } = salesRadar
        console.log(data, indicator)
        this.options = {
          tooltip: {},
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
            indicator: indicator
          },
          series: [
            {
              name: '运营指标',
              type: 'radar',
              // areaStyle: {normal: {}},
              data: data
            }
          ]
        }
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.sales-radar {
  position: absolute;
  top: 3250px;
  left: 0;
  z-index: 10;
  width: 100%;
  height: 800px;
  padding: 25px 25px 0;
  box-sizing: border-box;

  .sales-radar-inner {
    width: 100%;
    height: 100%;
    background: rgba(255, 255, 255, 0.05);
  }
}
</style>
