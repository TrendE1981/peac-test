<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PEAC Practice Test</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; background: #f9f9f9; }
    h1 { text-align: center; }
    .section { margin-bottom: 40px; padding: 20px; background: white; border-radius: 10px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    .question { margin-bottom: 20px; }
    .question p { margin-bottom: 5px; }
    input[type="radio"] { margin-right: 10px; }
    button { display: block; margin: 0 auto; padding: 10px 20px; background: #007bff; color: white; border: none; border-radius: 5px; font-size: 16px; cursor: pointer; }
    button:hover { background: #0056b3; }
    .result { text-align: center; font-size: 18px; margin-top: 20px; }
    .correct { background-color: #d4edda; padding: 5px; border-radius: 5px; }
    .incorrect { background-color: #f8d7da; padding: 5px; border-radius: 5px; }
  </style>
</head>
<body>
  <h1>PEAC Online Practice Test</h1>
  <form id="peacTest">
    <div class="section" id="testSection"><h2>Practice Questions</h2></div>
    <button type="submit">Submit</button>
  </form>
  <div class="result" id="result"></div>
  <script>
    const allQuestions = [
      { q: "Which word is most opposite in meaning to scarce?", options: ["Abundant", "Rare", "Limited", "Small"], answer: "Abundant" },
      { q: "Which word does not belong in this group? Banana, Apple, Carrot, Mango", options: ["Banana", "Apple", "Carrot", "Mango"], answer: "Carrot" },
      { q: "Puppy is to Dog as Kitten is to:", options: ["Cat", "Tiger", "Lion", "Baby"], answer: "Cat" },
      { q: "12 × (5 + 3) ÷ 4 = ?", options: ["24", "36", "12", "48"], answer: "24" },
      { q: "What is 25% of 240?", options: ["50", "60", "70", "80"], answer: "60" },
      { q: "Which number is prime?", options: ["21", "17", "25", "33"], answer: "17" },
      { q: "Area of rectangle (8 cm × 5 cm)?", options: ["13", "30", "40", "45"], answer: "40" },
      { q: "Pizza: 8 slices, 3 eaten. What fraction is left?", options: ["3/8", "5/8", "1/2", "6/8"], answer: "5/8" },
      { q: "Convert 2.75 to fraction.", options: ["11/4", "7/2", "9/4", "5/2"], answer: "11/4" },
      { q: "Round 3.786 to 2 decimal places.", options: ["3.78", "3.79", "3.77", "3.80"], answer: "3.79" },
      { q: "Next number in pattern: 2, 4, 8, 16, ___", options: ["24", "30", "32", "34"], answer: "32" },
      { q: "Complete: Square → Circle → Triangle → Square → ___", options: ["Circle", "Triangle", "Square", "Hexagon"], answer: "Circle" },
      { q: "Which shape is different?", options: ["Square", "Rectangle", "Rhombus", "Triangle"], answer: "Triangle" },
      { q: "Continue pattern: Z, X, V, T, ___", options: ["S", "R", "Q", "P"], answer: "R" },
      { q: "What’s common: Cube, Sphere, Pyramid?", options: ["2D shapes", "Flat faces", "3D shapes", "No edges"], answer: "3D shapes" }
    ];

    function loadRandomQuestions() {
      const shuffled = allQuestions.sort(() => 0.5 - Math.random());
      return shuffled.slice(0, 10);
    }

    function renderQuestions(questions) {
      const section = document.getElementById("testSection");
      section.innerHTML = "<h2>Practice Questions</h2>";
      questions.forEach((q, index) => {
        const div = document.createElement("div");
        div.classList.add("question");
        div.innerHTML = `<p>${index + 1}. ${q.q}</p>` + q.options.map(opt => `
          <label><input type="radio" name="q${index}" value="${opt}"> ${opt}</label><br>`).join("");
        section.appendChild(div);
      });
    }

    let currentQuestions = loadRandomQuestions();
    renderQuestions(currentQuestions);

    document.getElementById('peacTest').addEventListener('submit', function(e) {
      e.preventDefault();
      let score = 0;
      currentQuestions.forEach((q, i) => {
        const selected = document.querySelector(`input[name="q${i}"]:checked`);
        const labels = document.querySelectorAll(`input[name="q${i}"]`);
        labels.forEach(input => {
          const parent = input.parentElement;
          if (input.value === q.answer) {
            parent.classList.add("correct");
          } else if (selected && input.checked) {
            parent.classList.add("incorrect");
          }
        });
        if (selected && selected.value === q.answer) score++;
      });
      document.getElementById('result').innerHTML = `Your Score: ${score} out of 10 <br><br> Loading next set...`;
      setTimeout(() => {
        currentQuestions = loadRandomQuestions();
        renderQuestions(currentQuestions);
        document.getElementById('result').textContent = "";
      }, 5000);
    });
  </script>
</body>
</html>
