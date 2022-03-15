<template>
  <div v-for="(a, i) in onerooms" :key="i">
    <img :src="a.image">
    <h4 @click="$emit('openmodal', i)">{{a.title}}</h4> <!-- 원룸 (a, i) 중 a는 반복문 돌면서 값이 담김 -->
    <p>{{a.price}} 만원</p> <!-- (a, i) 중 i는 반복문 돌면서 index가 담김 -->
    <button v-on:click="increase(i)">허위매물신고</button> <span>신고수 : {{reports[i]}}</span>
  </div>
</template>

<script>
export default {
    name : 'ItemList',
    props : {
        onerooms : Array,
        reports : Array,
    }
}
</script>

<style>

</style>