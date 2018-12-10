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
  export default {
    name: 'HelloWorld',
    data() {
      return {
        buttonData: [
          {
            title: '环境温度',
            data: 30,
            unit: '℃'
          },
          {
            title: '环境湿度',
            data: 70.8,
            unit: '%'
          },
          {
            title: 'CO₂',
            data: 18,
            unit: '%'
          },
          {
            title: '光照强度',
            data: 5678,
            unit: 'lux'
          },
          {
            title: '土壤温度',
            data: 24.3,
            unit: '℃'
          },
          {
            title: '土壤湿度',
            data: 79.4,
            unit: '%'
          },
          {
            title: '土壤PH',
            data: 7.4,
            unit: ''
          }
        ],
        checkedButton: 0,
      }
    },
    methods:{
      // 点击切换按钮
      checkButton:(item,index)=>{
        console.log(item,index)
        this.checkedButton = index
      },

      // 切换图表
    }
  }
</script>

<style scoped>
  .console{
    height: 100vh;
    width: 100vw;
  }
  .echarts-box{
    width: 100vw;
    display: flex;
    justify-content: space-between;
    top: 13vh;
    position: relative;
    align-items: center;
  }
  .echarts-img{
    height: 31vh;
    width: 21vw;
  }
  .echarts-window{
    height: 49vh;
    width: 51vw;
    background: url("./../../static/3.png");
    overflow: auto;
    background-size: 100% 100%;
  }
  .nav{
    display: flex;
    justify-content: space-between;
    position: relative;
    top: 22vh;
    margin: 0 12vw;
    color: #ffffff;
  }
  .nav-item{
    height: 9vw;
    width: 9vw;
    background: url("./../../static/1.png");
    background-size: 100% 100%;
    position: relative;
    cursor: pointer;
  }
  .nav-item-checked{
    height: 9vw;
    width: 9vw;
    background: url("./../../static/2.png");
    background-size: 100% 100%;
    color: #ffaa00;
    position: relative;
    cursor: pointer;
  }
  .nav-title{
    font-size: 0.8vw;
    position: absolute;
    transform: translateX(-50%);
    left: 50%;
    top: 2.7vw;
  }
  .nav-data{
    font-size: 1.5vw;
    position: absolute;
    transform: translateX(-50%);
    left: 50%;
    text-align: center;
    top: 4.3vw;
  }
  .nav-unit{
    font-size: 0.6vw;
  }
</style>
