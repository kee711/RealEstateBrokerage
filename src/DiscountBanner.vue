<template>
  <div class="discount">
      <h4>오늘 결제하면 {{discountPer}}% 할인!</h4>
  </div>
</template>

<script>
export default {
    name : 'DiscountBanner', //컴포넌트 이름은 두글자 이상
    data(){
      return {
        discountPer : 3,
      }
    },
    methods : {
      async decrease() {  //ㄷㄷㄷ clearInterval 작동 안돼서 블로그보고 function을 async로 바꾸니까 됨...
        if(this.discountPer < 1){
          alert('할인 끝! 그러게 일찍 사지 그랬어요...');
          clearInterval(this.timerId);
        }
        else{
          this.discountPer--;
        }
      }
    },
    mounted(){
      this.timerId = setInterval(this.decrease, 1000);
      
      
      
    }
}
</script>

<style>

</style>