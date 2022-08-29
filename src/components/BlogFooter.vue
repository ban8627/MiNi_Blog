<template>
  <div class="clear-all-wrap">
    <span class="clear-all-bt" @click="clearAllMemo">Celar All</span>
    <span class="copy">Copyright 2022 by JS Ryu</span>
  </div>
</template>

<script>
  export default {
    setup() {
      const clearAllMemo = () => {
        // localStorage 에서 내용 전체 삭제
        // 추후 DB 연동 예정
        localStorage.clear();
      }
      return {
        clearAllMemo
      }
    }
  }
</script>

<style>
  .clear-all-wrap {
    position: relative;
    display: block;
    width:100%;
    /* height: 50px; */
    line-height:50px;
    background-color: #fff;
    text-align: center;
    margin:0 auto;
    border-radius: 5px;
  }

  .clear-all-bt {
    display: inline-block;
    width:80%;
    height:50px;
    cursor: pointer;
    border:1px solid #f00;
    border-radius: 5px;
    margin:10px;
  }

  .copy {
    display: inline-block;
    font-size: 9px;
    white-space:nowrap;
  }
</style>