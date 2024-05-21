<header>
    <div class="header-content">
      <div class="logo">Подорож Україною</div>
      <nav class="menu">
        <ul>
          <li><a href="#">Про проєкт</a></li>
          <li><a href="#">Карта</a></li>
          <li><a href="#">Статистика</a></li>
          <li><a href="#">Виконала</a></li>
         
        </ul>
      </nav>
    </div>
  </header>

<style>

 /* Стилі для заголовка */
header {
  background-color: #000000;
  font-family: "Montserrat", sans-serif;;
  color: #fff;
  padding: 20px;
}

.header-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* Стилі для логотипу */
.logo {
  font-size: 24px;
  font-weight: bold;
  width: 200px;
}

/* Стилі для меню */
.menu ul {
  list-style-type: none;
  padding: 0;
}

.menu ul li {
  display: inline;
  margin-right: 20px;
}

.menu ul li:last-child {
  margin-right: 0; /* Видаляємо відступ для останнього пункту меню */
}

.menu ul li a {
  color: #fff;
  text-decoration: none;
}
</style>