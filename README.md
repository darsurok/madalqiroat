# madalqiroat
Madalqiroat1
<button onclick="sendMessage()">Отправить сообщение</button>

<script>
  function sendMessage() {
    const url = 'https://script.google.com/macros/s/AKfycbw5mZVbH59LWOEgSZYRg3q_wvqHuec90-Rf2lKIKt855nnlRPoIuWxItYgJLP9LEI_o/exec';

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
