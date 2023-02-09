<template>
  <div class="board">
    <div v-for="(row, index) in board" class="gameRow">{{ row.letter }}</div>
  </div>
  <div class="result">
    <div v-for="row in dictionaryData" class="board">
      <div v-for="letter in row" class="gameRow">{{ letter }}</div>
    </div>
  </div>
  <keyboard @key="keyUp"></keyboard>
</template>

<script lang="ts" setup>
import {ref} from 'vue';
import {englishWords} from "./englishWords";

const board = ref(Array.from({length: 5}, () => ({
  letter: '',
})));
const dictionaryData = ref([]);
const keyUp = (key: string) => {
  if (/^[a-zA-Z]$/.test(key) || key === '?') {
    for (const letter of board.value) {
      if (!letter.letter) {
        letter.letter = key.toUpperCase();
        break
      }
    }
  } else if (key === 'BackSpace') {
    for (const letter of [...board.value].reverse()) {
      if (letter.letter) {
        letter.letter = ''
        break
      }
    }
  } else if (key === 'Enter') {
    searchDictionary();
  }
}

const searchDictionary = () => {
  const combinedString = board.value.map(letter => {
    if (letter.letter === '?') {
      return '.'
    }
    return letter.letter
  }).join('')
  const regex = new RegExp('^' + combinedString + '$', 'gmi')
  const matchedWord = englishWords.match(regex)
  if (!matchedWord) {
    for (const letter of board.value) {
      letter.letter = ''
    }
    ElMessage({message: 'No Word Matches', type: 'error', duration: 1000})
  } else {
    dictionaryData.value = matchedWord;
  }
}
</script>

<style>
.board {
  display: flex;
  justify-content: space-around;
  margin: 20px auto;
}

.result {
  max-height: 400px;
  overflow-x: hidden;
  overflow-y: scroll;
}

.result .board .gameRow {
  border-color: #6aaa64;
  background-color: #6aaa64;
  text-transform: uppercase;
  color: white;
}

.result::-webkit-scrollbar {
  display: none;
}

.gameRow {
  display: flex;
  height: 80px;
  width: 80px;
  border-style: solid;
  border-color: gray;
  justify-content: center;
  align-items: center;
  font-size: 2rem;
  font-weight: 700;
}

body {
  font-family: 'Clear Sans', 'Helvetica Neue', Arial, sans-serif;
  text-align: center;
  max-width: 500px;
  margin: 20px auto;
}
</style>