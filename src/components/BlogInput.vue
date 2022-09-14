<template>
  <div class="input-wrap shadow">
    <div class="input-inner">
      <input type="text" v-model="newItem" class="input-box" maxlength="30" @keyup.enter="addItem" placeholder="내용 넣어야지?">
  
      <div class="option">
        <span @click="addIcon(0)" class="img1">
          이미지1
        </span>
        <span @click="addIcon(1)" class="img2">
          이미지2
        </span>
        <span @click="addIcon(2)" class="img3">
          이미지2
        </span>
  
        <span @click="addItem" class="add-bt">
          <i class="fas fa-plus add-bt-icon"></i>
        </span>
      </div>
    </div>
    <!-- 안내창 -->
    <ModalVue :show="showModal" @closemodal="showModal=false">
      <template #header>
        <h3>안내창</h3>
      </template>
      <template #body>
        <h2>내용을 작성하여 주세요.</h2>
      </template>
    </ModalVue>
  </div>
</template>

<script>
  import {
    ref
  } from 'vue';
  import {
    useStore
  } from 'vuex';
  import ModalVue from '@/components/common/ModalVue.vue';
  export default {
    components: {
      ModalVue
    },
    setup() {
      const store = useStore();
      const newItem = ref('');
      const newIcon = ref(0);
      const showModal = ref(false);

      const addItem = () => {
        let temp = newItem.value;
        let icon = newIcon.value;
        // 앞쪽 뒷쪽 공백 제거
        temp = temp.trim();
        // 추후 업데이트 예정(정규표현식-문자열체크 문법)
        //  앞자리공백   공백    뒷자리공백
        if (temp !== '') {
          // context.emit("additem", temp, icon);
          // store.commit('ADD_MEMO',{item:temp,index:icon})
          store.dispatch('fetchAddMemo',{item:temp,index:icon})
          resetItem();
        } else {
          showModal.value = true;
        }
      }

      // 내용 재설정
      const resetItem = () => {
        newItem.value = '';
      }

      const addIcon = (index) => {
        newIcon.value = index;
      }

      return {
        newItem,
        addItem,
        addIcon,
        showModal
      }
    }
  }
</script>

<style scoped>
  .input-wrap {
    position: relative;
    display: block;
    width:80%;
    height: 60px;
    line-height: 58px;
    border-radius: 15px;
    background-color: rgb(0, 0, 0);
    overflow: hidden;
    margin: 20px auto;
    color:#fff;
  }
  .input-inner {
    position: relative;
    width:100%;
    margin:0 auto;
    border:1px solid #fff;
    border-radius: 15px;
  }
  .input-wrap input {
    border-style: none;
    color:#fff;
    background-color: #000;
    padding:0 30px;
  }
  .input-wrap input::placeholder {
    color:rgb(174, 174, 174);
  }
  .input-wrap input:focus {
    outline: none;
  }

  .input-box {
    width: calc(93% - 250px);
    font-size: 16px;
    margin-left: 20px;
  }

  .option {
    position: absolute;
    display: block;
    right: 0;
    top: 0;
  }

  .img1:active,
  .img2:active,
  .img3:active {
    outline: 3px solid #fff;
  }

  .img1 {
    display: inline-block;
    width: 40px;
    height: 40px;
    font-size: 0;
    cursor: pointer;
    background: url('@/assets/images/dog1.png') no-repeat center;
    background-size: cover;
  }

  .img2 {
    display: inline-block;
    width: 40px;
    height: 40px;
    font-size: 0;
    cursor: pointer;
    background: url('@/assets/images/dog2.png') no-repeat center;
    background-size: cover;
  }

  .img3 {
    display: inline-block;
    width: 40px;
    height: 40px;
    font-size: 0;
    cursor: pointer;
    background: url('@/assets/images/str.png') no-repeat center;
    background-size: cover;
  }

  .add-bt {
    display: inline-block;
    background-color: #fff;
    cursor: pointer;
    border-radius: 0 15px 15px 0;
  }

  .add-bt-icon {
    display: inline-block;
    vertical-align: middle;
    color: #000;
    margin: 0 20px;
  }
</style>