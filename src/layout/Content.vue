<template>
  <div class="warp">
    <div class="tab-bar"></div>
    <div class="left-side"></div>
    <div class="main-content">
      <MainContent  />
    </div>
    <div class="right-side"></div>
  </div>
</template>

<script setup lang="ts">
  import MainContent from '@/components/MainContent.vue';
</script>

<style scoped lang="less">
  .warp {
    display: grid;
    grid-template-areas:
      'tab-bar tab-bar tab-bar'
      'left-side main-content right-side';
    grid-template-rows: 100px 1fr;
    grid-template-columns: 280px 1fr 280px;
    .tab-bar {
      grid-area: tab-bar;
      background-color: #83e82dbb;
    }
    .left-side {
      grid-area: left-side;
      background-color: #2bd5a2ba;
    }
    .main-content {
      grid-area: main-content;
      background-color: #932d2cc6;
    }
    .right-side {
      grid-area: right-side;
      background-color: #7f48b4c5;
    }
  }
</style>
