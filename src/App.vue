<script setup>
import { ref, reactive } from 'vue'
const calculatorValue = ref('');
const calculatorElements = ['C', '*', '/', '-', 7, 8, 9, '+', 4, 5, 6, '%', 1, 2, 3, '=', 0, '.'];
const operator = ref(null);
let previousCalculatorValue = ref('');

const action = (item) => {
  /* Clear */
  if (item === 'C') {
    calculatorValue.value = '';
    return
  }

  /* Number input */
  if (!isNaN(item) || item === '.') {
    if (calculatorValue.value.includes('.') && item === '.') {
      return
    }
    calculatorValue.value += item;
    return
  }

  /* Percentage */
  if (item === "%") {
    calculatorValue.value /= 100;
  }

  if (['/', '*', '-', "+"].includes(item)) {
    if (previousCalculatorValue.value && operator.value) {
      calculatorValue.value = String(eval(previousCalculatorValue.value + operator.value + calculatorValue.value));
      previousCalculatorValue.value = calculatorValue.value;
    } else {
      previousCalculatorValue.value = calculatorValue.value;
    }
    calculatorValue.value = '';
    operator.value = item;
  }

  if (item === '=') {
    calculatorValue.value = String(eval(
      previousCalculatorValue.value + operator.value + calculatorValue.value
    ));

    previousCalculatorValue.value = '';
    operator.value = null;
  }

}

</script>

<template>
  <div class="calc-container">
    <div class="output">
      {{ calculatorValue || 0 }}
    </div>
    <div class="buttons">
      <table class="styled-table">
        <tbody>
          <tr>
            <td @click="action(calculatorElements[0])" class="operation">{{ calculatorElements[0] }}</td>
            <td @click="action(calculatorElements[1])" class="operation">{{ calculatorElements[1] }}</td>
            <td @click="action(calculatorElements[2])" class="operation">{{ calculatorElements[2] }}</td>
            <td @click="action(calculatorElements[3])" class="operation">{{ calculatorElements[3] }}</td>
          </tr>
          <tr>
            <td @click="action(calculatorElements[4])">{{ calculatorElements[4] }}</td>
            <td @click="action(calculatorElements[5])">{{ calculatorElements[5] }}</td>
            <td @click="action(calculatorElements[6])">{{ calculatorElements[6] }}</td>
            <td @click="action(calculatorElements[7])" class="operation">{{ calculatorElements[7] }}</td>
          </tr>
          <tr>
            <td @click="action(calculatorElements[8])">{{ calculatorElements[8] }}</td>
            <td @click="action(calculatorElements[9])">{{ calculatorElements[9] }}</td>
            <td @click="action(calculatorElements[10])">{{ calculatorElements[10] }}</td>
            <td @click="action(calculatorElements[11])" class="operation">{{ calculatorElements[11] }}</td>
          </tr>
          <tr>
            <td @click="action(calculatorElements[12])">{{ calculatorElements[12] }}</td>
            <td @click="action(calculatorElements[13])">{{ calculatorElements[13] }}</td>
            <td @click="action(calculatorElements[14])">{{ calculatorElements[14] }}</td>
            <td @click="action(calculatorElements[15])" class="operation">{{ calculatorElements[15] }}</td>
          </tr>
          <tr>
            <td @click="action(calculatorElements[16])" colspan="2">{{ calculatorElements[16] }}</td>
            <td @click="action(calculatorElements[17])">{{ calculatorElements[17] }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.calc-container {
  background-color: #234;
  border-radius: 8px;
  width: 400px;
  height: 400px;
  margin: 50px auto;
  padding: 20px;
}

.output {
  border-radius: 16px;
  background-color: #31475e;
  width: 360px;
  height: 50px;
  padding: 10px;
  margin-bottom: 16px;
  display: flex;
  align-items: center;
  justify-content: end;
  font-size: large;
}

.buttons {
  border-radius: 16px;
  background-color: #3c5c7e;
  width: 360px;
  height: 298px;
  margin-bottom: 16px;
  display: flex;
  align-items: center;
  border: 1px solid rgb(48, 52, 84);
}

.operation {
  background-color: #3fb984;
}

.styled-table {
  border-collapse: collapse;
  font-family: sans-serif;
  width: inherit;
  height: inherit;
}

.styled-table td {
  padding: 12px 15px;
  text-align: center;
  font-size: medium;
  border: 1px solid rgb(48, 52, 84);
  cursor: pointer;
}

.styled-table td:hover {
  opacity: 45%;
}
</style>
