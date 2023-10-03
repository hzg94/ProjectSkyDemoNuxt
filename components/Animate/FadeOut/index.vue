<template>
  <transition name="fade">
    <slot/>
  </transition>
</template>


<script lang="ts">
import {PropType} from "vue";
import 'animate.css/animate.css'

export enum FadeOutAnimate{
  Out,
  Up,
  Down,
  Right,
  Left,

  TopLeft,
  TopRight,

  BottomRight,
  BottomLeft,
}

export default {
  name: "fadeOut",
  props: {
    animation_duration: {
      type: String,
      default: "0.4s"
    },
    animation_type: {
      type: Number as PropType<FadeOutAnimate>,
      default: FadeOutAnimate.Out
    }
  },
  setup(props:any){
    let animation_fade_type = 'fadeOut'
    switch (props.animation_type){
      case FadeOutAnimate.Out:{
        animation_fade_type = 'fadeOut'
        break;
      }

      case FadeOutAnimate.Up:{
        animation_fade_type = 'fadeOutUp'
        break;
      }
      case FadeOutAnimate.Down:{
        animation_fade_type = 'fadeOutDown'
        break;
      }
      case FadeOutAnimate.Right:{
        animation_fade_type = 'fadeOutRight'
        break;
      }
      case FadeOutAnimate.Left:{
        animation_fade_type = 'fadeOutLeft'
        break;
      }

      case FadeOutAnimate.TopLeft:{
        animation_fade_type = 'fadeOutTopLeft'
        break;
      }
      case FadeOutAnimate.TopRight:{
        animation_fade_type = 'fadeOutTopRight'
        break;
      }
      case FadeOutAnimate.BottomRight:{
        animation_fade_type = 'fadeOutBottomRight'
        break;
      }case FadeOutAnimate.BottomLeft:{
        animation_fade_type = 'fadeOutBottomLeft'
        break;
      }

      default:{
        console.log("Error Type No Found")
      }
    }
    return {
      animation_fade_type
    }
  }
}



</script>

<style scoped>
.fade-leave-active {
  animation: v-bind(animation_fade_type);
  animation-duration: v-bind(animation_duration);
}
</style>