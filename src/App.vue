<script setup>
// Imports
import {ref} from "vue"
import {evaluate} from 'mathjs'
import { toNumber } from "@vue/shared";
const calculation = ref("")
const result = ref(0)
const lastCalc = ref(false)
const noCalc = ref(true)


/* addCharacter adds the character to the calculation string whilst also checking that it can be evaluated later on. 
   It will not allow the user to enter something invalid.
*/

let addCharacter = (character) => {
  let lastCharacter = calculation.value.slice(-1)

  if(noCalc.value == true) {
    if(typeof toNumber(character) == 'number') {
      
    }
  }

  if(calculation.value.length < 35) {
    if(typeof toNumber(character) != 'number') {
    lastCalc.value = false
    if(typeof toNumber(lastCharacter) == 'number') {
      calculation.value = calculation.value + character
    }
  } else if(typeof toNumber(character) == 'number') {
    if(lastCalc.value == false) {
      calculation.value = calculation.value + character
    }
  }
  }


}

function clearAll() {
  calculation.value = ""
  result.value = 0
  lastCalc.value = false
}

function clearLastEntry() {
  calculation.value = calculation.value.slice(0, -1)
}

function calculate() {
  // If last character is NOT a number then it removes it to allow it to calculate without error.
  const lastNumber = calculation.value.slice(-1)
  if(typeof toNumber(lastNumber) != 'number') {
    calculation.value = calculation.value.slice(0, -1)
    result.value = evaluate(calculation.value).toFixed(2)
    calculation.value = result.value
    lastCalc.value = true
  } else {
    result.value = evaluate(calculation.value).toFixed(2)
    calculation.value = result.value
    lastCalc.value = true
  }


}


</script>

<template>
  <main>
    <div class="calculator">
      <div class="display">
        <h4>{{ calculation }}</h4>
        <h2>{{ result }}</h2>
      </div>
      <div class="buttons">
        <button @click="addCharacter('%')" class="gray">%</button>
        <button @click="clearLastEntry" class="gray">CE</button>
        <button @click="clearAll" class="gray">AC</button>
        <button @click="addCharacter('/')" class="gray">/</button>
        <button @click="addCharacter('7')">7</button>
        <button @click="addCharacter('8')">8</button>
        <button @click="addCharacter('9')">9</button>
        <button @click="addCharacter('*')" class="gray">X</button>
        <button @click="addCharacter('4')">4</button>
        <button @click="addCharacter('5')">5</button>
        <button @click="addCharacter('6')">6</button>
        <button @click="addCharacter('-')" class="gray">-</button>
        <button @click="addCharacter('1')">1</button>
        <button @click="addCharacter('2')">2</button>
        <button @click="addCharacter('3')">3</button>
        <button @click="addCharacter('+')" class="gray">+</button>
        <button>&nbsp</button>
        <button @click="addCharacter('0')">0</button>
        <button @click="addCharacter('.')">.</button>
        <button @click="calculate" class="purple">=</button>
      </div>
    </div>

  </main>
</template>

<style>
main {
  display: flex;
  height: 100vh;
  width: 100vw;
  background-color: #222222;
  justify-content: center;
  align-items: center;
}

.calculator {
  background-color: #313131;
  height: 500px;
  width: 280px;
  border-radius: 24px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
}

.display {
  background-color: #313131;
  display: flex;
  flex-direction: column;
  border-radius: 24px 24px 0px 0px;
  height: 160px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  justify-content: center;
  align-items: center;
  
}

h2 {
  color: white;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  font-weight: bold;
  font-size: 32px;

}

h4 {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  color: #a161f7;
  font-weight: bold;
  font-size: 12px;
  margin-bottom: -10px;
}

.buttons {
  display: flexbox;
  justify-content: center;
  align-items: center;
  margin-left: 2px;
  margin-right: 2px;
  text-align: center;
}

button {
  background-color: #2f2f2f;
  border: 0px;
  height: 51px;
  width: 51px;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  color: white;
  border-radius: 16px;
  font-size: 18px;
  font-weight: bold;
  margin: 8px;
  cursor: pointer;
}

button:hover {
  background-color: #252525;
}

button:active {
  box-shadow: inset 0 0 10px #1f1f1f;
}

.gray {
  color: gray;
  font-weight: normal;
}

.purple {
  background-color: #a161f7;
}

.purple:hover {
  background-color: #9456e5;
}

.purple:active {
  box-shadow: inset 0 0 10px #2e174b;
}
</style>