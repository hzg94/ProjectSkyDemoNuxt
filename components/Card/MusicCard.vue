<template>
  <Card :card_type="CardTypeEnum.Big">
    <template #Header>
      Music Play
    </template>
    <template #Action>
      <el-button v-show="!IsPlay" size="small" type="primary" @click="Play">播放</el-button>
      <el-button v-show="IsPlay" size="small" type="danger" @click="Play">暂停</el-button>
      <el-button size="small">下一首</el-button>
    </template>
    <template #default>
      <div class="BodyFlex">
        <el-avatar
            :size="130"
            shape="square"
            src="https://p2.music.126.net/x44v5IkLN30gWgUYWYivbg==/109951164000997664.jpg?param=140y140"
        />
        <div class="MusicMessage">
          <p class="Title">
            测试 (测试歌手)
          </p>
          <el-progress :percentage="30" :show-text="false" :status="IsPlay ? ``: `warning` " style="width: 100%"/>
          <p class="PlayTime">
            1:00/3:00
          </p>
        </div>
      </div>
    </template>
    <template #BottomLeft>
      <span class="ReadyLrc">AA</span>
    </template>
    <template #BottomRight>
      <span class="NoReadyLrc">next:AAA</span>
    </template>
  </Card>
</template>

<script lang="ts">
import {defineComponent} from 'vue'
import Card from "../Card/index.vue";
import {CardTypeEnum} from "@/components/Card/types";

export default defineComponent({
  name: "MusicCard",
  computed: {
    CardTypeEnum() {
      return CardTypeEnum
    }
  },
  components: {Card},
  data() {
    return {
      IsPlay: false
    }
  },
  methods: {
    Play() {
      this.IsPlay = !this.IsPlay
    }
  },
})
</script>

<style lang="less" scoped>
.ReadyLrc{

}
.NoReadyLrc {
  color: #8c8c8c;
}

.BodyFlex {
  display: flex;

  .MusicMessage {
    vertical-align: top;
    padding-left: 15px;
    height: 100%;
    display: inline-flex;
    flex-direction: column;
    flex-grow: 1;

    .Title {
      flex-grow: 1;
      margin: 0;
      font-size: 20px;
      font-weight: bold;
      width: 100%;
    }

    .PlayTime {
      flex-grow: 1;
      margin: 0;
    }


  }
}

</style>