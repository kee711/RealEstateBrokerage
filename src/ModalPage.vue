
<template>
    <div class="black-bg" v-if="modalstatus == true"> <!-- v-if가 참일때만 html 보여줌 -->
        <div class="white-bg">
            <h4>상세페이지</h4>
            <p><img :src="onerooms[modalcontent].image"></p>
            <p>{{onerooms[modalcontent].content}}</p>
            <!-- v-model 또는 @input 사용하여 input받은 값 저장 -->
            <input v-model="month">
            <p>{{month}}개월 가격 : {{onerooms[modalcontent].price * month}}원</p>
            <!-- props는 read-only이기 때문에 custom event 문법으로 부모에게 클릭했을 때 반응해달라고 메세지 전송한 것. -->
            <p @click="$emit('closemodal')">[닫기]</p> 
            

        </div>
    </div>
</template>

<script>
export default {
    name : 'ModalPage',
    data (){
        return {
            month : 1,
        }
    },
    //watcher : 데이터 값 변할때마다 코드 실행
    watch : {
        month(a) {
            if(isNaN(a)){ //isNaN() : 숫자 아니면 true 반환
                alert('숫자만 입력하세요');
                this.month = 1;
            }
            if(a>12){
                alert('최대 입력값은 12입니다');
                this.month = 1;
            }else if(a<0){
                alert('최소 입력값은 1입니다');
                this.month = 1;
            }
        }
    },
    props : {
        onerooms : Array,
        modalstatus : Boolean,
        modalcontent : Number,

    }
}
</script>

<style>

</style>