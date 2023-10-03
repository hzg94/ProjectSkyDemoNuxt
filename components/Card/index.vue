<template>
  <div :class="`CardDiv ${cardType}`">
    <div v-if="set_header_div" class="HeaderDiv">
      <div ref="HeaderSlot" class="HeaderSlot">
        <slot name="Header"/>
      </div>
      <div ref="ActionSlot" class="ActionSlot">
        <slot name="Action"/>
      </div>
    </div>
    <div ref="BodySlot" class="BodySlot">
      <slot/>
    </div>
    <div v-if="set_bottom_div" class="BottomDiv">
      <div ref="BottomLeft" class="BottomLeft">
        <slot name="BottomLeft"/>
      </div>
      <div ref="BottomRight" class="BottomRight">
        <slot name="BottomRight"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import {CardTypeEnum} from "./types";
import {PropType} from "vue";

let props = defineProps({
  card_type: {
    type: Number as PropType<CardTypeEnum>,
    default: CardTypeEnum.Small
  },
  header_height: {
    type: String,
    default: "12%"
  },
  set_header_div: {
    type: Boolean,
    default: true
  },
  set_bottom_div: {
    type: Boolean,
    default: true
  },
  body_height: {
    type: String,
    default: "135px"
  }
})

let cardType: string = "Small";

switch (props.card_type) {
  case CardTypeEnum.Small: {
    cardType = "Small"
    break;
  }
  case CardTypeEnum.Middle: {
    cardType = "Middle"
    break;
  }
  case CardTypeEnum.Big: {
    cardType = "Big"
    break;
  }
  default: {
    console.error("Card Type Error")
  }
}


</script>

<style lang="less" scoped>
.CardDiv {
  display: flex;
  flex-wrap: wrap;
  padding-top: 5px;
  padding-bottom: 5px;
  background-color: rgba(255, 255, 255, 0.72);
  backdrop-filter: saturate(180%) blur(20px);
  box-shadow: 0 1px 2px -2px rgba(0, 0, 0, 0.16),
  0 3px 6px 0 rgba(0, 0, 0, 0.12),
  0 5px 12px 4px rgba(0, 0, 0, 0.09);

  &.Small {
    width: 200px;
    height: 200px;
    border-radius: 10%;
  }

  &.Middle {
    width: 400px;
    height: 200px;
    border-radius: 15px;
  }

  &.Big {
    width: 600px;
    height: 200px;
    border-radius: 20px;
  }
}

// Header
.HeaderDiv {
  display: flex;
  height: v-bind(header_height);
  width: 100%;
  padding-bottom: 5px;
  border-bottom: 2px solid rgba(5, 5, 5, 0.06);
  align-items: center;

  .HeaderSlot {
    padding-left: 10px;
    flex-grow: 1;
  }

  .ActionSlot {
    padding-right: 10px;
    transform-origin: right center;
  }
}

// Body
.BodySlot {
  height: v-bind(body_height);
  max-height: 100%;
  width: 100%;
  padding-left: 10px;
  padding-right: 10px;
  overflow: hidden;
  word-wrap: break-word;
  word-break: normal;
}

// Bottom
.BottomDiv {
  align-self: flex-end;
  display: flex;
  padding-top: 5px;
  padding-right: 5px;
  padding-left: 5px;
  width: 100%;
  border-top: 2px solid rgba(5, 5, 5, 0.06);

  .BottomLeft {
    padding-left: 10px;
    flex-grow: 1;
  }

  .BottomRight {
    padding-right: 10px;
    transform-origin: right center;
  }
}
</style>
