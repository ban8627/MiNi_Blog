<template>
  <div class="list-wrap">
    <ul>
      <!-- v-for  in  :key  -->
      <li v-for="(obj,index) in memoItemArr" :key="index" class="shadow">
        {{obj}}
        <span class="remove-bt" @click="removeMemo(obj, index)">
          <i class="fas fa-trash"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
import {ref,reactive} from 'vue';
  export default {
    setup() {
      // localStorage 의 목록을 가지고 오기
      const total = ref(0);
      total.value = localStorage.length;
      const memoItemArr = reactive([]);
      if(total.value > 0){
        for(let i = 0; i < total.value; i++){
          memoItemArr.push(localStorage.key(i));
        }
      }

      const removeMemo = (obj,index)=> {
        // localStorage 에서  key 를 통해서 지운다.
        localStorage.removeItem(obj);
        // 배열 (memoItemArr) 에서 지운다.
        memoItemArr.splice(index, 1);
      };
      return {
        memoItemArr,
        removeMemo
      }
    }
  }
</script>

<style scoped>
.list-wrap {
  width:50%;
  margin:30px auto;
}
.list-wrap ul {
  display: flex;
  flex-wrap: wrap;
}
.list-wrap ul li {
  position: relative;
  display: block;
  width:calc((100% / 3) - 6px);
  height:60px;
  border:1px solid rgba(0, 0, 0, 0.03);
  padding:20px 0;
  margin-right:5px;
  margin-bottom:30px;
  text-align: center;
  white-space: nowrap;
  border-radius: 8px;
  background-color: #fff;
  transition: all .5s;
}
.list-wrap ul li:hover {
  background-color: rgba(255, 0, 0, 1);
  color:#fff;
  font-size: 18px;
}
.remove-bt {
  cursor: pointer;
  float:right;
  margin-right:25px;
  color:green;
}
</style>