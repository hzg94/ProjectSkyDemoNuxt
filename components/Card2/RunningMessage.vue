<template>
  <Card2>
    <template #Header>
      <el-avatar class="Icons" :src="Mysql" shape="square" />
      <span class="Title">数据库信息</span>
    </template>
    <template #default>
      <div class="MessageConDiv">
        <div class="MessageDiv">
          <p>数据库数量</p><br/>
          <span>6</span>
        </div>
        <div class="MessageDiv">
          <p>用户数量</p><br/>
          <span>3</span>
        </div>
        <div class="MessageDiv">
          <p>数据库总大小</p><br/>
          <span>6MB</span>
        </div>
        <div class="MessageDiv">
          <p>数据库版本</p><br/>
          <span>8</span>
        </div>
      </div>
    </template>
  </Card2>
</template>

<script lang="ts" setup>

import Mysql from '../../assets/icon/Mysql.svg'
</script>

<style scoped lang="less">
.MessageConDiv{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  width: 100%;
  height: 100%;
}
.MessageDiv{
  width: 150px;
  height: 60px;
  display: flex;
  flex-wrap: wrap;
  padding-left: 5px;
  border-radius: 10px;
  background: white;
  align-items: center;
  p{
    margin: 0;
  }
  span{
    display: inline-block;
    width: 100%;
    color: #8c8c8c;
  }
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


</style>