<template>
    <div id="keyBoard">
        <div class="row" v-for="(row, index) in rows">
            <div class="spacer" v-if="index === 1"></div>
            <button v-for="key in row" :class="[key.length > 1 && 'big',key === '?' && 'color']">
                <span v-if="key !== 'BackSpace'">{{ key }}</span>
                <svg v-else xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                    class="bi bi-backspace" viewBox="0 0 16 16">
                    <path
                        d="M5.83 5.146a.5.5 0 0 0 0 .708L7.975 8l-2.147 2.146a.5.5 0 0 0 .707.708l2.147-2.147 2.146 2.147a.5.5 0 0 0 .707-.708L9.39 8l2.146-2.146a.5.5 0 0 0-.707-.708L8.683 7.293 6.536 5.146a.5.5 0 0 0-.707 0z" />
                    <path
                        d="M13.683 1a2 2 0 0 1 2 2v10a2 2 0 0 1-2 2h-7.08a2 2 0 0 1-1.519-.698L.241 8.65a1 1 0 0 1 0-1.302L5.084 1.7A2 2 0 0 1 6.603 1h7.08zm-7.08 1a1 1 0 0 0-.76.35L1 8l4.844 5.65a1 1 0 0 0 .759.35h7.08a1 1 0 0 0 1-1V3a1 1 0 0 0-1-1h-7.08z" />
                </svg>
            </button>
            <div class="spacer" v-if="index === 1"></div>
        </div>
        </div>
    
</template>

<script lang="ts" setup>
const rows = [
    [...'qwertyuiop'.split('')],
    [...'asdfghjkl'.split(''),'?'],
    ['Enter',...'zxcvbnm'.split(''), 'BackSpace']
]
</script>

<style scoped>
#keyBoard {
    margin: 30px 8px 0;
    user-select: none;
}

button {
    font-family: inherit;
  font-weight: bold;
  border: 0;
  padding: 0;
  margin: 0 6px 0 0;
  height: 50px;
  border-radius: 4px;
  cursor: pointer;
  user-select: none;
  background-color: #d3d6da;
  color: #1a1a1b;
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
  -webkit-tap-highlight-color: rgba(0, 0, 0, 0.3);
  transition: all 0.2s 1.5s;
}

.spacer {
    flex: .5;
}
button:last-of-type {
  margin: 0;
}

.row {
    display: flex;
    width: 100%;
    margin: 0 auto 8px;
     touch-action: manipulation;
}
button.big{
    flex: 1.5;
}
button.color{
    background-color: #ffc107;
}
</style>