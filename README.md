# DIGIBHEM
I'm creating a calculator by using html,css and javascript


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Real-Time Calculator</title>
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f0f0;
        }

        .calculator {
            border: 1px solid #000;
            padding: 20px;
            border-radius: 5px;
            background-color: #fff;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }

        button {
            padding: 10px;
            font-size: 16px;
            cursor: pointer;
        }

        #display {
            margin-bottom: 20px;
            font-size: 20px;
            padding: 10px;
            width: calc(100% - 22px);
        }
    </style>
</head>
<body>

<div class="calculator">
    <input type="text" id="display" disabled>
    <div class="buttons">
        <button onclick="appendNumber('1')">1</button>
        <button onclick="appendNumber('2')">2</button>
        <button onclick="appendNumber('3')">3</button>
        <button onclick="selectOperation('+')">+</button>
        <button onclick="appendNumber('4')">4</button>
        <button onclick="appendNumber('5')">5</button>
        <button onclick="appendNumber('6')">6</button>
        <button onclick="selectOperation('-')">-</button>
        <button onclick="appendNumber('7')">7</button>
        <button onclick="appendNumber('8')">8</button>
        <button onclick="appendNumber('9')">9</button>
        <button onclick="selectOperation('*')">*</button>
        <button onclick="appendNumber('0')">0</button>
        <button onclick="calculate()">=</button>
        <button onclick="clearDisplay()">C</button>
        <button onclick="selectOperation('/')">/</button>
    </div>
</div>

<script>
    let currentInput = '';
    let previousInput = '';
    let operation = null;

    function appendNumber(number) {
        if(currentInput.includes('.') && number === '.') return;
        currentInput += number;
        updateDisplay();
    }

    function selectOperation(op) {
        if(currentInput === '') return;
        if(previousInput !== '') {
            calculate();
        }
        operation = op;
        previousInput = currentInput;
        currentInput = '';
    }

    function calculate() {
        let computation;
        const prev = parseFloat(previousInput);
        const current = parseFloat(currentInput);
        if(isNaN(prev) || isNaN(current)) return;
        switch(operation) {
            case '+':
                computation = prev + current;
                break;
            case '-':
                computation = prev - current;
                break;
            case '*':
                computation = prev * current;
                break;
            case '/':
                if(current === 0) {
                    alert("Division by zero is not allowed.");
                    return;
                }
                computation = prev / current;
                break;
            default:
                return;
        }
        currentInput = computation.toString();
        operation = undefined;
        previousInput = '';
        updateDisplay();
    }

    function clearDisplay() {
        currentInput = '';
        previousInput = '';
        operation = null;
        updateDisplay();
    }

    function updateDisplay() {
        document.getElementById('display').value = currentInput;
    }
</script>
</body>
</html>
