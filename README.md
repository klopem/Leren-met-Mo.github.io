<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Study English-Dutch Words & Quiz</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: 'Arial', sans-serif;
    }

    /* Header styling */
    header {
      background: linear-gradient(135deg, #007BFF, #0056b3);
      color: white;
      padding: 1.5rem;
      text-align: center;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      animation: slideDown 0.5s ease-out;
    }

    @keyframes slideDown {
      from { transform: translateY(-100%); }
      to { transform: translateY(0); }
    }

    header h1 {
      font-size: 2rem;
      font-weight: bold;
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
    }

    /* Body styling */
    body {
      background: #f4f4f9;
      color: #333;
      padding-top: 80px;
    }

    .container {
      max-width: 800px;
      margin: 0 auto;
      padding: 20px;
    }

    h1 {
      color: #007BFF;
      margin-bottom: 20px;
      animation: fadeIn 1s ease-in;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    /* Table styling */
    table {
      width: 100%;
      margin: 20px auto;
      border-collapse: collapse;
      background: white;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      border-radius: 10px;
      overflow: hidden;
      animation: fadeIn 1s ease-in;
    }

    th, td {
      border: 1px solid #ddd;
      padding: 12px;
      text-align: left;
    }

    th {
      background-color: #007BFF;
      color: white;
      font-weight: bold;
    }

    td {
      background-color: #f9f9f9;
    }

    tr:hover td {
      background-color: #f1f1f1;
      transform: scale(1.02);
      transition: transform 0.3s ease, background 0.3s ease;
    }

    /* Quiz section styling */
    .quiz-section {
      background: white;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      margin-top: 20px;
      animation: fadeIn 1s ease-in;
    }

    .quiz-section h1 {
      margin-bottom: 15px;
    }

    input[type="text"] {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #ddd;
      border-radius: 5px;
      font-size: 1rem;
    }

    button {
      padding: 10px 20px;
      background-color: #007BFF;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background 0.3s ease, transform 0.3s ease;
    }

    button:hover {
      background: #0056b3;
      transform: scale(1.05);
    }

    #feedback {
      margin-top: 15px;
      font-weight: bold;
      animation: fadeIn 0.5s ease;
    }

    .correct {
      color: green;
    }

    .incorrect {
      color: red;
    }

    /* Responsive design */
    @media (max-width: 768px) {
      header h1 {
        font-size: 1.5rem;
      }

      table {
        font-size: 0.9rem;
      }

      .quiz-section {
        padding: 15px;
      }
    }
  </style>
</head>
<body>
  <header>
    <h1>Leren met Mo</h1>
  </header>

  <div class="container">
    <h1>Study English-Dutch Words</h1>
    <table>
      <tr>
        <th>English</th>
        <th>Dutch</th>
      </tr>
      <tr><td>matter</td><td>ertoe doen</td></tr>
      <tr><td>memorial service</td><td>herdenkingsdienst</td></tr>
      <tr><td>struggle</td><td>strijd</td></tr>
      <tr><td>mobilise</td><td>mobiliseren</td></tr>
      <tr><td>movement</td><td>beweging</td></tr>
      <tr><td>appoint</td><td>benoemen (tot)</td></tr>
      <tr><td>observant</td><td>oplettend</td></tr>
      <tr><td>outrageous</td><td>schandelijk</td></tr>
      <tr><td>legacy</td><td>nalatenschap</td></tr>
      <tr><td>chokehold</td><td>wurggreep</td></tr>
      <tr><td>unconscious</td><td>bewusteloos</td></tr>
      <tr><td>injustice</td><td>onrechtvaardigheid, onrecht</td></tr>
      <tr><td>mindset</td><td>mentaliteit</td></tr>
      <tr><td>participate in</td><td>deelnemen aan</td></tr>
      <tr><td>make a difference</td><td>verschil maken</td></tr>
      <!-- Add more rows as needed -->
    </table>

    <div class="quiz-section">
      <h1>Quiz: Translate the Word</h1>
      <p>Translate the word: <strong id="question-word"></strong></p>
      <input type="text" id="answer" placeholder="Type your answer" aria-label="Type your answer">
      <button onclick="checkAnswer()">Submit</button>
      <p id="feedback"></p>
    </div>
  </div>

  <script>
    const words = {
      "matter": "ertoe doen",
      "memorial service": "herdenkingsdienst",
      "struggle": "strijd",
      "mobilise": "mobiliseren",
      "movement": "beweging",
      "appoint": "benoemen (tot)",
      "observant": "oplettend",
      "outrageous": "schandelijk",
      "legacy": "nalatenschap",
      "chokehold": "wurggreep",
      "unconscious": "bewusteloos",
      "injustice": "onrechtvaardigheid, onrecht",
      "mindset": "mentaliteit",
      "participate in": "deelnemen aan",
      "make a difference": "verschil maken",
      // Add more words as needed
    };

    let wordKeys = Object.keys(words);
    let shuffledWords = shuffleArray(wordKeys);
    let currentIndex = 0;

    // Shuffle array function
    function shuffleArray(array) {
      return array.sort(() => Math.random() - 0.5);
    }

    // Display the next word
    function getNextWord() {
      if (currentIndex >= shuffledWords.length) {
        shuffledWords = shuffleArray(wordKeys);
        currentIndex = 0;
      }
      document.getElementById("question-word").textContent = shuffledWords[currentIndex];
      currentIndex++;
    }

    // Check the user's answer
    function checkAnswer() {
      const userAnswer = document.getElementById("answer").value.trim().toLowerCase();
      const correctAnswer = words[document.getElementById("question-word").textContent].toLowerCase();
      const feedbackElement = document.getElementById("feedback");

      if (!userAnswer) {
        feedbackElement.textContent = "Please enter an answer.";
        feedbackElement.className = "incorrect";
        return;
      }

      if (userAnswer === correctAnswer) {
        feedbackElement.textContent = "✅ Correct!";
        feedbackElement.className = "correct";
      } else {
        feedbackElement.textContent = `❌ Incorrect. The correct answer is "${correctAnswer}".`;
        feedbackElement.className = "incorrect";
      }

      document.getElementById("answer").value = "";
      getNextWord();
    }

    // Event listener for Enter key
    document.getElementById("answer").addEventListener("keypress", function(event) {
      if (event.key === "Enter") {
        checkAnswer();
      }
    });

    // Initialize the first word
    getNextWord();
  </script>
</body>
</html>
