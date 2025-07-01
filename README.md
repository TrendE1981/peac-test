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
    #timer { text-align: center; font-size: 18px; margin-bottom: 20px; }
  </style>
</head>
<body>
  <h1>PEAC Online Practice Test</h1>
  <div id="timer">Time Remaining: <span id="time">15:00</span></div>
  <form id="peacTest">
    <div class="section" id="verbal"><h2>Verbal Reasoning</h2></div>
    <div class="section" id="quantitative"><h2>Quantitative Reasoning</h2></div>
    <div class="section" id="abstract"><h2>Abstract Reasoning</h2></div>
    <button type="submit">Submit</button>
  </form>
  <div class="result" id="result"></div>
  <script>
    let totalSeconds = 15 * 60;
    const timerDisplay = document.getElementById("time");
    const countdown = setInterval(() => {
      let minutes = Math.floor(totalSeconds / 60);
      let seconds = totalSeconds % 60;
      timerDisplay.textContent = `${minutes}:${seconds.toString().padStart(2, '0')}`;
      totalSeconds--;
      if (totalSeconds < 0) {
        clearInterval(countdown);
        document.getElementById("peacTest").requestSubmit();
      }
    }, 1000);

    const questionBank = { /* ... existing questions ... */ };

    function getRandomSubset(arr, size) {
      return arr.sort(() => 0.5 - Math.random()).slice(0, size);
    }

    function renderSection(sectionId, questions) {
      const section = document.getElementById(sectionId);
      section.innerHTML = "<h2>" + sectionId.charAt(0).toUpperCase() + sectionId.slice(1) + " Reasoning</h2>";
      questions.forEach((q, index) => {
        const div = document.createElement("div");
        div.classList.add("question");
        div.innerHTML = `<p>${index + 1}. ${q.q}</p>` + q.options.map(opt => `
          <label><input type="radio" name="${sectionId}_${index}" value="${opt}"> ${opt}</label><br>`).join("");
        section.appendChild(div);
      });
    }

    let current = {
      verbal: getRandomSubset(questionBank.verbal, 15),
      quantitative: getRandomSubset(questionBank.quantitative, 15),
      abstract: getRandomSubset(questionBank.abstract, 15)
    };

    renderSection("verbal", current.verbal);
    renderSection("quantitative", current.quantitative);
    renderSection("abstract", current.abstract);

    document.getElementById('peacTest').addEventListener('submit', function(e) {
      e.preventDefault();
      clearInterval(countdown);
      let score = 0;
      const total = 45;

      Object.entries(current).forEach(([sectionId, questions]) => {
        questions.forEach((q, i) => {
          const selected = document.querySelector(`input[name="${sectionId}_${i}"]:checked`);
          const options = document.querySelectorAll(`input[name="${sectionId}_${i}"]`);
          options.forEach(input => {
            const label = input.parentElement;
            if (input.value === q.answer) {
              label.classList.add("correct");
            } else if (selected && input.checked) {
              label.classList.add("incorrect");
            }
          });
          if (selected && selected.value === q.answer) score++;
        });
      });

      document.getElementById('result').innerHTML = `Your Score: ${score} out of ${total} <br><br> Loading next set...`;
      setTimeout(() => {
        totalSeconds = 15 * 60;
        current = {
          verbal: getRandomSubset(questionBank.verbal, 15),
          quantitative: getRandomSubset(questionBank.quantitative, 15),
          abstract: getRandomSubset(questionBank.abstract, 15)
        };
        renderSection("verbal", current.verbal);
        renderSection("quantitative", current.quantitative);
        renderSection("abstract", current.abstract);
        document.getElementById('result').textContent = "";
        countdown = setInterval(() => {
          let minutes = Math.floor(totalSeconds / 60);
          let seconds = totalSeconds % 60;
          timerDisplay.textContent = `${minutes}:${seconds.toString().padStart(2, '0')}`;
          totalSeconds--;
          if (totalSeconds < 0) {
            clearInterval(countdown);
            document.getElementById("peacTest").requestSubmit();
          }
        }, 1000);
      }, 7000);
    });
  </script>
</body>
</html>
