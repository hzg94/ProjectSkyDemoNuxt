<template>
  <Card :card_type="CardTypeEnum.Middle" :set_bottom_div="false">
    <template #Header>
      time
    </template>
    <template #default>
      <div class="TimeDiv">
        <p class="Time">{{time}}</p>
        <span class="Day">{{day}}</span>
      </div>
    </template>
  </Card>
</template>

<script lang="ts" setup>
import {CardTypeEnum} from "./types";
import localizedFormat from 'dayjs/plugin/localizedFormat'
import 'dayjs/locale/zh-cn.js'
import dayjs from "dayjs";
import {onMounted} from "vue";

// dayjs init
dayjs.locale('zh-cn')
dayjs.extend(localizedFormat);

let time = ref("")
let day = ref("")

onMounted(() => {
  day.value = dayjs().format("YYYY/MM/DD dddd")
  setInterval(() => {
    time.value = dayjs().format("HH : mm : ss")
  },999)
})

</script>

<style lang="less" scoped>
.TimeDiv {
  display: flex;
  flex-wrap: wrap;

  .Time {
    margin: 0;
    width: 100%;
    font-weight: bold;
    font-size: 50px;
    text-align: center;
  }

  .Day {
    margin-top: 5px;
    width: 100%;
    text-align: center;
  }
}

</style>