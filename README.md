<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Text Editor</title>
<style>
    #text-box {
        width: 300px;
        height: 150px;
        border: 1px solid #ccc;
        padding: 5px;
        font-size: 16px;
        font-family: Arial, sans-serif;
    }
</style>
</head>
<body>
  <div>
    <button onclick="undo()">Undo</button>
    <button onclick="redo()">Redo</button>
  </div>
<div>
    <textarea id="text-box"></textarea>
</div>
<div>
    <select id="font-style" onchange="changeFontStyle()">
        <option value="Arial">Arial</option>
        <option value="Verdana">Verdana</option>
        <option value="Tahoma">Tahoma</option>
        <option value="bold">bold</option>
    </select>
    <input type="color" id="font-color" onchange="changeFontColor()">
    <select id="font-size" onchange="changeFontSize()">
        <option value="12">12px</option>
        <option value="16">16px</option>
        <option value="20">20px</option>
        <option value="30">30px</option>
    </select>
</div>
<script>
    let textHistory = [];
    let textIndex = -1;

    const textBox = document.getElementById('text-box');
    const fontStyleSelect = document.getElementById('font-style');
    const fontColorInput = document.getElementById('font-color');
    const fontSizeSelect = document.getElementById('font-size');

    textBox.addEventListener('input', function() {
        saveState();
    });

    function saveState() {
        if (textIndex < textHistory.length - 1) {
            textHistory.splice(textIndex + 1);
        }
        textHistory.push(textBox.value);
        textIndex++;
    }

    function undo() {
        if (textIndex > 0) {
            textIndex--;
            textBox.value = textHistory[textIndex];
        }
    }

    function redo() {
        if (textIndex < textHistory.length - 1) {
            textIndex++;
            textBox.value = textHistory[textIndex];
        }
    }

    function changeFontStyle() {
        textBox.style.fontFamily = fontStyleSelect.value;
    }

    function changeFontColor() {
        textBox.style.color = fontColorInput.value;
    }

    function changeFontSize() {
        textBox.style.fontSize = fontSizeSelect.value + 'px';
    }
</script>
</body>
</html>
