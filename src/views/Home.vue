<template>
  <div class="home" v-if="!loading">
    <div class="data-wrapper" />
    <top-header />
    <sales-bar :data="data" />
    <sales-line :data="data" />
    <sales-pie :data="data" />
    <sales-map :data="data" />
    <sales-sun :data="data" />
    <sales-radar :data="data"/>
  </div>
  <div class="home" v-else>
    <div class="loading0wraooer"></div>
    <loading />
  </div>
</template>

<script>
import { getScreenMobileData } from '../api/index'
import loading from '../components/Loading/index.vue'

export default {
  name: 'Home',
  components: {
    loading
  },
  watch: {
    data() {
      console.log(this.data)
    }
  },
  data() {
    return {
      data: null,
      loading: true
    }
  },
  mounted() {
    getScreenMobileData()
      .then(data => {
        this.loading = false
        this.$nextTick(() => {
          this.data = data
        })
      })
      .catch(err => {
        console.log(err)
      })
  }
}
</script>

<style lang="scss" scoped>
.home {
  position: relative;
  height: 100%;
  .data-wrapper {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 1336px;
    z-index: 1;
    background-image: url("//datav.oss-cn-hangzhou.aliyuncs.com/uploads/images/44b2ad11c37339db11f8ca5d59c5b31c.jpg");
    background-size: 100% 100%;
    background-repeat: no-repeat;
  }
}
</style>
