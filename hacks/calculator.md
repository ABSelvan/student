---
title: JS Calculator
comments: true
hide: true
layout: base
description: A common way to become familiar with a language is to build a calculator.  This calculator shows off button with actions.
permalink: /calculator
---

<!-- Calculator with Square Function -->

<style>
  .calculator-output {
    grid-column: span 4;
    grid-row: span 1;
    border-radius: 10px;
    padding: 0.25em;
    font-size: 20px;
    border: 5px solid black;
    display: flex;
    justify-content: flex-end; /* Right justify result (Hack 0) */
    align-items: center;
  }
  canvas {
    filter: none;
  }
</style>

<div id="animation">
  <div class="calculator-container">
      <!-- result -->
      <div class="calculator-output" id="output">0</div>
      
      <!-- row 1 -->
      <div class="calculator-number">1</div>
      <div class="calculator-number">2</div>
      <div class="calculator-number">3</div>
      <div class="calculator-operation">+</div>
      
      <!-- row 2 -->
      <div class="calculator-number">4</div>
      <div class="calculator-number">5</div>
      <div class="calculator-number">6</div>
      <div class="calculator-operation">-</div>
      
      <!-- row 3 -->
      <div class="calculator-number">7</div>
      <div class="calculator-number">8</div>
      <div class="calculator-number">9</div>
      <div class="calculator-operation">*</div>
      
      <!-- row 4 -->
      <div class="calculator-clear">A/C</div>
      <div class="calculator-number">0</div>
      <div class="calculator-number">.</div>
      <div class="calculator-equals">=</div>

      <!-- row 5 (new: square) -->
      <div class="calculator-operation">/</div>
      <div class="calculator-operation">x²</div>
  </div>
</div>

<script>
var firstNumber = null;
var operator = null;
var nextReady = true;

const output = document.getElementById("output");
const numbers = document.querySelectorAll(".calculator-number");
const operations = document.querySelectorAll(".calculator-operation");
const clear = document.querySelectorAll(".calculator-clear");
const equals = document.querySelectorAll(".calculator-equals");

// Number buttons listener
numbers.forEach(button => {
  button.addEventListener("click", () => number(button.textContent));
});

function number(value) {
  if (value !== ".") {
    if (nextReady) {
      output.innerHTML = value;
      if (value !== "0") nextReady = false;
    } else {
      output.innerHTML += value;
    }
  } else {
    if (output.innerHTML.indexOf(".") === -1) {
      output.innerHTML += value;
      nextReady = false;
    }
  }
}

// Operation buttons listener
operations.forEach(button => {
  button.addEventListener("click", () => operation(button.textContent));
});

function operation(choice) {
  if (choice === "x²") {   // Square operation (Hack 3 extended)
    let num = parseFloat(output.innerHTML);
    output.innerHTML = (num * num).toString();
    firstNumber = null;
    nextReady = true;
    return;
  }

  if (firstNumber === null) {
    firstNumber = parseFloat(output.innerHTML);
    nextReady = true;
    operator = choice;
    return;
  }
  firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
  operator = choice;
  output.innerHTML = firstNumber.toString();
  nextReady = true;
}

function calculate(first, second) {
  switch (operator) {
    case "+": return first + second;
    case "-": return first - second;
    case "*": return first * second;
    case "/": return second !== 0 ? first / second : "Error";
    default: return first;
  }
}

equals.forEach(button => {
  button.addEventListener("click", () => equal());
});

function equal() {
  firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
  output.innerHTML = firstNumber.toString();
  nextReady = true;
}

clear.forEach(button => {
  button.addEventListener("click", () => clearCalc());
});

function clearCalc() {
  firstNumber = null;
  operator = null;
  output.innerHTML = "0";
  nextReady = true;
}
</script>

