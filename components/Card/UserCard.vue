<template>
  <Card :body_height="`150px`" :set_header_div="false">
    <template #default>
      <el-avatar :size="90" :src="user_avatar"/>
      <br/>
      <p class="UserName">{{ user_name }}</p>
      <span class="UserEMail">admin@admin.org</span>
    </template>
    <template #BottomRight>
      <el-button @click="OnEdit" size="small">编辑</el-button>
    </template>
  </Card>
</template>

<script lang="ts" setup>

let emits = defineEmits(["OnEdit"])

let props = defineProps({
  user_name: {
    type: String,
    default: "Admin"
  },
  user_avatar: {
    type: String,
    default: "https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png"
  }
})

const OnEdit = () => {
  emits('OnEdit',[props.user_name])
}
</script>

<style scoped>
.UserName {
  display: inline-block;
  width: 100%;
  margin-top: 3px;
  margin-bottom: 0;
  font-size: 19px;
  font-weight: bold;
}

.UserEMail {
  color: #8c8c8c;
}
</style>