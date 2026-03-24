<!DOCTYPE html>
<html lang="ru">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Викторина и Х и О</title>
  <h1>Викторина и Х и О</h1>
  <section id="math">
    <button onclick="openMath()">Математика</button>
    <div id="math-percent"></div>
    <div id="math-level"></div>
    <div id="math-progress"></div>
    <div id="math-question"></div>

    <div id="math-answers"></div>

    <button onclick="startMath()">🔄 Начать заново</button>

    <div id="math-result"></div>
  </section>
  <style>
    body {
      font-family: Arial;
      background: #f0f0f0;
      padding: 20px;
    }

    nav {
      margin-bottom: 20px;
    }

    button.tab {
      padding: 10px 20px;
      margin-right: 5px;
      cursor: pointer;
      background: #2196f3;
      color: #fff;
      border: none;
      border-radius: 5px;
    }

    button.tab:hover {
      background: #1976d2;
    }

    section {
      display: none;
    }

    section.active {
      display: block;
    }

    #question {
      font-size: 1.2em;
      margin-bottom: 15px;
    }

    #answers {
      display: flex;
      flex-direction: column;
      gap: 10px;
      margin-bottom: 15px;
    }

    .answer {
      padding: 10px;
      border-radius: 5px;
      border: 1px solid #ccc;
      background: #fff;
      cursor: pointer;
      transition: 0.3s;
    }

    .answer.correct {
      background: #4caf50;
      color: #fff;
    }

    .answer.wrong {
      background: #f44336;
      color: #fff;
    }

    #result {
      font-weight: bold;
      min-height: 20px;
      margin-bottom: 10px;
    }

    #progress {
      margin-bottom: 10px;
    }

    #tic-tac-toe {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      gap: 5px;
      margin-top: 20px;
    }

    .ttt-cell {
      width: 100px;
      height: 100px;
      background: #fff;
      border: 1px solid #000;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 2em;
      cursor: pointer;
    }

    .ttt-cell.win {
      background: #4caf50;
      color: #fff;
    }

    #ttt-result {
      margin-top: 10px;
      font-weight: bold;
    }

    body {
      font-family: Arial, sans-serif;
      background: #f5f7fb;
      margin: 0;
      padding: 20px;
    }

    /* Кнопки вкладок */
    button.tab {
      padding: 16px 34px;
      margin: 6px;
      cursor: pointer;
      background: linear-gradient(135deg, #4facfe, #2196f3);
      color: #fff;
      border: none;
      border-radius: 12px;
      font-size: 18px;
      font-weight: bold;
      transition: 0.3s;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
    }

    button.tab:hover {
      transform: translateY(-2px);
      box-shadow: 0 6px 14px rgba(0, 0, 0, 0.2);
    }

    /* Кнопки ответов */
    .answer {
      display: block;
      width: 100%;
      max-width: 400px;
      margin: 10px auto;
      padding: 16px;
      font-size: 18px;
      border-radius: 10px;
      border: none;
      background: #ffffff;
      cursor: pointer;
      transition: 0.3s;
      box-shadow: 0 3px 8px rgba(0, 0, 0, 0.1);
    }

    .answer:hover {
      background: #e3f2fd;
      transform: scale(1.03);
    }

    /* Правильный / неправильный ответ */
    .correct {
      background: #4caf50 !important;
      color: white;
    }

    .wrong {
      background: #f44336 !important;
      color: white;
    }

    /* Общие кнопки */
    button {
      font-size: 18px;
      padding: 14px 24px;
      border-radius: 10px;
    }

    /* Контент */
    section {
      margin-top: 20px;
      padding: 20px;
      background: #fff;
      border-radius: 16px;
      box-shadow: 0 6px 18px rgba(0, 0, 0, 0.1);
    }

    /* Текст вопросов */
    #question,
    #math-question {
      font-size: 22px;
      margin-bottom: 15px;
    }

    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #e3f2fd, #f5f7fb);
      margin: 0;
      padding: 20px;
    }

    section {
      max-width: 500px;
      margin: auto;
      background: #fff;
      padding: 25px;
      border-radius: 16px;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
      text-align: center;
    }

    button.tab {
      padding: 15px 30px;
      margin: 5px;
      font-size: 18px;
      border-radius: 10px;
      border: none;
      background: linear-gradient(135deg, #2196f3, #4facfe);
      color: white;
      cursor: pointer;
      transition: 0.3s;
    }

    button.tab:hover {
      transform: scale(1.05);
    }

    /* Варианты ответов */
    .answer {
      display: block;
      width: 100%;
      margin: 10px 0;
      padding: 15px;
      font-size: 18px;
      border-radius: 10px;
      border: none;
      background: #ffffff;
      cursor: pointer;
      transition: 0.3s;
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    }

    .answer:hover {
      transform: scale(1.03);
      background: #e3f2fd;
    }

    .correct {
      background: #4caf50 !important;
      color: white;
    }

    .wrong {
      background: #f44336 !important;
      color: white;
    }

    #math-question {
      font-size: 22px;
      margin: 20px 0;
    }

    #math-progress,
    #math-level {
      font-size: 16px;
      margin-bottom: 10px;
    }

    button.answer {
      width: 100%;
      padding: 20px;
      font-size: 20px;
      margin: 10px 0;
      border-radius: 12px;
    }
  </style>
</head>

<body>

  <nav>
    <button class="tab" onclick="showTab('quiz')">Викторина</button>
    <button class="tab" onclick="showTab('xo')">Х и О</button>
  </nav>

  <section id="quiz" class="active">
    <div id="question"></div>
    <div id="answers"></div>
    <div id="result"></div>
    <div id="progress"></div>
  </section>

  <section id="xo">
    <button id="start-ttt">Начать Х и О</button>
    <div id="tic-tac-toe"></div>
    <div id="ttt-result"></div>
  </section>

  <script>
    let correctMath = 0;
    let totalMath = 0;
    // ===== Навигация по вкладкам =====
    function showTab(tabId) {
      document.querySelectorAll('section').forEach(sec => sec.classList.remove('active'));
      document.getElementById(tabId).classList.add('active');
    }

    // ===== 100 Логических вопросов =====
    const allQuestions = [
      // УРОВЕНЬ 1
      { q: "Что тяжелее: 1 кг железа или 1 кг ваты?", a: ["Железо", "Вата", "Одинаково"], c: 2, l: 1 },
      { q: "Сколько будет 2+2?", a: ["3", "4", "5"], c: 1, l: 1 },
      { q: "Сколько дней в неделе?", a: ["5", "7", "10"], c: 1, l: 1 },
      { q: "У тебя есть 3 яблока, ты взял 2. Сколько у тебя?", a: ["1", "2", "3"], c: 1, l: 1 },
      { q: "Что идёт, но не двигается?", a: ["Часы", "Время", "Дорога"], c: 2, l: 1 },
      { q: "Что можно сломать, не трогая?", a: ["Обещание", "Стекло", "Камень"], c: 0, l: 1 },
      { q: "Я всегда впереди тебя, но ты не можешь меня увидеть. Что это?", a: ["Будущее", "Воздух", "Свет"], c: 0, l: 1 },
      { q: "Чем больше берёшь, тем больше становится?", a: ["Долг", "Яма", "Деньги"], c: 1, l: 1 },
      { q: "Что имеет ключи, но не открывает двери?", a: ["Карта", "Пианино", "Код"], c: 1, l: 1 },
      { q: "Что можно увидеть с закрытыми глазами?", a: ["Сон", "Темнота", "Свет"], c: 0, l: 1 },
      // УРОВЕНЬ 2
      { q: "Что увеличивается, если перевернуть?", a: ["6", "9", "0"], c: 0, l: 2 },
      { q: "Что всегда перед тобой, но ты не видишь?", a: ["Будущее", "Тень", "Свет"], c: 0, l: 2 },
      { q: "Без чего не испечь хлеб?", a: ["Мука", "Огонь", "Печь"], c: 1, l: 2 },
      { q: "Что можно держать, не касаясь руками?", a: ["Слово", "Дыхание", "Обещание"], c: 2, l: 2 },
      { q: "У кого нет ног, но ходит?", a: ["Часы", "Река", "Облако"], c: 1, l: 2 },
      { q: "Что может летать без крыльев?", a: ["Самолет", "Время", "Слон"], c: 1, l: 2 },
      { q: "Чем больше отнимаешь, тем больше оно?", a: ["Долг", "Яма", "Деньги"], c: 1, l: 2 },
      { q: "Что можно сломать только словом?", a: ["Обещание", "Стекло", "Дерево"], c: 0, l: 2 },
      { q: "Что можно открыть, но нельзя закрыть?", a: ["Книга", "Секрет", "Письмо"], c: 1, l: 2 },
      { q: "Что принадлежит тебе, но пользуются им чаще другие?", a: ["Имя", "Телефон", "Рюкзак"], c: 0, l: 2 },
      // УРОВЕНЬ 3
      { q: "Что всегда с тобой, но его нельзя увидеть?", a: ["Тень", "Будущее", "Воздух"], c: 0, l: 3 },
      { q: "Что можно поймать, но нельзя бросить?", a: ["Холод", "Слово", "Мяч"], c: 1, l: 3 },
      { q: "Что растет, но никогда не живет?", a: ["Возраст", "Дерево", "Река"], c: 0, l: 3 },
      { q: "Что никогда не возвращается?", a: ["Время", "Мяч", "Воздух"], c: 0, l: 3 },
      { q: "Что всегда идет, но не движется?", a: ["Часы", "Река", "Дорога"], c: 0, l: 3 },
      { q: "Что нельзя использовать, пока оно целое?", a: ["Яйцо", "Книга", "Телефон"], c: 0, l: 3 },
      { q: "Что можно услышать, но нельзя увидеть?", a: ["Эхо", "Свет", "Тень"], c: 0, l: 3 },
      { q: "Что имеет зубы, но не ест?", a: ["Пила", "Человек", "Слон"], c: 0, l: 3 },
      { q: "Что растет, когда его берешь?", a: ["Яма", "Долг", "Деньги"], c: 0, l: 3 },
      { q: "Что можно тронуть, но не увидеть?", a: ["Тень", "Воздух", "Любовь"], c: 1, l: 3 },
      // УРОВЕНЬ 4
      { q: "Что становится мокрым, когда сохнет?", a: ["Полотенце", "Свет", "Вода"], c: 0, l: 4 },
      { q: "У кого есть сердце, но нет крови?", a: ["Арбуз", "Человек", "Река"], c: 0, l: 4 },
      { q: "Что можно разбить, но не тронув?", a: ["Обещание", "Стекло", "Камень"], c: 0, l: 4 },
      { q: "Что можно увидеть, но нельзя потрогать?", a: ["Тень", "Стена", "Дверь"], c: 0, l: 4 },
      { q: "Что бежит, но никогда не устает?", a: ["Время", "Собака", "Река"], c: 0, l: 4 },
      { q: "Что всегда меняется, но никогда не стареет?", a: ["Время", "Человек", "Солнце"], c: 0, l: 4 },
      { q: "Что имеет корни, но не дерево?", a: ["Гора", "Дерево", "Камень"], c: 0, l: 4 },
      { q: "Что не живое, но может расти?", a: ["Кристалл", "Река", "Человек"], c: 0, l: 4 },
      { q: "Что всегда говорит правду, но никогда не говорит?", a: ["Зеркало", "Солнце", "Часы"], c: 0, l: 4 },
      { q: "Что можно найти в конце радуги?", a: ["Сокровище", "Свет", "Дождь"], c: 0, l: 4 },
      // ===== УРОВЕНЬ 5 =====
      { q: "Что идет вверх и вниз, но всегда остается на месте?", a: ["Лестница", "Лифт", "Дорога"], c: 0, l: 5 },
      { q: "Что имеет руки, но не может работать?", a: ["Часы", "Робот", "Человек"], c: 0, l: 5 },
      { q: "Что растет без корней?", a: ["Гриб", "Дерево", "Камень"], c: 0, l: 5 },
      { q: "Что не говорит, но отвечает на вопросы?", a: ["Эхо", "Робот", "Собака"], c: 0, l: 5 },
      { q: "Что можно хранить, но нельзя увидеть?", a: ["Секрет", "Книга", "Сокровище"], c: 0, l: 5 },
      { q: "Что всегда перед глазами, но невидимо?", a: ["Будущее", "Тень", "Свет"], c: 0, l: 5 },
      { q: "Что можно открыть, но нельзя закрыть?", a: ["Секрет", "Дверь", "Книга"], c: 0, l: 5 },
      { q: "Что можно видеть, но нельзя трогать?", a: ["Тень", "Воздух", "Свет"], c: 0, l: 5 },
      { q: "Что можно поймать, но нельзя удержать?", a: ["Слово", "Мяч", "Река"], c: 0, l: 5 },
      { q: "Что имеет глаза, но не видит?", a: ["Картошка", "Человек", "Слон"], c: 0, l: 5 },
      // ===== УРОВЕНЬ 6 =====
      { q: "Что нельзя съесть на завтрак?", a: ["Обед", "Яйцо", "Хлеб"], c: 0, l: 6 },
      { q: "Что никогда не бывает мокрым?", a: ["Тень", "Вода", "Дождь"], c: 0, l: 6 },
      { q: "Что всегда увеличивается, но никогда не уменьшается?", a: ["Возраст", "Долг", "Сумма"], c: 0, l: 6 },
      { q: "Что можно увидеть, но нельзя услышать?", a: ["Тень", "Свет", "Эхо"], c: 0, l: 6 },
      { q: "Что растет, но не дышит?", a: ["Кристалл", "Человек", "Река"], c: 0, l: 6 },
      { q: "Что имеет зубы, но не ест?", a: ["Пила", "Слон", "Человек"], c: 0, l: 6 },
      { q: "Что можно держать в руках, но не увидеть?", a: ["Воздух", "Книга", "Свет"], c: 0, l: 6 },
      { q: "Что всегда возвращается, но никогда не приходит?", a: ["Эхо", "Мяч", "Ветер"], c: 0, l: 6 },
      { q: "Что можно увидеть с закрытыми глазами?", a: ["Сон", "Темнота", "Свет"], c: 0, l: 6 },
      { q: "Что растет вверх, но не дерево?", a: ["Дым", "Растение", "Человек"], c: 0, l: 6 },
      // ===== УРОВЕНЬ 7 =====
      { q: "Что не имеет начала и конца?", a: ["Кольцо", "Река", "Дорога"], c: 0, l: 7 },
      { q: "Что можно сломать, не касаясь?", a: ["Обещание", "Стекло", "Камень"], c: 0, l: 7 },
      { q: "Что всегда с тобой, но не видно?", a: ["Тень", "Будущее", "Воздух"], c: 0, l: 7 },
      { q: "Что растет, но не живое?", a: ["Возраст", "Гора", "Река"], c: 0, l: 7 },
      { q: "Что можно открыть, но нельзя закрыть?", a: ["Секрет", "Дверь", "Книга"], c: 0, l: 7 },
      { q: "Что летает без крыльев?", a: ["Время", "Птица", "Самолет"], c: 0, l: 7 },
      { q: "Что всегда идет, но не движется?", a: ["Часы", "Река", "Дорога"], c: 0, l: 7 },
      { q: "Что можно услышать, но нельзя увидеть?", a: ["Эхо", "Свет", "Тень"], c: 0, l: 7 },
      { q: "Что растет без корней?", a: ["Гриб", "Дерево", "Камень"], c: 0, l: 7 },
      { q: "Что можно поймать, но нельзя удержать?", a: ["Слово", "Мяч", "Река"], c: 0, l: 7 },
      // ===== УРОВЕНЬ 8 =====
      { q: "Что всегда перед тобой, но невидимо?", a: ["Будущее", "Тень", "Свет"], c: 0, l: 8 },
      { q: "Что можно сломать словом?", a: ["Обещание", "Стекло", "Дерево"], c: 0, l: 8 },
      { q: "Что никогда не возвращается?", a: ["Время", "Мяч", "Воздух"], c: 0, l: 8 },
      { q: "Что растет, когда его берешь?", a: ["Яма", "Долг", "Деньги"], c: 0, l: 8 },
      { q: "Что можно держать, но не трогать?", a: ["Слово", "Дыхание", "Обещание"], c: 0, l: 8 },
      { q: "Что можно увидеть с закрытыми глазами?", a: ["Сон", "Темнота", "Свет"], c: 0, l: 8 },
      { q: "Что растет вверх, но не дерево?", a: ["Дым", "Растение", "Человек"], c: 0, l: 8 },
      { q: "Что всегда увеличивается, но не уменьшается?", a: ["Возраст", "Долг", "Сумма"], c: 0, l: 8 },
      { q: "Что идет вверх и вниз, но остается на месте?", a: ["Лестница", "Лифт", "Дорога"], c: 0, l: 8 },
      { q: "Что имеет руки, но не работает?", a: ["Часы", "Робот", "Человек"], c: 0, l: 8 },
      // ===== УРОВЕНЬ 9 =====
      { q: "Что нельзя съесть на завтрак?", a: ["Обед", "Яйцо", "Хлеб"], c: 0, l: 9 },
      { q: "Что растет без корней?", a: ["Гриб", "Дерево", "Камень"], c: 0, l: 9 },
      { q: "Что нельзя использовать, пока оно целое?", a: ["Яйцо", "Книга", "Телефон"], c: 0, l: 9 },
      { q: "Что можно увидеть, но нельзя потрогать?", a: ["Тень", "Стена", "Дверь"], c: 0, l: 9 },
      { q: "Что всегда меняется, но никогда не стареет?", a: ["Время", "Человек", "Солнце"], c: 0, l: 9 },
      { q: "Что имеет корни, но не дерево?", a: ["Гора", "Дерево", "Камень"], c: 0, l: 9 },
      { q: "Что не живое, но растет?", a: ["Кристалл", "Река", "Человек"], c: 0, l: 9 },
      { q: "Что всегда говорит правду, но не говорит?", a: ["Зеркало", "Солнце", "Часы"], c: 0, l: 9 },
      { q: "Что можно найти в конце радуги?", a: ["Сокровище", "Свет", "Дождь"], c: 0, l: 9 },
      { q: "Что растет, когда его берешь?", a: ["Яма", "Долг", "Деньги"], c: 0, l: 9 },
      // ===== УРОВЕНЬ 10 =====
      { q: "Что всегда впереди, но его нельзя увидеть?", a: ["Будущее", "Тень", "Свет"], c: 0, l: 10 },
      { q: "Что можно поймать, но нельзя удержать?", a: ["Слово", "Мяч", "Река"], c: 0, l: 10 },
      { q: "Что нельзя увидеть, но оно вокруг?", a: ["Воздух", "Тень", "Свет"], c: 0, l: 10 },
      { q: "Что растет вверх, но не дерево?", a: ["Дым", "Растение", "Человек"], c: 0, l: 10 },
      { q: "Что можно открыть, но нельзя закрыть?", a: ["Секрет", "Дверь", "Книга"], c: 0, l: 10 },
      { q: "Что всегда увеличивается, но не уменьшается?", a: ["Возраст", "Долг", "Сумма"], c: 0, l: 10 },
      { q: "Что всегда идет, но не движется?", a: ["Часы", "Река", "Дорога"], c: 0, l: 10 },
      { q: "Что можно увидеть с закрытыми глазами?", a: ["Сон", "Темнота", "Свет"], c: 0, l: 10 },
      { q: "Что можно сломать, не трогая?", a: ["Обещание", "Стекло", "Камень"], c: 0, l: 10 },
      { q: "Что имеет глаза, но не видит?", a: ["Картошка", "Человек", "Слон"], c: 0, l: 10 },


    ];

    // ===== Переменные викторины =====
    let current = 0, score = 0, level = 1, questions = [], usedQuestions = [];

    // ===== Функции викторины =====
    function shuffle(array) { for (let i = array.length - 1; i > 0; i--) { let j = Math.floor(Math.random() * (i + 1));[array[i], array[j]] = [array[j], array[i]]; } return array; }
    function getQuestions(level) {
      let filtered = allQuestions.filter(q => q.l === level).filter(q => !usedQuestions.includes(q.q));
      let selected = shuffle(filtered).slice(0, 10);
      selected.forEach(q => usedQuestions.push(q.q));
      return selected;
    }
    function startGame() { current = 0; score = 0; level = 1; usedQuestions = []; questions = getQuestions(level); loadQuestion(); }
    function loadQuestion() {
      const q = questions[current]; document.getElementById("question").textContent = "Уровень " + level + ": " + q.q;
      const answers = document.getElementById("answers"); answers.innerHTML = "";
      q.a.forEach((ans, i) => { const btn = document.createElement("button"); btn.textContent = ans; btn.className = "answer"; btn.onclick = () => checkAnswer(i, btn); answers.appendChild(btn); });
      document.getElementById("progress").textContent = `Вопрос ${current + 1} из ${questions.length}`; document.getElementById("result").textContent = "";
    }
    function checkAnswer(i, btn) {
      const q = questions[current]; Array.from(document.getElementById("answers").children).forEach((b, idx) => { b.disabled = true; if (idx === q.c) b.classList.add("correct"); else if (idx === i) b.classList.add("wrong"); });
      const result = document.getElementById("result"); if (i === q.c) { score++; result.textContent = "✅ Правильно"; } else result.textContent = "❌ Неправильно";
      current++; setTimeout(() => { if (current < questions.length) loadQuestion(); else nextLevel(); }, 700);
    }
    function nextLevel() {
      level++; if (level > 10) { document.getElementById("question").textContent = "🏆 Викторина завершена!"; document.getElementById("answers").innerHTML = ""; document.getElementById("result").textContent = "Результат: " + score; document.getElementById("progress").textContent = ""; return; }
      document.getElementById("question").textContent = `Уровень ${level - 1} пройден!`; document.getElementById("answers").innerHTML = "";
      const btn = document.createElement("button"); btn.textContent = "Следующий уровень"; btn.onclick = () => { current = 0; questions = getQuestions(level); loadQuestion(); }; document.getElementById("answers").appendChild(btn);
    }

    // ===== Игра Х и О =====
    const ttt = document.getElementById("tic-tac-toe"); const tttResult = document.getElementById("ttt-result"); let board = ["", "", "", "", "", "", "", "", ""]; let turn = "X";
    function startTTT() { board = ["", "", "", "", "", "", "", "", ""]; tttResult.textContent = ""; ttt.innerHTML = ""; ttt.style.display = "grid"; for (let i = 0; i < 9; i++) { const cell = document.createElement("div"); cell.className = "ttt-cell"; cell.dataset.idx = i; cell.onclick = () => tttClick(i, cell); ttt.appendChild(cell); } }
    function tttClick(i, cell) { if (board[i] !== "") return; board[i] = turn; cell.textContent = turn; if (checkWin(turn)) { highlightWin(turn); tttResult.textContent = turn + " выиграл!"; disableBoard(); return; } if (board.every(c => c !== "")) { tttResult.textContent = "Ничья!"; return; } turn = turn === "X" ? "O" : "X"; }
    function checkWin(p) { const wins = [[0, 1, 2], [3, 4, 5], [6, 7, 8], [0, 3, 6], [1, 4, 7], [2, 5, 8], [0, 4, 8], [2, 4, 6]]; return wins.some(line => line.every(idx => board[idx] === p)); }
    function highlightWin(p) { const wins = [[0, 1, 2], [3, 4, 5], [6, 7, 8], [0, 3, 6], [1, 4, 7], [2, 5, 8], [0, 4, 8], [2, 4, 6]]; wins.forEach(line => { if (line.every(idx => board[idx] === p)) { line.forEach(idx => ttt.children[idx].classList.add("win")); } }); }
    function disableBoard() { Array.from(ttt.children).forEach(c => c.onclick = null); }
    document.getElementById("start-ttt").onclick = startTTT;

    // старт викторины
    startGame();
  </script>
  <button class="tab" onclick="showTab('math')">Математика</button>
  <section id="math">
    <div id="math-question"></div>
    <div id="math-answers"></div>
    <div id="math-result"></div>
    <div id="math-progress"></div>
  </section>
  <script>
    // ===== МАТЕМАТИЧЕСКИЕ ВОПРОСЫ (100 ШТУК, 10 УРОВНЕЙ) =====
    const mathQuestions = [
      // УРОВЕНЬ 1
      { q: "1 + 1 = ?", a: ["1", "2", "3"], c: 1, l: 1 },
      { q: "2 + 2 = ?", a: ["3", "4", "5"], c: 1, l: 1 },
      { q: "3 + 1 = ?", a: ["3", "4", "5"], c: 1, l: 1 },
      { q: "5 - 2 = ?", a: ["2", "3", "4"], c: 1, l: 1 },
      { q: "6 - 3 = ?", a: ["2", "3", "4"], c: 1, l: 1 },
      { q: "2 + 3 = ?", a: ["4", "5", "6"], c: 1, l: 1 },
      { q: "7 - 5 = ?", a: ["1", "2", "3"], c: 1, l: 1 },
      { q: "4 + 1 = ?", a: ["4", "5", "6"], c: 1, l: 1 },
      { q: "8 - 6 = ?", a: ["1", "2", "3"], c: 1, l: 1 },
      { q: "2 + 5 = ?", a: ["6", "7", "8"], c: 1, l: 1 },

      // УРОВЕНЬ 2
      { q: "10 - 4 = ?", a: ["5", "6", "7"], c: 1, l: 2 },
      { q: "3 × 2 = ?", a: ["5", "6", "7"], c: 1, l: 2 },
      { q: "8 ÷ 2 = ?", a: ["3", "4", "5"], c: 1, l: 2 },
      { q: "7 + 2 = ?", a: ["8", "9", "10"], c: 1, l: 2 },
      { q: "9 - 3 = ?", a: ["5", "6", "7"], c: 1, l: 2 },
      { q: "2 × 4 = ?", a: ["6", "8", "10"], c: 1, l: 2 },
      { q: "6 ÷ 3 = ?", a: ["1", "2", "3"], c: 1, l: 2 },
      { q: "5 + 5 = ?", a: ["9", "10", "11"], c: 1, l: 2 },
      { q: "12 - 5 = ?", a: ["6", "7", "8"], c: 1, l: 2 },
      { q: "4 × 2 = ?", a: ["6", "8", "10"], c: 1, l: 2 },

      // УРОВЕНЬ 3
      { q: "15 - 7 = ?", a: ["6", "7", "8"], c: 2, l: 3 },
      { q: "3 × 4 = ?", a: ["10", "11", "12"], c: 2, l: 3 },
      { q: "20 ÷ 5 = ?", a: ["3", "4", "5"], c: 1, l: 3 },
      { q: "9 + 6 = ?", a: ["14", "15", "16"], c: 1, l: 3 },
      { q: "18 - 9 = ?", a: ["8", "9", "10"], c: 1, l: 3 },
      { q: "6 × 3 = ?", a: ["16", "18", "20"], c: 1, l: 3 },
      { q: "24 ÷ 6 = ?", a: ["3", "4", "5"], c: 1, l: 3 },
      { q: "7 + 8 = ?", a: ["14", "15", "16"], c: 1, l: 3 },
      { q: "13 - 6 = ?", a: ["6", "7", "8"], c: 1, l: 3 },
      { q: "5 × 5 = ?", a: ["20", "25", "30"], c: 1, l: 3 },

      // УРОВЕНЬ 4
      { q: "12 × 2 = ?", a: ["22", "24", "26"], c: 1, l: 4 },
      { q: "36 ÷ 6 = ?", a: ["5", "6", "7"], c: 1, l: 4 },
      { q: "14 + 9 = ?", a: ["22", "23", "24"], c: 1, l: 4 },
      { q: "25 - 8 = ?", a: ["16", "17", "18"], c: 1, l: 4 },
      { q: "7 × 3 = ?", a: ["20", "21", "22"], c: 1, l: 4 },
      { q: "40 ÷ 5 = ?", a: ["6", "7", "8"], c: 2, l: 4 },
      { q: "18 + 7 = ?", a: ["24", "25", "26"], c: 1, l: 4 },
      { q: "30 - 12 = ?", a: ["16", "18", "20"], c: 1, l: 4 },
      { q: "9 × 4 = ?", a: ["32", "36", "40"], c: 1, l: 4 },
      { q: "16 ÷ 4 = ?", a: ["3", "4", "5"], c: 1, l: 4 },

      // УРОВЕНЬ 5
      { q: "11 × 3 = ?", a: ["33", "30", "36"], c: 0, l: 5 },
      { q: "48 ÷ 6 = ?", a: ["7", "8", "9"], c: 1, l: 5 },
      { q: "27 + 14 = ?", a: ["40", "41", "42"], c: 1, l: 5 },
      { q: "50 - 23 = ?", a: ["26", "27", "28"], c: 1, l: 5 },
      { q: "8 × 7 = ?", a: ["54", "56", "58"], c: 1, l: 5 },
      { q: "81 ÷ 9 = ?", a: ["8", "9", "10"], c: 1, l: 5 },
      { q: "19 + 17 = ?", a: ["35", "36", "37"], c: 1, l: 5 },
      { q: "60 - 25 = ?", a: ["34", "35", "36"], c: 1, l: 5 },
      { q: "6 × 9 = ?", a: ["52", "54", "56"], c: 1, l: 5 },
      { q: "72 ÷ 8 = ?", a: ["8", "9", "10"], c: 1, l: 5 }
    ];

    // ===== ЛОГИКА МАТЕМАТИКИ =====
    let mathCurrent = 0, mathScore = 0, mathLevel = 1, mathList = [];

    function startMath() {
      mathCurrent = 0;
      mathScore = 0;
      mathLevel = 1;
      mathList = shuffle(mathQuestions).filter(q => q.l === 1).slice(0, 10);
      loadMath();
    }

    function loadMath() {
      const q = mathList[mathCurrent];
      document.getElementById("math-question").textContent = "Уровень " + mathLevel + ": " + q.q;

      const answers = document.getElementById("math-answers");
      answers.innerHTML = "";

      q.a.forEach((ans, i) => {
        const btn = document.createElement("button");
        btn.textContent = ans;
        btn.className = "answer";
        btn.onclick = () => checkMath(i, btn);
        answers.appendChild(btn);
      });

      document.getElementById("math-progress").textContent = `Вопрос ${mathCurrent + 1} из ${mathList.length}`;
    }

    function checkMath(i, btn) {
      const q = mathList[mathCurrent];

      const buttons = document.getElementById("math-answers").children;
      for (let b of buttons) b.disabled = true;

      if (i === q.c) {
        mathScore++;
        btn.classList.add("correct");
      } else {
        btn.classList.add("wrong");
        buttons[q.c].classList.add("correct");
      }

      mathCurrent++;

      setTimeout(() => {
        if (mathCurrent < mathList.length) {
          loadMath();
        } else {
          nextMathLevel();
        }
      }, 700);
    }

    function nextMathLevel() {
      mathLevel++;

      if (mathLevel > 10) {
        document.getElementById("math-question").textContent = "🏆 Математика завершена!";
        document.getElementById("math-answers").innerHTML = "";
        document.getElementById("math-progress").textContent = "Счёт: " + mathScore;
        return;
      }

      mathCurrent = 0;
      mathList = shuffle(mathQuestions).filter(q => q.l === mathLevel).slice(0, 10);
      loadMath();
    }

    // запуск
    document.querySelector("button[onclick=\"showTab('math')\"]").onclick = () => {
      showTab('math');
      startMath();
    };
    function openMath() {
      showTab('math');
      startMath();
    }
    if (i === q.c) {
      correctMath++;
    }
    totalMath++;

    let percent = Math.round((correctMath / totalMath) * 100);

    console.log("Процент правильных: " + percent + "%");
function playErrorSound(){
  let audio = new Audio("https://actions.google.com/sounds/v1/cartoon/wood_plank_flicks.ogg");
  audio.play();
}

  </script>

</body>

</html>
instagram:https://www.instagram.com/uvaysiddin_22/#
telegram:https://t.me/EFOOTBALSTART_10
