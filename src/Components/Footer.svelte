<footer>
  <div class="footer-content">
    <div class="logo">Подорож Україною</div>
    <nav class="menu">
      <!-- <ul>
        <li><a href="#">Про проєкт</a></li>
        <li><a href="#">Карта</a></li>
        <li><a href="#">Статистика</a></li>
      </ul> -->
    </nav>
    <div class="description">
      <p>Хараїм Юлія</p>
      <p>ЛНАМ, кафедра ГД</p>
      <p>2024 рік</p>
    </div>
  </div>
</footer>

<style>
  footer {
    background-color: #004638;
    font-family: 'Manrope';
    color: #C7DDDC;
    padding: 20px;
    text-align: center;
    bottom: 0;
    height: 110px;
    display: flex;
    align-items: center; /* Вирівнюємо елементи по вертикалі */
  }

  .footer-content {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 100%; /* Додано */
    max-width: 1200px; /* Додано */
    margin: 0 auto; /* Додано */
  }

  .logo {
    font-size: 25px;
    font-family: sans-serif;
    font-weight: bold;
    width: 200px;
  }


  .description {
    text-align: right;
    color: #C7DDDC;
    font-weight: 300;
    width: 200px;
    text-align: right;
    font-size: 17px;
    line-height: 150%;
  }

  .description p {
    margin: 4px 0;
  }
</style>
