<template>
  <Card :card_type="CardTypeEnum.Middle">
    <template #Header>
      TO-DO List
    </template>
    <template #Action>
      <span v-show="tableData.length !== 0">你还有{{ tableData.length }}件事情未解决</span>
      <span v-show="tableData.length === 0">今天任务已全部完成</span>
    </template>
    <template #default>
      <el-table :data="tableData" :show-header="false" row-key="id" class="ElTable"
                @row-click="CheckNumber">
        <el-table-column label="data" prop="data">
          <template #default="scope">
            <AnimateFadeOut :animation_type="FadeOutAnimate.Right">
              <div v-show="scope.row.Read">{{ scope.row.data }}</div>
            </AnimateFadeOut>
          </template>
        </el-table-column>
        <template #empty>
          <el-result
              icon="success"
              style="height: 120px"
              sub-title="今天任务已全部完成"
          />
        </template>
      </el-table>
    </template>
    <template #BottomRight>
      <AnimateFadeOut>
        <el-button v-show="tableData.length !== 0" size="small" @click="AllFinish">
          这些全部已完成
        </el-button>
      </AnimateFadeOut>
    </template>
  </Card>
</template>

<script lang="ts" setup>
import Card from "../Card/index.vue";
import {Ref, ref} from "vue";
import {CardTypeEnum} from "./types";
import {FadeOutAnimate} from '../Animate/FadeOut/index.vue'

// type
type tableType = {
  id: number,
  data: string,
  Read: boolean
}

let Data = new Array(10)

for (let i = 0; i <= Data.length - 1; i++) {
  Data[i] = {id: i, data: "Message Demo" + i, Read: true}
}


// vue ref
let tableData: Ref<Array<tableType>> = ref(Data)


//methods
const CheckNumber = (_ :tableType) => {
  tableData.value.forEach((x, index) => {
    if (x.id == _.id) {
      tableData.value[index].Read = false
      setTimeout(function () {
        tableData.value.splice(index, 1)
      },400)
    }
  })
}

const AllFinish = () => {
  for (let i = 0; i < tableData.value.length; i++) {
    tableData.value[i].Read = false
  }
  setTimeout(function () {
    tableData.value = []
  },400)
}
</script>


<style scoped>
.ElTable{
  height: 100%;
  --el-table-bg-color: none;
  --el-table-tr-bg-color: none;
  --el-table-row-hover-bg-color:none;
  --el-table-border: 2px solid rgba(5, 5, 5, 0.06);
}
</style>