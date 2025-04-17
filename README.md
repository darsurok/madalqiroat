# madalqiroat
Madalqiroat1

<!-- ВСТАВКА ТОЛЬКО В БЛОК <body> -->
<div class="progress">Тест 1 из 10</div>
<div id="testsContainer"></div>

<script>
  const tests = [
    {
      words: [
        { text: "Собака", correct: 1 },
        { text: "весело", correct: 3 },
        { text: "бегает", correct: 2 },
        { text: "по парку", correct: 4 }
      ],
      correctSentence: "Собака бегает весело по парку",
      translation: "The dog is running happily in the park"
    },
    {
      words: [
        { text: "Мы", correct: 1 },
        { text: "завтра", correct: 3 },
        { text: "в кино", correct: 4 },
        { text: "идем", correct: 2 }
      ],
      correctSentence: "Мы идем завтра в кино",
      translation: "We are going to the cinema tomorrow"
    },
    {
      words: [
        { text: "Солнце", correct: 1 },
        { text: "ярко", correct: 2 },
        { text: "светит", correct: 3 },
        { text: "на небе", correct: 4 }
      ],
      correctSentence: "Солнце ярко светит на небе",
      translation: "The sun is shining brightly in the sky"
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
        <input class="name-input" id="translationInput" value="${test.translation}" disabled style="margin-bottom: 10px;" />
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

    const wordsBox = document.getElementById('wordsBox');
    for (let i = wordsBox.children.length; i >= 0; i--) {
      wordsBox.appendChild(wordsBox.children[Math.random() * i | 0]);
    }
  }

  function initWordClick() {
    document.querySelectorAll('.word').forEach(word => {
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
    const words = [...document.querySelectorAll('.sentence-box .word')];

    const isCorrect = words.length === test.words.length &&
      words.every((word, index) =>
        parseInt(word.dataset.correct) === index + 1
      );

    const result = document.getElementById('result');
    result.textContent = isCorrect ?
      `Правильно! ✔️ "${test.correctSentence}"` :
      `Неправильно! ❌ Попробуйте еще раз`;
    result.className = `result ${isCorrect ? 'correct' : 'incorrect'}`;

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
    const name = document.getElementById('username').value || "Аноним";
    const sentence = [...document.querySelectorAll('.sentence-box .word')].map(w => w.textContent).join(' ');

    const payload = {
      username: name,
      message: sentence,
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
      document.getElementById('testsContainer').innerHTML = `
        <div class="test-container active">
          <div class="result correct">Данные успешно отправлены!</div>
          <a href="https://t.me/channel3" target="_blank" class="telegram-btn">Войти в группу Telegram</a>
        </div>
      `;
    }).catch(error => {
      console.error("Ошибка при отправке:", error);
      alert("Ошибка при отправке: " + error);
    });
  }

  window.onload = init;
</script>
