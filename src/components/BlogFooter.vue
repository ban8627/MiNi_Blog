<template>
 
  <div class="clear-all-wrap">
    <span class="clear-all-bt" @click="clearAllMemo">Clear All</span>
    <span class="copy">Copyright 2022 by Hon Guil Dong</span>
  </div>
</template>

<script>
export default {
  setup(props, context) {
    const clearAllMemo = () => {
      context.emit('deleteitem')
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
    padding:15px 0;
    border-radius: 5px;
  }

  .clear-all-bt {
    display: block;
    width:80%;
    max-width:150px;
    height:50px;
    cursor: pointer;
    color:#fff;
    background-color: #f00;
    border-radius: 5px;
    margin:10px auto;
  }

  .copy {
    display: inline-block;
    font-size: 9px;
    white-space:nowrap;
  }
</style>