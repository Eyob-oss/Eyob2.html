<!DOCTYPE html>
<html lang="en">
<head>
 <body> <button oneclick = "aboutUs()"> <p1> aboutUs ℹ️</p1> </button> </body>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chemistry Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
            padding: 20px;
            background-color: #f4f4f4;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .question {
            margin: 15px 0;
            font-weight: bold;
            color: #555;
        }
        .options {
            margin: 10px 0;
        }
        label {
            display: block;
            margin: 5px 0;
            padding: 5px;
            background-color: #FFD4A8;
            border-radius: 4px;
            cursor: pointer;
        }
        label:hover {
            background-color: #FFD4A8;
        }
        button {
            display: block;
            margin: 20px auto;
            padding: 10px 20px;
            font-size: 16px;
            color: white;
            background-color: #007bff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        #result {
            margin-top: 20px;
            font-size: 16px;
            color: #333;
        }
    </style>
</head>
<body>

<h1>Chemistry Quiz</h1>
<div id="quiz"></div>
<button onclick="checkAnswers()"> Checke<br> Answer</button>
<div id="result"></div>
<button onclick="resetanswer()"> Reset Answer</button>
<div id="reset"></div>

<script>
    const questions = [
        {
            question: "1.What is the chemical symbol for water?",
            options: ["A) H2O", "B) O2", "C) H2", "D) HO"],
            answer: "H2O",
            explanation: "Water is made up of two hydrogen atoms bonded to one oxygen atom."
        },
        {
            question: "2.What is the pH of pure water at 25°C?",
            options: ["A) 6", "B) 7", "C) 8", "D) 5"],
            answer: "7",
            explanation: "Pure water is neutral, which has a pH of 7."
        },
        {
            question: "3.What is the atomic number of carbon?",
            options: ["A) 6", "B) 12", "C) 14", "D) 8"],
            answer: "6",
            explanation: "Carbon has 6 protons in its nucleus, which defines its atomic number."
        },
        {
            question: "4.Is sodium chloride (NaCl) an example of a covalent bond?",
            options: ["A) Yes", "B) No", "C) Depends on conditions", "D) Not sure"],
            answer: "No",
            explanation: "Sodium chloride is an ionic compound, formed from the electrostatic attraction between ions."
        },
        {
            question: "5.What is the chemical formula for glucose?",
            options: ["A) C6H12O6", "B) C12H22O11", "C) C6H6", "D) CH4"],
            answer: "C6H12O6",
            explanation: "Glucose is a simple sugar with the chemical formula C6H12O6."
        },
        {
            question: "6.Which gas is produced during photosynthesis?",
            options: ["A) Oxygen", "B) Carbon dioxide", "C) Nitrogen", "D) Hydrogen"],
            answer: "Oxygen",
            explanation: "Oxygen is produced as a byproduct of photosynthesis."
        },
        {
            question: "7.What is the most abundant gas in the Earth's atmosphere?",
            options: ["A) Oxygen", "B) Carbon dioxide", "C) Nitrogen", "D) Argon"],
            answer: "Nitrogen",
            explanation: "Nitrogen makes up about 78% of the Earth's atmosphere."
        },
        {
            question: "8.What is the primary component of natural gas?",
            options: ["A) Ethylene", "B) Methane", "C) Propane", "D) Butane"],
            answer: "Methane",
            explanation: "Methane (CH4) is the main component of natural gas."
        },
        {
            question: "9.Which element has the chemical symbol 'Fe'?",
            options: ["A) Fluorine", "B) Iron", "C) Francium", "D) Fermium"],
            answer: "Iron",
            explanation: "Fe is the chemical symbol for iron."
        },
        {
            question: "10.What is the boiling point of water at sea level?",
            options: ["A) 100°C", "B) 90°C", "C) 80°C", "D) 110°C"],
            answer: "100°C",
            explanation: "Water boils at 100°C (212°F) at sea level."
        },
        {
            question: "11.What is the chemical formula for table salt?",
            options: ["A) NaCl", "B) KCl", "C) CaCl2", "D) MgCl2"],
            answer: "NaCl",
            explanation: "Table salt is sodium chloride (NaCl)."
        },
        {
            question: "12.Which acid is found in vinegar?",
            options: ["A) Hydrochloric acid", "B) Acetic acid", "C) Sulfuric acid", "D) Citric acid"],
            answer: "Acetic acid",
            explanation: "Vinegar contains acetic acid (CH3COOH)."
        },
        {
            question: "13.What is the chemical name for the compound with the formula NH3?",
            options: ["A) Ammonia", "B) Nitric acid", "C) Nitrogen dioxide", "D) Urea"],
            answer: "Ammonia",
            explanation: "NH3 is known as ammonia."
        },
        {
            question: "14.Which of the following is a noble gas?",
            options: ["A) Oxygen", "B) Helium", "C) Nitrogen", "D) Hydrogen"],
            answer: "Helium",
            explanation: "Helium is a noble gas, known for its lack of reactivity."
        },
        {
            question: "15.What is the main product of the combustion of hydrocarbons?",
            options: ["A) Carbon monoxide", "B) Carbon dioxide", "C) Water", "D) All of the above"],
            answer: "All of the above",
            explanation: "Combustion can produce carbon monoxide, carbon dioxide, and water."
        },
        {
            question: "16.Which element is essential for all living things?",
            options: ["A) Gold", "B) Carbon", "C) Lead", "D) Silver"],
            answer: "Carbon",
            explanation: "Carbon is a fundamental element in organic compounds."
        },
        {
            question: "17.What is the chemical formula for sulfuric acid?",
            options: ["A) HCl", "B) H2SO4", "C) HNO3", "D) CH3COOH"],
            answer: "H2SO4",
            explanation: "Sulfuric acid is represented by the formula H2SO4."
        },
        {
            question: "18.Which of the following is a strong acid?",
            options: ["A) Acetic acid", "B) Citric acid", "C) Hydrochloric acid", "D) Carbonic acid"],
            answer: "Hydrochloric acid",
            explanation: "Hydrochloric acid (HCl) is a strong acid."
        },
        {
            question: "19.What is the formula for calculating density?",
            options: ["A) Mass/Volume", "B) Volume/Mass", "C) Mass + Volume", "D) Mass - Volume"],
            answer: "Mass/Volume",
            explanation: "Density is calculated as mass divided by volume."
        },
        {
            question: "20.Which of the following is NOT a chemical change?",
            options: ["A) Burning wood", "B) Rusting iron", "C) Dissolving sugar in water", "D) Baking a cake"],
            answer: "Dissolving sugar in water",
            explanation: "Dissolving sugar is a physical change, not a chemical change."
        }
    ];

    function loadQuiz() {
        const quizContainer = document.getElementById('quiz');
        questions.forEach((q, index) => {
            quizContainer.innerHTML += `
                <div class="question">
                    ${q.question}
                    <div class="options">
                        ${q.options.map(option => `
                            <label>
                                <input type="radio" name="question${index}" value="${option.substring(3)}">
                                ${option}
                            </label>
                        `).join('')}
                    </div>
                </div>
            `;
        });
    }

    function checkAnswers() {
        let resultHTML = '';
        questions.forEach((q, index) => {
            const selectedOption = document.querySelector(`input[name="question${index}"]:checked`);
            if (selectedOption) {
                const userAnswer = selectedOption.value;
                if (userAnswer === q.answer) {
                    resultHTML += `<p>Question ${index + 1}: Correct!</p>`;
                } else {
                    resultHTML += `<p>Question ${index + 1}: Incorrect. ${q.explanation}</p>`;
                }
            } else {
                resultHTML += `<p>Question ${index + 1}: No answer selected.</p>`;
            }
        });
        document.getElementById('result').innerHTML = resultHTML;
    }

    // Load the quiz on page load
    window.onload = loadQuiz;
</script>

</body>
</html>
