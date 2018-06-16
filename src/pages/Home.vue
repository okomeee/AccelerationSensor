<template>
  <v-ons-page>
    <v-ons-toolbar class="home-toolbar">
      <div class="center">{{ msg }}</div>
    </v-ons-toolbar>

    <div class="header" style="margin: 5% 0;">
      <img src="../assets/Vso59x2r_400x400.jpg" alt="logo">
    </div>

    <div style="text-align: center;"><button @click="init()"><p style="display: inline-block;margin:2% 0;">加速度センサ</p></button></div>
    <div id="force" style="font-size: 64px; text-align: center; margin: 5% 0;">{{ force }}</div>
  </v-ons-page>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      msg: 'AccelerationSensor',
      force: '',
      ua: {}
    }
  },
  methods: {
    init () {
      window.addEventListener('devicemotion', this.devicemotionHandler)
      this.ua = window.navigator.userAgent
    },
    devicemotionHandler (event) {
      // 加速度
      // X軸
      let x = event.acceleration.x
      // Y軸
      let y = event.acceleration.y
      // Z軸
      let z = event.acceleration.z
      if (this.ua.indexOf('iPhone') > 0 || this.ua.indexOf('iPad') > 0 || this.ua.indexOf('iPod') > 0) {
        x *= -1
        y *= -1
        z *= -1
      }
      if (x < -3) {
        this.force = '右'
      } else if (x > 3) {
        this.force = '左'
      } else if (y < -3) {
        this.force = '上'
      } else if (y > 3) {
        this.force = '下'
      } else if (z < -3) {
        this.force = '手前'
      } else if (z > 3) {
        this.force = '奥'
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.header {
  text-align: center;
}

img {
  max-width: 300px;
}

ons-list-title {
  text-transform: none;
}

ons-list-title:not(:first-of-type) {
  margin-top: 30px;
}

ons-card {
  text-align: center;
}

ons-list-item, ons-card {
  cursor: pointer;
}
</style>
