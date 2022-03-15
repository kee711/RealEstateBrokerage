<template>

  <div class="menu">
    <a v-for="작명 in menus" :key="작명">{{작명}}</a>
  </div>

  <!-- 컴포넌트 사용 -->
  <DiscountBanner/> 

  <button @click="priceSort()">가격순 정렬</button> <button @click="originalSort()">원래대로 정렬</button>

  <ModalPage @closemodal='modalstatus = false' v-bind:onerooms="onerooms" :modalstatus="modalstatus" :modalcontent="modalcontent"/>
  <ItemList @openmodal='modalstatus = true; modalcontent = $event' v-bind:onerooms="onerooms" :reports="reports"/>

</template>

<script>

import data from './assets/data.js'
import DiscountBanner from './DiscountBanner.vue'
import ItemList from './ItemList.vue'
import ModalPage from './ModalPage.vue'

export default {
  name: 'App',  
  data(){  //eocp
    return { //이 데이터 저장공간을 react에서는 state라고 함. 데이터/상태를 저장한다는 뜻
      oneroomsOriginal : [...data],
      onerooms : data,
      modalstatus : false, //false는 닫힘, true는 열림 (UI의 현재 상태 저장)
      modalcontent : 0,
      menus : ['Home', 'Shop', 'About'],
      reports : [0, 0, 0]
    }
  },
  methods : {
    increase(i){
      this.reports[i]++;
    },
    priceSort(){
      this.onerooms.sort(function(a,b){
        return a.price - b.price
      });
    },
    originalSort(){
      // this.onerooms = this.oneroomsOriginal; 는 안됨. = 는 좌우 값을 서로 공유해달라는 뜻이기 때문
      this.onerooms = [...this.oneroomsOriginal];
    }
  },
  components : {
    DiscountBanner : DiscountBanner, // 좌우 항목 같은경우 한해서 DiscountBanner, 만 써도 가능. 
    ItemList : ItemList,
    ModalPage : ModalPage,
  }
}
</script>

<style>

body {
  margin: 0;
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}

img {
  width: 50%;
  margin-top: 40px;
}

.discount{
  background: #eee;
  margin: 10px;
  padding: 10px;
  border-radius: 5px;
}
</style>

