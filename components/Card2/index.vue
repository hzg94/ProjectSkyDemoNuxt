<template>
  <div :class="`CardDiv ${cardType}`">
    <div v-if="set_header_div" class="HeaderDiv">
      <div  class="HeaderSlot">
        <slot name="Header"/>
      </div>
      <div  class="ActionSlot">
        <slot name="Action"/>
      </div>
    </div>
    <div  class="BodySlot">
      <slot/>
    </div>
    <div v-if="set_bottom_div" class="BottomDiv">
      <div  class="BottomLeft">
        <slot name="BottomLeft"/>
      </div>
      <div  class="BottomRight">
        <slot name="BottomRight"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent, PropType} from 'vue'
import {CardTypeEnum} from "@/components/Card/types";


export default defineComponent({
  name: "Card",
  props: {
    card_type: {
      type: Number as PropType<CardTypeEnum>,
      default: CardTypeEnum.Middle
    },
    header_height: {
      type: String,
      default: "20%"
    },
    set_header_div: {
      type: Boolean,
      default: true
    },
    set_bottom_div: {
      type: Boolean,
      default: false
    },
    body_height: {
      type: String,
      default: "135px"
    }
  },
  setup(props) {
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
    return {
      cardType: cardType
    }
  },
})
</script>

<style scoped lang="less">
// var
@Border_Small: 10%;
@Border_Middle: 15px;
@Border_Big: 20px;


.CardDiv {
  display: flex;
  flex-wrap: wrap;
  padding-bottom: 5px;
  background-color: rgba(255, 255, 255, 0.72);
  backdrop-filter: saturate(180%) blur(20px);
  box-shadow: 0 1px 2px -2px rgba(0, 0, 0, 0.16),
  0 3px 6px 0 rgba(0, 0, 0, 0.12),
  0 5px 12px 4px rgba(0, 0, 0, 0.09);

  &.Small {
    width: 200px;
    height: 200px;
    border-radius: @Border_Small;
  }

  &.Middle {
    width: 400px;
    height: 200px;
    border-radius: @Border_Middle;
  }

  &.Big {
    width: 600px;
    height: 200px;
    border-radius: @Border_Big;
  }
}

// Header
.HeaderDiv {
  display: flex;
  height: v-bind(header_height);
  width: 100%;
  padding-bottom: 5px;
  background: white;
  align-items: center;

  .CardDiv.Small &{
    border-top-left-radius: @Border_Small 75%;
    border-top-right-radius: @Border_Small 75%;
  }

  .CardDiv.Middle &{
    border-top-left-radius: @Border_Middle 35%;
    border-top-right-radius: @Border_Middle 35%;
  }

  .CardDiv.Big &{
    border-top-left-radius: @Border_Big 55% ;
    border-top-right-radius: @Border_Big 55%;
  }

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