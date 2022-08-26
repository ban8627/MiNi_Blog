<template>
  <div class="list-wrap">
    <ul>
      <!-- v-for  in  :key  -->
      <li v-for="(item,index) in memoItemArr" :key="index" class="shadow">
        <i class="fas fa-check check-bt" @click="updateMemo(item)" :class="{memoComplete:item.complete}"></i>
        <span :class="{memoCompleteTxt:item.complete}">{{item.memotitle}}</span>
        <span class="remove-bt" @click="removeMemo(item.id, index)">
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
          // 배열에 요소를 밀어넣는다
          // 키값도 필요하지만 실제 내용 (값)이 필요하다.
          // 추후 DB 연동 예정
          let obj = localStorage.getItem(localStorage.key(i));
          
          memoItemArr.push(JSON.parse(obj));
        }
        // 키값을 이용해서 정렬하기
        memoItemArr.sort();
      }

      const removeMemo = (item,index)=> {
        // localStorage 에서  key 를 통해서 지운다.
        localStorage.removeItem(item);
        // 배열 (memoItemArr) 에서 지운다.
        memoItemArr.splice(index, 1);
      };

      const updateMemo = (item)=>{
        // localStorage 에서는 update 메소드를 지원하지 않음.
        // 찾아서 지운다.
        localStorage.removeItem(item.id);
        // 사항 변경한다.
        item.complete = !item.complete;
        // 다시 set한다.
        localStorage.setItem(item.id,JSON.stringify(item))
        
      }
      return {
        memoItemArr,
        removeMemo,
        updateMemo
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
  padding:20px 15px;
  margin-right:5px;
  margin-bottom:30px;
  text-align: left;
  white-space: nowrap;
  border-radius: 8px;
  background-color: #fff;
  transition: all .5s;
}
.remove-bt {
  cursor: pointer;
  float:right;
  margin-right:5px;
  color:rgba(5, 116, 5, 0.8)
}
.list-wrap ul li:hover {
  background-color: rgba(255, 0, 0, 1);
  color:#fff;
  font-size: 18px;
}

.check-bt {
  margin-right:15px;
  cursor: pointer;
  font-size: 18px;
  color:rgba(5, 116, 5, 0.8)
}

.list-wrap ul li:hover .remove-bt,.list-wrap ul li:hover .check-bt {
  color:#fff;
}
.memoComplete {
  color:red;
}
.memoCompleteTxt {
  color:#ddd;
  text-decoration: line-through;
}
</style>