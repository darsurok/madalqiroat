# madalqiroat
Madalqiroat1
<button onclick="sendMessage()">Отправить сообщение</button>

<script>
  function sendMessage() {
    const url = 'ВСТАВЬ_ТУТ_URL_ТВОЕГО_APPS_SCRIPT';

    fetch(url, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify({
        text: 'Пользователь нажал кнопку на сайте!'
      })
    })
    .then(res => res.text())
    .then(res => {
      console.log('Ответ от скрипта:', res);
    })
    .catch(err => {
      console.error('Ошибка:', err);
    });
  }
</script>
