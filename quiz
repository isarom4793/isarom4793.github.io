<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Veterinary Anatomy Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            line-height: 1.6;
            background-color: #f9f9f9;
        }
        .quiz-container {
            max-width: 600px;
            margin: auto;
            padding: 20px;
            background: #fff;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        .question {
            margin-bottom: 20px;
        }
        .answers {
            list-style-type: none;
            padding: 0;
        }
        .answers li {
            margin-bottom: 10px;
        }
        .answers label {
            cursor: pointer;
        }
        .button {
            display: block;
            margin: 20px auto;
            padding: 10px 20px;
            font-size: 16px;
            color: #fff;
            background-color: #007BFF;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .button:hover {
            background-color: #0056b3;
        }
        .result {
            text-align: center;
            font-size: 18px;
            margin-top: 20px;
        }
        .write-in {
            margin-top: 10px;
        }
        .match {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
        }
        .match .item {
            background: #eef;
            padding: 10px;
            border-radius: 5px;
            cursor: grab;
            border: 1px solid #ccc;
        }
        .match .droppable {
            padding: 15px;
            background: #f7f7f7;
            border: 2px dashed #ccc;
            border-radius: 5px;
            min-width: 120px;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <h1>Veterinary Anatomy Quiz</h1>
        <div id="quiz"></div>
        <button id="submit" class="button">Submit</button>
        <div id="results" class="result"></div>
    </div>

    <script>
        const quizData = [
            {
                type: "multiple-choice",
                question: "¿Cuáles son las partes principales del sistema urinario?",
                answers: [
                    "El corazón y los pulmones",
                    "Los riñones y las vías de excreción",
                    "El estómago y el intestino",
                    "Los huesos y los músculos"
                ],
                correct: 1
            },
            {
                type: "write-in",
                question: "¿Cuál es la unidad funcional del riñón?",
                correct: "La nefrona"
            },
            {
                type: "match",
                question: "Empareja los órganos con sus funciones:",
                pairs: [
                    { key: "Riñón", value: "Filtrar la sangre" },
                    { key: "Útero", value: "Alojar el embrión" },
                    { key: "Túbulos seminíferos", value: "Producir espermatozoides" }
                ]
            }
        ];

        const quizContainer = document.getElementById('quiz');
        const resultsContainer = document.getElementById('results');
        const submitButton = document.getElementById('submit');

        function buildQuiz() {
            const output = [];
            quizData.forEach((question, index) => {
                if (question.type === "multiple-choice") {
                    const answers = question.answers.map((answer, i) => `
                        <li>
                            <label>
                                <input type="radio" name="question${index}" value="${i}">
                                ${answer}
                            </label>
                        </li>
                    `).join('');
                    output.push(`
                        <div class="question">${question.question}</div>
                        <ul class="answers">${answers}</ul>
                    `);
                } else if (question.type === "write-in") {
                    output.push(`
                        <div class="question">${question.question}</div>
                        <input type="text" class="write-in" id="writein-${index}" />
                    `);
                } else if (question.type === "match") {
                    const keys = question.pairs.map(pair => `<div class="item" draggable="true" data-key="${pair.key}">${pair.key}</div>`).join('');
                    const values = question.pairs.map(pair => `<div class="droppable" data-value="${pair.value}">${pair.value}</div>`).join('');
                    output.push(`
                        <div class="question">${question.question}</div>
                        <div class="match">${keys}${values}</div>
                    `);
                }
            });
            quizContainer.innerHTML = output.join('');

            // Add drag and drop functionality
            const draggableItems = document.querySelectorAll('.item');
            const droppableAreas = document.querySelectorAll('.droppable');

            draggableItems.forEach(item => {
                item.addEventListener('dragstart', e => {
                    e.dataTransfer.setData('text/plain', e.target.getAttribute('data-key'));
                });
            });

            droppableAreas.forEach(area => {
                area.addEventListener('dragover', e => {
                    e.preventDefault();
                });
                area.addEventListener('drop', e => {
                    e.preventDefault();
                    const data = e.dataTransfer.getData('text/plain');
                    const matchKey = e.target.getAttribute('data-value');
                    if (data === matchKey) {
                        e.target.textContent = `✓ ${matchKey}`;
                        e.target.style.background = '#d4edda';
                        e.target.style.color = '#155724';
                    } else {
                        e.target.textContent = `✗ ${matchKey}`;
                        e.target.style.background = '#f8d7da';
                        e.target.style.color = '#721c24';
                    }
                });
            });
        }

        function showResults() {
            let score = 0;
            quizData.forEach((question, index) => {
                if (question.type === "multiple-choice") {
                    const selected = document.querySelector(`input[name=question${index}]:checked`);
                    if (selected && parseInt(selected.value) === question.correct) {
                        score++;
                    }
                } else if (question.type === "write-in") {
                    const input = document.getElementById(`writein-${index}`);
                    if (input && input.value.trim().toLowerCase() === question.correct.toLowerCase()) {
                        score++;
                    }
                } else if (question.type === "match") {
                    const droppableAreas = document.querySelectorAll('.droppable');
                    droppableAreas.forEach(area => {
                        if (area.textContent.startsWith('✓')) {
                            score++;
                        }
                    });
                }
            });
            resultsContainer.textContent = `You got ${score} out of ${quizData.length} correct!`;
        }

        buildQuiz();
        submitButton.addEventListener('click', showResults);
    </script>
</body>
</html>
