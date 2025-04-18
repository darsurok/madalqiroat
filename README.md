# madalqiroat
Madalqiroat1

<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>10 Тестов на Составление Предложений</title>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body { font-family: Arial, sans-serif; background: #f0f0f0; padding: 10px; }
    .test-container { max-width: 600px; margin: 0 auto 30px; background: white; padding: 15px; border-radius: 10px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); display: none; }
    .test-container.active { display: block; }
    .words-box, .sentence-box { background: #fff; border: 2px dashed #ccc; border-radius: 10px; padding: 15px; margin-bottom: 15px; min-height: 80px; display: flex; flex-wrap: wrap; gap: 8px; flex-direction: row-reverse; }
    .sentence-box { background: #e3f2fd; border: 2px solid #2196F3; }
    .word { background: #4CAF50; color: white; padding: 8px 12px; border-radius: 15px; cursor: pointer; user-select: none; transition: all 0.2s; font-size: 20px; }
    .readonly-word { background: #888 !important; cursor: default !important; }
    .check-btn { background: #2196F3; color: white; border: none; padding: 10px 20px; border-radius: 20px; cursor: pointer; margin: 5px 0; }
    .next-btn { background: #9C27B0; display: none; }
    .result { padding: 10px; font-weight: bold; text-align: center; }
    .correct { color: #2ecc71; }
    .incorrect { color: #e74c3c; }
    .progress { text-align: center; margin-bottom: 20px; font-size: 18px; }
    .name-input { width: 100%; padding: 10px; margin: 10px 0; border: 1px solid #ccc; border-radius: 10px; font-size: 16px; }
    .telegram-btn {
      display: inline-block;
      background: #2196F3;
      color: white;
      border: none;
      padding: 10px 20px;
      border-radius: 20px;
      text-decoration: none;
      font-size: 16px;
      cursor: pointer;
      margin-top: 10px;
    }
  </style>
</head>
<body>
  <div class="progress">Тест 1 из 10</div>
  <div id="testsContainer"></div>

  <script>
    const tests = [
  {
    words: [
      { text: "مَنْ", correct: 1 },
      { text: "هَذَا؟", correct: 2 },
      { text: "مُعَلِّمٌ", correct: 3 },
      { text: "مَنْ", correct: 4 },
      { text: "هَؤُلاَءِ؟", correct: 5 },
      { text: "مُعَلِّمُونَ", correct: 6 }
    ],
    correctSentence: "مَنْ هَذَا؟ - مُعَلِّمٌ. مَنْ هَؤُلاَءِ؟ - مُعَلِّمُونَ.",
    translation: "Кто это? - Учитель. Кто это? - Учителя."
  },
  {
    words: [
      { text: "مَنْ", correct: 1 },
      { text: "هَذِهِ؟", correct: 2 },
      { text: "تِلْمِيذَةٌ", correct: 3 },
      { text: "مَنْ", correct: 4 },
      { text: "هَؤُلاَءِ؟", correct: 5 },
      { text: "تِلْمِيذَاتٌ", correct: 6 }
    ],
    correctSentence: "مَنْ هَذِهِ؟ - تِلْمِيذَةٌ. مَنْ هَؤُلاَءِ؟ - تِلْمِيذَاتٌ.",
    translation: "Кто это? - Ученица. Кто это? - Ученицы."
  },
  {
    words: [
      { text: "هُوَ", correct: 1 },
      { text: "مُعَلِّمٌ", correct: 2 },
      { text: "هُمْ", correct: 3 },
      { text: "مُعَلِّمُونَ", correct: 4 }
    ],
    correctSentence: "هُوَ مُعَلِّمٌ. هُمْ مُعَلِّمُونَ.",
    translation: "Он учитель. Они учителя."
  },
  {
    words: [
      { text: "اَنْتَ", correct: 1 },
      { text: "تِلْمِيذٌ", correct: 2 },
      { text: "اَنْتُمْ", correct: 3 },
      { text: "تَلاَمِيذُ", correct: 4 }
    ],
    correctSentence: "اَنْتَ تِلْمِيذٌ. اَنْتُمْ تَلاَمِيذُ.",
    translation: "Ты ученик. Вы ученики."
  },
  {
    words: [
      { text: "هِىَ", correct: 1 },
      { text: "تِلْمِيذَةٌ", correct: 2 },
      { text: "هُنَّ", correct: 3 },
      { text: "تِلْمِيذَاتٌ", correct: 4 }
    ],
    correctSentence: "هِىَ تِلْمِيذَةٌ. هُنَّ تِلْمِيذَاتٌ.",
    translation: "Она ученица. Они ученицы."
  },
  {
    words: [
      { text: "اَنَا", correct: 1 },
      { text: "مُعَلِّمَةٌ", correct: 2 },
      { text: "نَحْنُ", correct: 3 },
      { text: "مُعَلِّمَاتٌ", correct: 4 }
    ],
    correctSentence: "اَنَا مُعَلِّمَةٌ. نَحْنُ مُعَلِّمَاتٌ.",
    translation: "Я учительница. Мы учительницы."
  },
  {
    words: [
      { text: "هَذَا", correct: 1 },
      { text: "الرَّجُلُ", correct: 2 },
      { text: "مُعَلِّمٌ", correct: 3 },
      { text: "هَؤُلاَءِ", correct: 4 },
      { text: "الرِّجَالُ", correct: 5 },
      { text: "مُعَلِّمُونَ", correct: 6 }
    ],
    correctSentence: "هَذَا الرَّجُلُ مُعَلِّمٌ. هَؤُلاَءِ الرِّجَالُ مُعَلِّمُونَ.",
    translation: "Этот мужчина учитель. Эти мужчины учителя."
  },
  {
    words: [
      { text: "هَذِهِ", correct: 1 },
      { text: "الْمَرْأَةُ", correct: 2 },
      { text: "مُعَلِّمَةٌ", correct: 3 },
      { text: "هَؤُلاَءِ", correct: 4 },
      { text: "النِّسَاءُ", correct: 5 },
      { text: "مُعَلِّمَاتٌ", correct: 6 }
    ],
    correctSentence: "هَذِهِ الْمَرْأَةُ مُعَلِّمَةٌ. هَؤُلاَءِ النِّسَاءُ مُعَلِّمَاتٌ.",
    translation: "Эта женщина учительница. Эти женщины учительницы."
  },
  {
    words: [
      { text: "مَنْ", correct: 1 },
      { text: "هُوَ؟", correct: 2 },
      { text: "مَنْ", correct: 3 },
      { text: "هِىَ؟", correct: 4 }
    ],
    correctSentence: "مَنْ هُوَ؟ مَنْ هِىَ؟",
    translation: "Кто он? Кто она?"
  },
  {
    words: [
      { text: "مَنْ", correct: 1 },
      { text: "اَنْتَ؟", correct: 2 },
      { text: "مَنْ", correct: 3 },
      { text: "اَنْتُمْ؟", correct: 4 }
    ],
    correctSentence: "مَنْ اَنْتَ؟ مَنْ اَنْتُمْ؟",
    translation: "Кто ты? Кто вы?"
  },
  {
    words: [
      { text: "مَنْ", correct: 1 },
      { text: "هُمْ؟", correct: 2 }
    ],
    correctSentence: "مَنْ هُمْ؟",
    translation: "Кто они?"
  }
    ];

    let currentTest = 0;

    function init() {
      document.querySelector('.progress').textContent = `Тест ${currentTest + 1} из ${tests.length}`;
      createTest(currentTest);
      initWordClick();
    }

    function createTest(index) {
      const container = document.getElementById('testsContainer');
      container.innerHTML = '';

      const test = tests[index];

      const testHTML = `
        <div class="test-container active">
          <div class="sentence-box" id="answerArea"></div>
          <div class="sentence-box" id="sentenceArea"></div>
          <div class="words-box" id="wordsBox">
            ${test.words.map(word => `
              <div class="word" data-correct="${word.correct}">${word.text}</div>
            `).join('')}
          </div>
          <button class="check-btn" onclick="checkTest()">Проверить</button>
          <button class="check-btn next-btn" onclick="nextTest()">Следующий тест →</button>
          <div class="result" id="result"></div>
        </div>
      `;
      container.innerHTML = testHTML;

      // Добавление слов из перевода
      const answerArea = document.getElementById('answerArea');
      test.translation.split(" ").forEach(word => {
        const span = document.createElement('div');
        span.className = 'word readonly-word';
        span.textContent = word;
        answerArea.appendChild(span);
      });

      const wordsBox = document.getElementById('wordsBox');
      for (let i = wordsBox.children.length; i >= 0; i--) {
        wordsBox.appendChild(wordsBox.children[Math.random() * i | 0]);
      }
    }

    function initWordClick() {
      document.querySelectorAll('.word').forEach(word => {
        if (word.classList.contains('readonly-word')) return;
        word.addEventListener('click', () => {
          const sentenceBox = document.getElementById('sentenceArea');
          const wordsBox = document.getElementById('wordsBox');
          if (word.parentElement === wordsBox) {
            sentenceBox.appendChild(word);
          } else {
            wordsBox.appendChild(word);
          }
        });
      });
    }

    function checkTest() {
      const test = tests[currentTest];
      const words = [...document.querySelectorAll('.sentence-box#sentenceArea .word')];

      const isCorrect = words.length === test.words.length &&
        words.every((word, index) =>
          parseInt(word.dataset.correct) === index + 1
        );

      const result = document.getElementById('result');
      result.textContent = isCorrect ?
        `Правильно! ✔️ "${test.correctSentence}"` :
        'Неправильно! ❌ Попробуйте еще раз';
      result.className = isCorrect ? 'result correct' : 'result incorrect';

      if (isCorrect) {
        document.querySelector('.next-btn').style.display = 'inline-block';
      }
    }

    function nextTest() {
      if (currentTest < tests.length - 1) {
        currentTest++;
        document.querySelector('.progress').textContent = `Тест ${currentTest + 1} из ${tests.length}`;
        createTest(currentTest);
        initWordClick();
      } else {
        document.getElementById('testsContainer').innerHTML = `
          <div class="test-container active">
            <div class="result correct">Все тесты пройдены! Молодец!</div>
            <input class="name-input" id="username" placeholder="Введите ваше имя">
            <button class="check-btn" onclick="sendToMessenger()">Отправить в мессенджер</button>
          </div>
        `;
        document.querySelector('.progress').style.display = 'none';
      }
    }

    function sendToMessenger() {
  const name = document.getElementById('username').value.trim();

  if (!name) {
    alert("Пожалуйста, введите ваше имя перед отправкой.");
    return;
  }

  const payload = {
    username: name,
    text: `Пользователь прошёл тест!\nИмя: ${name}`,
    channel: 'channel3'
  };

  fetch('https://script.google.com/macros/s/AKfycbxKtfqb4Tx0gGeDFnTtH3yA7ZoU0N_yHz6qTW066T_r9rGHsVuuYrwbhT4gkJ2B-yXK/exec', {
    method: 'POST',
    mode: 'no-cors',
    body: JSON.stringify(payload),
    headers: {
      'Content-Type': 'application/json'
    }
  }).then(() => {
    document.getElementById('testsContainer').innerHTML = 
      `<div class="test-container active">
        <div class="result correct">Данные успешно отправлены!</div>
        <a href="https://sites.google.com/view/mabdalqiroat" class="telegram-btn">Начать заново</a>
      </div>`;
  }).catch(error => {
    console.error("Ошибка при отправке:", error);
    alert("Ошибка при отправке: " + error);
  });
}

    window.onload = init;
  </script>
</body>
</html>
