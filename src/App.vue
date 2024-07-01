<script setup>
import axios from 'axios';
import { onMounted, ref } from 'vue';

// import HelloWorld from './components/HelloWorld.vue'

const minNum=1
const maxNum=100
const postNum = ref([])
const postBody = ref ([])
const apiURL = 'https://jsonplaceholder.typicode.com/posts/'
let currentPostNum = '';
let randomPostNumber = ''

function getRandomPost(){
  randomPostNumber = Math.floor(Math.random()*(maxNum-minNum+1))+minNum
  currentPostNum=randomPostNumber
  // console.log(currentPostNum)
  getData()
};

function getPlusNumPost (){
  currentPostNum=++currentPostNum
  getData()
}

function getMinusNumPost(){
  currentPostNum=--currentPostNum
  getData()
}

function getData(){
  axios
  .get(apiURL+currentPostNum,{
    headers:{'Content-Type':'application/json'}
  })
  .then((response) => {
    postBody.value = response.data.body
    postNum.value = response.data.id
    // console.log(response.data)
    
  })
  
};



onMounted(()=>getRandomPost())

  
</script>

<template>
  <div>
    <div class="postNum">POST NUMBER {{ postNum }}</div>
    <div class="response"><h4 class="HREsponse"> {{ postBody }}</h4>
      <div class="BTNbar">
        <button class="prevBTN" @click="getMinusNumPost()"><</button>
        <button class="randomBTN" @click="getRandomPost()">RANDOM</button>
        <button class="nextBTN" @click="getPlusNumPost()">></button>
      </div>
    </div>
  </div>
  
  <!-- <HelloWorld msg="Vite + Vue" /> -->
</template>

<style scoped>
.HREsponse{
  color: black;
  /* height: 20px;
  width: 500px; */
}
.response{
  width: 500px;
  height: 500px;
  margin: 0 auto;
  background-color: aquamarine;
}
button{
  margin: 15px;
  color: black;
  background-color: blanchedalmond;
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
