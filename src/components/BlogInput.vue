<template>
  <div class="input-wrap shadow">
    <input type="text" v-model="newItem" maxlength="70" @keyup.enter="addItem">
    <span @click="addItem" class="add-bt">
      <i class="fas fa-plus add-bt-icon"></i>
    </span>
  </div>
</template>

<script>
  import {
    ref
  } from 'vue';
  export default {
    setup() {
      const newItem = ref('');
      // 현재 시간값을 계산해서 중복이 되지 않는 값을 처리한다.
      // key 와 id 를 생성해 주기 위해서 처리
      // 10보다 작은 값에 0을 붙임
      const addZero = (n) => {
      return n < 10 ? '0' + n : n;
      }
      // 현재 시간을 리턴
      const getCurrentDate = () => {
      let date = new Date();
      return date.getFullYear().toString() + addZero(date.getMonth() + 1) + addZero(date.getDate()) +
        addZero(date.getHours()) + addZero(date.getMinutes()) + addZero(date.getSeconds());              
      }

      const addItem = () => {
        let temp = newItem.value;
        // 앞 뒤 공백 제거
        temp = temp.trim();
        // 추후 업데이트 예정(정규표현식 - 문자열체크 문법)
        // 앞자리 공백 공백 뒷자리 공백
        if (temp !== '') {
        // json 저장 문자열 Json.stringify(오브젝트)
        // { completed:false,  title:제목이지?, 등:등 }
        let memoTemp = {
          id:getCurrentDate(),
          memotitle:newItem.value,
          memocate:'memo[info]',
          memolink:'http://naver.com',
          memoicon:'icon.png',
          memopic:'a.jpg',
          complete:false,
          memodate:new Date(),
        }
        // 추후 실제 DB 연동 예정
          localStorage.setItem(memoTemp.id, JSON.stringify(memoTemp));
          resetItem();
        }else {
        alert('내용 입력해야지?')
        }
        // localStorage.setItem(키,값)
        // 추후 json 형태로 만들어서 저장

        // localStorage.setItem(키, json 문자열로 저장)
        

      } 
      // 내용 재설정
      const resetItem = () => {
        newItem.value = '';
      }
      return {
        newItem,
        addItem
      }
    }
  }
</script>

<style scoped>
  .input-wrap {
    position: relative;
    display: block;
    margin:0 auto;
    width:50%;
    padding:8px 20px;
    line-height:50px;
    overflow: hidden;
    border:1px solid rgba(0, 0, 0, 0.05);
    border-radius: 5px;
    background-color: #fff;
  }
  .input-wrap input {
    border:1px solid rgba(0, 0, 0, 0.09);
    width:90%;
    height:46px;
    border-radius: 5px;
  }
  .input-wrap input:focus {
    outline: none;
  }
  .input-wrap .add-bt {
    display: block;
    width:46px;
    height:46px;
    text-align: center;
    background-color: green;
    float:right;
    cursor: pointer;
    border-radius: 5px;
  }
  .input-wrap .add-bt-icon {
    display: inline-block;
    vertical-align: middle;
    font-size: 20px;
    color:#fff;
  }
</style>