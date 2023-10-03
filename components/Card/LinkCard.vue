<template>
  <Card :body_height="`100%`" :set_bottom_div="false" :set_header_div="false">
    <div class="LinkIconsDiv">
      <el-popover
          placement="top-start"
          :title="item.alt"
          :width="1"
          :show-arrow="false"
          :popper-style="PopplerStyle"
          trigger="hover"
          v-for="item in icons"
      >
        <template #reference>
          <el-avatar
              :src="item.icon"
              class="Icons"
              shape="square"
              @click="OpenLinkUrl(item.url)"/>
        </template>
      </el-popover>
    </div>
  </Card>
</template>

<script lang="ts">

import {defineComponent} from 'vue'
import Card from "../Card/index.vue";
import python from '../../assets/icon/python.svg'

export default defineComponent({
  name: "LinkCard",
  components: {Card},
  data() {
    return {}
  },
  methods: {
    OpenLinkUrl(url: string) {
      window.open(url)
    }
  },
  mounted() {
    let alpha = 0.72
    let Colors = [
      `rgba(92,219,211,${alpha})`,
      `rgba(105,177,255,${alpha})`,
      `rgba(149,222,100,${alpha})`,

      `rgba(255,214,102,${alpha})`,
      `rgba(255,245,102,${alpha})`,
      `rgba(211,242,97,${alpha})`,

      `rgba(255,120,117,${alpha})`,
      `rgba(255,156,110,${alpha})`,
      `rgba(255,192,105,${alpha})`,
    ]
    let elementNodeListOf = document.querySelectorAll('.Icons');
    for (let i = 0; i < elementNodeListOf.length; i++) {
      elementNodeListOf[i].setAttribute("style", `background-color:${Colors[i] ? Colors[i] : "red"}`)
    }

  },
  setup() {
    let icons = new Array(9)

    for (let i = icons.length - 1; i >= 0; i--) {
      icons[i] = {
        "icon": python,
        "url": "https://www.python.org",
        "alt": "mysql"
      }
    }

    let PopplerStyle = {
      "background": "none",
      "border":"none",
      "backdrop-filter": "saturate(180%) blur(20px)",
    }

    return {
      icons,PopplerStyle
    }
  },
})
</script>
<style lang="less" scoped>
.LinkIconsDiv {
  display: flex;
  height: 100%;
  flex-wrap: wrap;
  justify-content: center;
  align-content: center;

  & > * {
    margin: 7px;
    backdrop-filter: saturate(180%) blur(20px);
  }
}
</style>