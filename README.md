<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grammar Spell Caster</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
        }
        .game-container {
            margin: 50px auto;
            width: 80%;
            background: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
        }
        .word-bank, .sentence {
            display: flex;
            justify-content: center;
            margin: 20px;
        }
        .word {
            padding: 10px 15px;
            margin: 5px;
            background: #6200ea;
            color: white;
            border-radius: 5px;
            cursor: grab;
        }
        .dropzone {
            width: 100px;
            height: 40px;
            margin: 5px;
            background: #ddd;
            display: inline-block;
            border-radius: 5px;
            line-height: 40px;
        }
        #checkAnswer {
            padding: 10px 20px;
            background: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h2>Grammar Spell Caster</h2>
        <p>Drag the words into the correct order to form a proper sentence!</p>
        <div class="word-bank">
            <div class="word" draggable="true">quickly</div>
            <div class="word" draggable="true">The</div>
            <div class="word" draggable="true">fox</div>
            <div class="word" draggable="true">jumps</div>
            <div class="word" draggable="true">over</div>
            <div class="word" draggable="true">the</div>
            <div class="word" draggable="true">lazy</div>
            <div class="word" draggable="true">dog</div>
        </div>
        <div class="sentence">
            <div class="dropzone"></div>
            <div class="dropzone"></div>
            <div class="dropzone"></div>
            <div class="dropzone"></div>
            <div class="dropzone"></div>
            <div class="dropzone"></div>
            <div class="dropzone"></div>
            <div class="dropzone"></div>
        </div>
        <button id="checkAnswer">Check Answer</button>
        <p id="result"></p>
    </div>
    
    <script>
        const words = document.querySelectorAll('.word');
        const dropzones = document.querySelectorAll('.dropzone');
        const correctSentence = ["The", "quickly", "fox", "jumps", "over", "the", "lazy", "dog"];

        words.forEach(word => {
            word.addEventListener('dragstart', dragStart);
        });

        dropzones.forEach(zone => {
            zone.addEventListener('dragover', dragOver);
            zone.addEventListener('drop', drop);
        });

        function dragStart(event) {
            event.dataTransfer.setData('text', event.target.innerText);
        }

        function dragOver(event) {
            event.preventDefault();
        }

        function drop(event) {
            event.preventDefault();
            const text = event.dataTransfer.getData('text');
            event.target.innerText = text;
            event.target.classList.add('filled');
        }

        document.getElementById('checkAnswer').addEventListener('click', () => {
            let userSentence = Array.from(dropzones).map(zone => zone.innerText.trim());
            if (JSON.stringify(userSentence) === JSON.stringify(correctSentence)) {
                document.getElementById('result').innerText = 'Correct! You cast the right grammar spell! ✨';
                document.getElementById('result').style.color = 'green';
            } else {
                document.getElementById('result').innerText = 'Oops! Try again. 🧐';
                document.getElementById('result').style.color = 'red';
            }
        });
    </script>
</body>
</html>
