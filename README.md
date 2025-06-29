# peac-test
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
  </style>
</head>
<body>
  <h1>PEAC Online Practice Test</h1>
  <form id="peacTest">

    <div class="section" id="verbal">
      <h2>Verbal Reasoning</h2>
    </div>

    <div class="section" id="quantitative">
      <h2>Quantitative Reasoning</h2>
    </div>

    <div class="section" id="abstract">
      <h2>Abstract Reasoning</h2>
    </div>

    <button type="submit">Submit</button>
  </form>

  <div class="result" id="result"></div>

  <script>
    const questions = [
      // Verbal Reasoning (Questions 1-15)
      { q: "Which word is most opposite in meaning to scarce?", options: ["Abundant", "Rare", "Limited", "Small"], answer: "Abundant" },
      { q: "Which word does not belong in this group?\nBanana, Apple, Carrot, Mango", options: ["Banana", "Apple", "Carrot", "Mango"], answer: "Carrot" },
      { q: "Puppy is to Dog as Kitten is to:", options: ["Cat", "Tiger", "Lion", "Baby"], answer: "Cat" },
      { q: "Which sentence is grammatically correct?", options: ["He don’t like maths.", "She has went to the library.", "They have completed the homework.", "Me and him are friends."], answer: "They have completed the homework." },
      { q: "Choose the best synonym for ancient:", options: ["Recent", "Modern", "Old", "Fresh"], answer: "Old" },
      { q: "The scientist made an amazing __________.", options: ["Decoration", "Discovery", "Distribution", "Decision"], answer: "Discovery" },
      { q: "Which word is a compound word?", options: ["Sunlight", "Sunny", "Lighten", "Shine"], answer: "Sunlight" },
      { q: "Plural form of analysis:", options: ["Analysises", "Analyzes", "Analysi", "Analyses"], answer: "Analyses" },
      { q: "Find the correct spelling:", options: ["Definately", "Definitely", "Definantly", "Definetly"], answer: "Definitely" },
      { q: "Which two words are most similar?", options: ["Brave, coward", "Fast, rapid", "Hard, soft", "Loud, silent"], answer: "Fast, rapid" },
      { q: "Best title for a teamwork story:", options: ["The Lonely Tree", "The Magical Hat", "Together We Win", "The Secret Cave"], answer: "Together We Win" },
      { q: "Add a word to both sides of '____time____' to make compounds:", options: ["Pass", "Over", "Some", "Any"], answer: "Some" },
      { q: "Rearrange: NATLOAVIC to form a meaningful word:", options: ["Vocation", "Vacation", "Volcanic", "National"], answer: "Vocation" },
      { q: "She will __________ the prize:", options: ["Except", "Accept"], answer: "Accept" },
      { q: "Meaning of 'Don’t cry over spilt milk':", options: ["Don’t waste food", "Don’t be sad about what can’t be changed", "Clean up your mess", "Always drink your milk"], answer: "Don’t be sad about what can’t be changed" },

      // Quantitative Reasoning (16-30)
      { q: "12 × (5 + 3) ÷ 4 = ?", options: ["24", "36", "12", "48"], answer: "24" },
      { q: "Chocolate bar costs $3.50. Cost of 4 bars?", options: ["$14.00", "$12.50", "$11.50", "$10.00"], answer: "$14.00" },
      { q: "What is 25% of 240?", options: ["50", "60", "70", "80"], answer: "60" },
      { q: "Which number is prime?", options: ["21", "17", "25", "33"], answer: "17" },
      { q: "Area of rectangle (8 cm × 5 cm)?", options: ["13", "30", "40", "45"], answer: "40" },
      { q: "Complete: 7, 14, ___, 56, 112", options: ["21", "28", "35", "42"], answer: "28" },
      { q: "Pizza: 8 slices, 3 eaten. What fraction is left?", options: ["3/8", "5/8", "1/2", "6/8"], answer: "5/8" },
      { q: "Convert 2.75 to fraction.", options: ["11/4", "7/2", "9/4", "5/2"], answer: "11/4" },
      { q: "Round 3.786 to 2 decimal places.", options: ["3.78", "3.79", "3.77", "3.80"], answer: "3.79" },
      { q: "Complete the pattern: 5, 9, 17, 33, ___", options: ["41", "53", "65", "49"], answer: "65" },
      { q: "Mean of 5, 10, 15, 20?", options: ["10", "12.5", "15", "20"], answer: "12.5" },
      { q: "1.5 litres in millilitres?", options: ["500", "1000", "1500", "2000"], answer: "1500" },
      { q: "1/3 of number is 12. Find number.", options: ["36", "24", "18", "30"], answer: "36" },
      { q: "Train travels 60 km/hr. How far in 2.5 hrs?", options: ["120", "140", "150", "160"], answer: "150" },
      { q: "Triangle angles: 65° & 75°. Third angle?", options: ["30°", "40°", "45°", "50°"], answer: "40°" },

      // Abstract Reasoning (31-45)
      { q: "What comes next? * ^ * ^ * ___", options: ["*", "^", "#", "o"], answer: "^" },
      { q: "Which shape is different?", options: ["Square", "Rectangle", "Rhombus", "Triangle"], answer: "Triangle" },
      { q: "Next number in pattern: 2, 4, 8, 16, ___", options: ["24", "30", "32", "34"], answer: "32" },
      { q: "Complete: Square → Circle → Triangle → Square → ___", options: ["Circle", "Triangle", "Square", "Hexagon"], answer: "Circle" },
      { q: "Which pattern is rotated differently?", options: ["A", "B", "C", "D"], answer: "C" },
      { q: "Fill in: A, C, F, J, O, ___", options: ["S", "T", "U", "V"], answer: "U" },
      { q: "Odd one out:", options: ["121", "144", "169", "152"], answer: "152" },
      { q: "Mirror image of L-shape facing right-down is facing?", options: ["Left-up", "Left-down", "Right-up", "Right-down"], answer: "Left-up" },
      { q: "If D=2, C=3, H=5, then D + C + H = ?", options: ["10", "9", "11", "8"], answer: "10" },
      { q: "Continue pattern: Z, X, V, T, ___", options: ["S", "R", "Q", "P"], answer: "R" },
      { q: "Grid: 3 6 9 | 2 4 6 | 1 ___ 3", options: ["1", "2", "3", "4"], answer: "2" },
      { q: "What’s common: Cube, Sphere, Pyramid?", options: ["2D shapes", "Flat faces", "3D shapes", "No edges"], answer: "3D shapes" },
      { q: "Which has no straight sides?", options: ["Triangle", "Circle", "Pentagon", "Hexagon"], answer: "Circle" },
      { q: "Shaded pattern: [X][ ][X][ ][X][ ][X] ___", options: ["[X]", "[ ]", "[#]", "[*]"], answer: "[ ]" },
      { q: "Pattern: 100, 90, 81, 73, ___", options: ["64", "66", "65", "67"], answer: "66" },
    ];

    const sections = {
      verbal: document.getElementById("verbal"),
      quantitative: document.getElementById("quantitative"),
      abstract: document.getElementById("abstract")
    };

    questions.forEach((q, index) => {
      const div = document.createElement("div");
      div.classList.add("question");
      div.innerHTML = `<p>${index + 1}. ${q.q}</p>` + q.options.map(opt => `
        <label><input type="radio" name="q${index + 1}" value="${opt}">${opt}</label><br>`).join("");

      if (index < 15) sections.verbal.appendChild(div);
      else if (index < 30) sections.quantitative.appendChild(div);
      else sections.abstract.appendChild(div);
    });

    document.getElementById('peacTest').addEventListener('submit', function(e) {
      e.preventDefault();
      let score = 0;
      questions.forEach((q, i) => {
        const selected = document.querySelector(`input[name="q${i + 1}"]:checked`);
        if (selected && selected.value === q.answer) score++;
      });
      document.getElementById('result').textContent = `Your Score: ${score} out of 45`;
    });
  </script>
</body>
</html>
