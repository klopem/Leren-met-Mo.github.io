<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive English-Dutch Word Quiz</title>
  <style>
    /* General Styles */
    body {
      font-family: 'Arial', sans-serif;
      text-align: center;
      margin: 0;
      padding: 0;
      background-color: #f0f8f0;
      color: #333;
      transition: background-color 0.5s, color 0.5s;
    }

    h1 {
      color: #228B22;
      margin-bottom: 20px;
      font-size: 2.5em;
      animation: fadeIn 2s ease-in-out;
    }

    h1::after {
      content: " - Created by [Your Name]";
      font-size: 0.6em;
      color: #555;
    }

    /* Dark Mode Styles */
    body.dark-mode {
      background-color: #121212;
      color: #e0e0e0;
    }

    body.dark-mode h1 {
      color: #4CAF50;
    }

    body.dark-mode table {
      background-color: #1e1e1e;
      color: #e0e0e0;
    }

    body.dark-mode th {
      background-color: #4CAF50;
    }

    body.dark-mode td {
      background-color: #2c2c2c;
    }

    body.dark-mode button {
      background-color: #4CAF50;
    }

    body.dark-mode button:hover {
      background-color: #45a049;
    }

    /* Table Styles */
    table {
      width: 90%;
      max-width: 800px;
      margin: 20px auto;
      border-collapse: collapse;
      background: white;
      box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
      border-radius: 10px;
      overflow: hidden;
      animation: slideIn 1s ease-in-out;
    }

    th, td {
      border: 1px solid #ddd;
      padding: 12px;
    }

    th {
      background-color: #228B22;
      color: white;
    }

    td {
      background-color: #f9f9f9;
    }

    tr:hover td {
      background-color: #f1f1f1;
      transition: background-color 0.3s ease;
    }

    /* Quiz Section Styles */
    #quiz-section {
      margin-top: 40px;
      animation: fadeIn 2s ease-in-out;
    }

    #question-word {
      font-size: 1.5em;
      color: #228B22;
      animation: bounce 1s infinite;
    }

    input[type="text"] {
      padding: 10px;
      margin-top: 10px;
      border: 2px solid #228B22;
      border-radius: 5px;
      font-size: 1em;
      transition: border-color 0.3s ease;
    }

    input[type="text"]:focus {
      border-color: #4CAF50;
      outline: none;
    }

    button {
      padding: 10px 20px;
      margin-top: 10px;
      background-color: #228B22;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1em;
      transition: background-color 0.3s ease, transform 0.3s ease;
    }

    button:hover {
      background-color: #1c6b1c;
      transform: scale(1.05);
    }

    #feedback {
      margin-top: 15px;
      font-weight: bold;
      animation: fadeIn 1s ease-in-out;
    }

    .correct {
      color: green;
    }

    .incorrect {
      color: red;
    }

    /* Animations */
    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    @keyframes slideIn {
      from { transform: translateY(-20px); opacity: 0; }
      to { transform: translateY(0); opacity: 1; }
    }

    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }

    /* Dark Mode Toggle Button */
    #mode-toggle {
      position: fixed;
      top: 20px;
      right: 20px;
      background-color: #228B22;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 5px;
      cursor: pointer;
      font-size: 1em;
      transition: background-color 0.3s ease, transform 0.3s ease;
    }

    #mode-toggle:hover {
      background-color: #1c6b1c;
      transform: scale(1.05);
    }

    /* Background Image */
    body {
      background-image: url('https://via.placeholder.com/1920x1080'); /* Replace with your image link */
      background-size: cover;
      background-position: center;
    }

    body.dark-mode {
      background-image: url('https://via.placeholder.com/1920x1080/000000/333333'); /* Replace with your dark mode image link */
    }
  </style>
</head>
<body>
  <h1>Study English-Dutch Words</h1>
  <button id="mode-toggle">Toggle Dark Mode</button>

  <table>
    <tr>
      <th>#</th>
      <th>English</th>
      <th>Dutch</th>
    </tr>
    <tr><td>1</td><td>matter</td><td>ertoe doen</td></tr>
    <tr><td>2</td><td>memorial service</td><td>herdenkingsdienst</td></tr>
    <tr><td>3</td><td>struggle</td><td>strijd</td></tr>
    <!-- Add more rows as needed -->
  </table>

  <div id="quiz-section">
    <h1>Quiz: Translate the Word</h1>
    <p>Translate the word: <strong id="question-word"></strong></p>
    <input type="text" id="answer" placeholder="Type your answer">
    <button onclick="checkAnswer()">Submit</button>
    <p id="feedback"></p>
  </div>

  <script>
    const words = {
      "matter": "ertoe doen",
      "memorial service": "herdenkingsdienst",
      "struggle": "strijd",
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

    // Dark Mode Toggle
    const modeToggle = document.getElementById("mode-toggle");
    modeToggle.addEventListener("click", () => {
      document.body.classList.toggle("dark-mode");
    });

    // Initialize the first word
    getNextWord();
  </script>
</body>
</html>
