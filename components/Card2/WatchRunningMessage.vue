<template>
  <Card2 :body_height="`150px`">
    <template #Header>
      <el-avatar class="Icons" :src="Redis" shape="circle"/>
      <span class="Title">Redis 监控</span>
    </template>
    <template #Action>
      <span class="WatchType">CPU利用率</span>
    </template>
    <template #default>
      <div ref="Main" class="main"/>
    </template>
  </Card2>
</template>

<script lang="ts" setup>
import Redis from '../../assets/icon/Redis.svg'
import * as echarts from 'echarts';
import {EChartsType} from "echarts";
import {ECBasicOption} from "echarts/types/dist/shared";

let Main: Ref<HTMLDivElement | undefined> = ref()

let Chart: Ref<EChartsType | undefined> = ref()

let max_value = 10

let data: Array<Array<any>> = []

let option:ECBasicOption = {
  xAxis: {
    type: 'time',
    axisLabel:{
      formatter: '{mm}:{ss}'
    },
    splitLine: {
      show: false
    }
  },
  yAxis: {
    type: 'value',
    splitLine: {
      show: false
    }
  },
  series: [
    {
      name: 'Fake Data',
      type: 'line',
      data: data
    }
  ],
  height: 120,
  grid: {
    y: 10
  }
}

onMounted(() => {

  Chart.value = echarts.init(Main.value);

  Chart.value.setOption(option);

  setInterval(() => {
    let now = new Date();
    if(data.length >=  max_value){
      data.shift()
    }
    data.push([new Date(),Math.random() * 10])
    Chart.value?.setOption({
      series: [
        {
          data: data
        }
      ]
    })
  }, 1000)
});

const DataAdd = () => {
  Chart.value?.appendData({
    seriesIndex: 5,
    data: ['5', 77]
  })
}

</script>

<style scoped>
.WatchType{
  color: #8c8c8c;
  font-size: 10px;
}

.Icons {
  margin-bottom: 0;
  margin-top: 5px;
  background: none;
  vertical-align: middle;
  margin-right: 5px;
}

.Title {
  vertical-align: middle;
}


.main {
  width: 100%;
  height: 150px;
}
</style>