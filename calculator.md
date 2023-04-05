<!-- HTML implementation of the calculator. 
    CSS sets 4 buttons (calculator-button) to a row
    All buttons have onclick JavaScript action
    All actions result in calculator-output.innerHTML change
-->
<div class="calculator-container">
    <!--result-->
    <div class="calculator-output" id="output">0</div>
    <!--row 1-->
    <div class="calculator-button" onclick="number('1')">1</div>
    <div class="calculator-button" onclick="number('2')">2</div>
    <div class="calculator-button" onclick="number('3')">3</div>
    <div class="calculator-button" onclick="operation('+')">+</div>
    <!--row 2-->
    <div class="calculator-button" onclick="number('4')">4</div>
    <div class="calculator-button" onclick="number('5')">5</div>
    <div class="calculator-button" onclick="number('6')">6</div>
    <div class="calculator-button" onclick="operation('-')">-</div>
    <!--row 3-->
    <div class="calculator-button" onclick="number('7')">7</div>
    <div class="calculator-button" onclick="number('8')">8</div>
    <div class="calculator-button" onclick="number('9')">9</div>
    <div class="calculator-button" onclick="operation('*')">*</div>
    <!--row 4-->
    <div class="calculator-button-clear" onclick="clearCalc()">A/C</div>
    <div class="calculator-button" onclick="number('0')">0</div>
    <div class="calculator-button" onclick="number('.')">.</div>
    <div class="calculator-button-equals" onclick="equals()">=</div>
</div>


<!-- JavaScript (JS) implementation of the calculator. -->
<script>
// initialize important variables
let output = document.getElementById("output");
let operator = null;
let firstNumber = null;
let nextReady = true;

// Number action
function number (value) { // function to input numbers into the calculator
    if (value != ".") {
        if (nextReady == true) { // nextReady is used to tell the computer when the user is going to input a completely new number
            output.innerHTML = value;
            if (value != "0") { // if statement to ensure that there are no multiple leading zeroes
                nextReady = false;
            }
        } else {
            output.innerHTML = output.innerHTML + value; // concatenation is used to add the numbers to the end of the input
        }
    } else { // special case for adding a decimal; can't have two decimals
        if (output.innerHTML.indexOf(".") == -1) {
            output.innerHTML = output.innerHTML + value;
            nextReady = false;
        }
    }
}

// Operator action
function operation (choice) { // function to input operations into the calculator
    if (firstNumber == null) { // once the operation is chosen, the displayed number is stored into the variable firstNumber
        firstNumber = parseInt(output.innerHTML);
        nextReady = true;
        operator = choice;
        return; // exits function
    }
    // occurs if there is already a number stored in the calculator
    firstNumber = calculate(firstNumber, parseFloat(output.innerHTML)); 
    operator = choice;
    output.innerHTML = firstNumber.toString();
    nextReady = true;
}

// Calculator
function calculate (first, second) { // function to calculate the result of the equation
    let result = 0;
    switch (operator) {
        case "+":
            result = first + second;
            break;
        case "-":
            result = first - second;
            break;
        case "*":
            result = first * second;
            break;
        case "/":
            result = first / second;
            break;
        default: 
            break;
    }
    return result;
}

// Equal action
function equals () { // function used when the equals button is clicked; calculates equation and displays it
    firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
    output.innerHTML = firstNumber.toString();
    nextReady = true;
}

// A/C action
function clearCalc () { // clears calculator
    firstNumber = null;
    output.innerHTML = "0";
    nextReady = true;
}
</script>