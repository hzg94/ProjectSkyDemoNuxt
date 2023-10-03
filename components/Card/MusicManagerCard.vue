<template>
  <Card :header_height="`15%`" :card_type="CardTypeEnum.Big" :set_bottom_div="false">
    <template #Header>
      热门榜
    </template>
    <template #Action>
      <el-input
          v-model="SearchInput"
          placeholder="请输入歌曲信息"
          size="small"
      >
        <template #append>
          <el-button :icon="Search"/>
        </template>
      </el-input>
    </template>
    <template #default>
      <el-table :data="tableData"  row-key="id" class="ElTable"
                @row-click="CheckNumber">
        <template #empty>
          <el-result
              icon="error"
              style="height: 120px"
              sub-title="服务异常"
          />
        </template>
      </el-table>
    </template>
  </Card>
</template>

<script lang="ts" setup>
import Card from "../Card/index.vue";
import {Search} from "@element-plus/icons-vue";
import {ref} from "vue";
import {CardTypeEnum} from "@/components/Card/types";

let SearchInput = ref("")

let tableData = ref([])

const CheckNumber = (_:any) => {

}

</script>

<style lang="less" scoped>
.ElTable{
  height: 100%;
  --el-table-bg-color: none;
  --el-table-tr-bg-color: none;
  --el-table-row-hover-bg-color:none;
  --el-table-border: 2px solid rgba(5, 5, 5, 0.06);
}
</style>