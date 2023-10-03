<template>
  <Card2 >
    <template #Header>
      <el-avatar :src="python" class="Ac"/>
      <span class="Title">Python 每日一闻</span>
    </template>
    <template #Action>
      <el-button @click="GetData" class="ReFlush" circle :icon="Loading"/>
    </template>
    <template #default>
      <el-table v-loading="GetLoading" :data="tableData" :show-header="false" row-key="id" class="ElTable"
                @row-click="CheckNumber" :max-height="150">
        <el-table-column label="data" prop="data">
          <template #default="scope">
            <div>{{ scope.row.data }}</div>
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
  </Card2>
</template>

<script lang="ts" setup>
import python from '../../assets/icon/python.svg'
import {Loading} from "@element-plus/icons-vue";
import {Ref, ref} from "vue";

type tableType = {
  id: number,
  data: string,
  Read: boolean
}

const GetLoading = ref(false)


const GetData = () => {
  GetLoading.value = true
  setTimeout(() => {
    GetLoading.value = false
  }, 55000)
}

let Data = new Array(10)

for (let i = 0; i <= Data.length - 1; i++) {
  Data[i] = {id: i, data: "Message Demo" + i, Read: true}
}


// vue ref
let tableData: Ref<Array<tableType>> = ref(Data)


//methods
const CheckNumber = (_: tableType) => {
  tableData.value.forEach((x, index) => {

  })
}

</script>

<style lang="less" scoped>
.ElTable {
  height: 100%;
  --el-table-bg-color: none;
  --el-table-tr-bg-color: none;
  --el-table-row-hover-bg-color: none;
  --el-table-border: 2px solid rgba(5, 5, 5, 0.06);
  --el-mask-color:rgba(255,255,255,0.3);
}

.Ac {
  margin-bottom: 0;
  margin-top: 5px;
  background: none;
  vertical-align: middle;
}

.Title {
  vertical-align: middle;
}
</style>