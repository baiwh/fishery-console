<template>
  <div class="console">

    <div class="echarts-box">
      <img class="echarts-img" src="./../../static/left.png" alt="">
      <div class="echarts-window">

      </div>
      <img class="echarts-img" src="./../../static/right.png" alt="">
    </div>

    <div class="nav">
      <div v-for="(item,index) in buttonData">
        <div
          :class="checkedButton == index?'nav-item-checked':'nav-item'"
          @click="checkButton(item,index)">
          <div class="nav-title">{{item.title}}</div>
          <div class="nav-data">
            {{item.data}}<span class="nav-unit">{{item.unit}}</span>
          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
  import axios from 'axios'
  // import echarts from 'echarts'
  export default {
    name: 'HelloWorld',
    data() {
      return {
        buttonData: [
          {
            title: '环境温度',
            data: 0,
            unit: '℃'
          },
          {
            title: '环境湿度',
            data: 0,
            unit: '%'
          },
          {
            title: 'CO₂',
            data: 0,
            unit: '%'
          },
          {
            title: '光照强度',
            data: 0,
            unit: 'lux'
          },
          {
            title: '土壤温度',
            data: 0,
            unit: '℃'
          },
          {
            title: '土壤湿度',
            data: 0,
            unit: '%'
          },
          {
            title: '土壤PH',
            data: 0,
            unit: ''
          }
        ],
        checkedButton: 0,
      }
    },
    mounted() {
      this.getButtonData()
    },
    methods: {
      // 点击切换按钮
      checkButton: function (item, index) {
        console.log(item, index)
        this.checkedButton = index
        switch (index) {
          case 0 :
            this.getEchartsData('airTemperature')
            break
          case 1 :
            this.getEchartsData('airHumidity')
            break
          case 2 :
            this.getEchartsData('CO2')
            break
          case 3 :
            this.getEchartsData('illuminance')
            break
          case 4 :
            this.getEchartsData('soilTemperature')
            break
          case 5 :
            this.getEchartsData('soilHumidity')
            break
          case 6 :
            this.getEchartsData('soilpH')
            break
        }
      },

      // 获取图表数据的接口
      getEchartsData: function (type) {
        axios.get('/api/device/get_data_in_chart', {
          params: {
            id: 504626770,
            type: type
          },
          withCredentials: false
        }).then((res) => {
          console.log(res.data.data)
          let data = res.data.data
        })
      },

      // 获取按钮数据的接口
      getButtonData: function () {
        axios.get('/api/device/get_latest_data', {
          params: {
            id: 504626770
          },
          withCredentials: false
        }).then((res) => {
          console.log(res.data.data)
          let data = res.data.data
          this.buttonData[0].data = data.airTemperature
          this.buttonData[1].data = data.airHumidity
          this.buttonData[2].data = data.CO2
          this.buttonData[3].data = data.illuminance
          this.buttonData[4].data = data.soilTemperature
          this.buttonData[5].data = data.soilHumidity
          this.buttonData[6].data = data.soilpH
        })
      }
    }
  }
</script>

<style scoped>
  .console {
    height: 100vh;
    width: 100vw;
  }

  .echarts-box {
    width: 100vw;
    display: flex;
    justify-content: space-between;
    top: 13vh;
    position: relative;
    align-items: center;
  }

  .echarts-img {
    height: 31vh;
    width: 21vw;
  }

  .echarts-window {
    height: 49vh;
    width: 51vw;
    background: url("./../../static/3.png");
    overflow: auto;
    background-size: 100% 100%;
  }

  .nav {
    display: flex;
    justify-content: space-between;
    position: relative;
    top: 22vh;
    margin: 0 12vw;
    color: #ffffff;
  }

  .nav-item {
    height: 9vw;
    width: 9vw;
    background: url("./../../static/1.png");
    background-size: 100% 100%;
    position: relative;
    cursor: pointer;
  }

  .nav-item-checked {
    height: 9vw;
    width: 9vw;
    background: url("./../../static/2.png");
    background-size: 100% 100%;
    color: #ffaa00;
    position: relative;
    cursor: pointer;
  }

  .nav-title {
    font-size: 0.8vw;
    position: absolute;
    transform: translateX(-50%);
    left: 50%;
    top: 2.7vw;
  }

  .nav-data {
    font-size: 1.5vw;
    position: absolute;
    transform: translateX(-50%);
    left: 50%;
    text-align: center;
    top: 4.3vw;
  }

  .nav-unit {
    font-size: 0.6vw;
  }
</style>
