<template>
  <div class="main">
    单词:<input type="text" v-model="newWord">
    释义:<input type="text" v-model="newMeaning">
    例句:<input type="text" v-model="newExample">
    <button @click="add()">添加</button>
    <fieldset>
      <h1 align="center">今日单词</h1>
      <div id="today">
        <p v-for="(item,index) in list" :key="index">
          {{`${index+1}、单词:${item.word} 释义:${item.meaning} 例子:${item.example}`}}
          <button @click="remove(index)">已会</button>
          <button @click="unknown(index)">不会</button>
        </p>
      </div>
      <h1 align="center">重新记忆</h1>
       <div id="unknownToday">
         <p v-for="(item,index) in unknownList" :key="index">{{`${index+1}、单词:${item.word} 释义:${item.meaning} 例子:${item.example}`}}</p>
       </div>
      <h1 align="center">今日新增</h1>
        <div id="newAddWord">
          <p v-for="(item,index) in newAddList" :key="index">{{`${index+1}、单词:${item.word} 释义:${item.meaning} 例子:${item.example}`}}</p>
        </div>
    </fieldset>
  </div>
</template>

<style>
p {
  text-align: center;
}
</style>

<script setup>
import {reactive,ref} from 'vue'
const list=reactive([
  {
    word: 'apple',
    meaning: '苹果',
    example: 'I love apple!'
  },
  {
    word: 'pear',
    meaning: '梨子',
    example: 'I love pear!'
  },
  {
    word: 'pineapple',
    meaning: '菠萝',
    example: 'I love pineapple!'
  }
]);
function remove(index) {
  list.splice(index,1);
}
const unknownList=reactive([]);
function unknown(index) {
  unknownList.push({
    word: list[index].word,
    meaning: list[index].meaning,
    example: list[index].example,
  })
  list.splice(index,1)
}
const newAddList=reactive([]);
const newWord=ref(""),newMeaning=ref(""),newExample=ref("");
function add() {
  newAddList.push({
    word: newWord,
    meaning: newMeaning,
    example: newExample,
  })
}
</script>