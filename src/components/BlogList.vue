<template>
  <div class="list-wrap">
    <ul>
        <li v-for="(item, index) in memodata" :key="index" class="shadow"> 
          <i class="fas fa-check-circle check-bt" @click="updateMemo(item)" :class="{memoComplete:item.complete}"></i>
          <span :class="{memoCompleteTxt:item.complete}"> {{item.memotitle}} </span>
          <span class="remove-bt" @click="removeMemo(item.id, index)">
            <i class="fas fa-trash"></i>
          </span>
        </li>  
    </ul>
  </div>
</template>

<script>
export default {  
  props: ['memodata'],
  setup(props, context) {
    const removeMemo = (item, index) => {
      context.emit('removeitem', item, index);
    }
    const updateMemo = (item) => {      
      context.emit("updateitem", item);
    }
    return {            
      removeMemo,
      updateMemo
    }
  }
}
</script>

<style scoped>
  .list-wrap {
    width: 50%;
    margin: 30px auto;
  }

  .list-wrap ul {
    display: flex;
    flex-wrap: wrap;
  }

  .list-wrap ul li {
    position: relative;
    display: block;
    width: calc((100% / 3) - 6px);
    height: 60px;
    border: 1px solid rgba(0, 0, 0, 0.03);
    padding: 20px 15px;
    margin-right: 5px;
    margin-bottom: 30px;
    text-align: left;
    white-space: nowrap;
    border-radius: 8px;
    background-color: #fff;
    transition: all .5s;
  }

  .remove-bt {
    cursor: pointer;
    float: right;
    margin-right: 5px;
    color: rgba(5, 116, 5, 0.8)
  }

  .list-wrap ul li:hover {
    background-color: rgba(255, 0, 0, 1);
    color: #fff;
    font-size: 18px;
  }

  .check-bt {
    margin-right: 15px;
    cursor: pointer;
    font-size: 18px;
    color: rgba(5, 116, 5, 0.8)
  }

  .list-wrap ul li:hover .remove-bt,
  .list-wrap ul li:hover .check-bt {
    color: #fff;
  }

  .memoComplete {
    color: red;
  }

  .memoCompleteTxt {
    color: #ddd;
    text-decoration: line-through;
  }
</style>