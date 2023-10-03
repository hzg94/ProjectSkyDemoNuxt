<template>

  <div class="BackGround">
    <div class="CardDiv">
      <CardUserCard user_name="admin"/>
      <CardMusicCard/>

      <CardTimeCard/>
      <CardPlanCard/>

      <CardMusicManagerCard/>
      <CardLinkCard/>
    </div>
  </div>
</template>

<script lang="ts" setup>




</script>

<style lang="less" scoped>
.BackGround {
  width: 100vw;

  min-height: 100vh;

  height: 100%;

  display: flex;
  flex-wrap: wrap;

  justify-content: center;
  align-content: center;

  background-image: url("../assets/restaurant.webp");
  background-repeat: repeat;
}

.CardDiv {
  display: inline-flex;
  flex-wrap: wrap;
  margin: 0 auto;
  width: 80%;
  justify-content: center;



  & > * {
    margin: 5px 10px;
  }
}
</style>