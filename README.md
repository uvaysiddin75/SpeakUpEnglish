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
    <div id="lives"></div>
    <div id="math-answers"></div>

    <button onclick="startMath()">🔄 Начать заново</button>
    <div style="width:100%;background:#ddd;height:10px;border-radius:5px;">
      <div id="progress-bar" style="height:10px;background:#4caf50;width:0%;border-radius:5px;"></div>
    </div>
    <div id="math-result"></div>
  </section>
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg, #4facfe, #00f2fe);
      margin: 0;
      padding: 0;
      text-align: center;
      color: #333;
    }

    h1 {
      color: white;
      margin-top: 20px;
    }

    nav {
      margin: 20px;
    }

    /* КНОПКИ ВКЛАДОК */
    button.tab {
      padding: 12px 25px;
      margin: 5px;
      font-size: 18px;
      border: none;
      border-radius: 10px;
      background: white;
      color: #2196f3;
      cursor: pointer;
      font-weight: bold;
      transition: 0.3s;
    }

    button.tab:hover {
      background: #2196f3;
      color: white;
      transform: scale(1.05);
    }

    /* СЕКЦИИ */
    section {
      display: none;
      max-width: 500px;
      margin: 20px auto;
      padding: 20px;
      background: white;
      border-radius: 15px;
      box-shadow: 0 10px 25px rgba(0, 0, 0, 0.2);
    }

    section.active {
      display: block;
    }

    /* ВОПРОС */
    #question,
    #math-question {
      font-size: 22px;
      margin-bottom: 15px;
      font-weight: bold;
    }

    /* ОТВЕТЫ */
    .answer {
      display: block;
      width: 100%;
      margin: 10px 0;
      padding: 15px;
      font-size: 18px;
      border-radius: 10px;
      border: none;
      background: #f1f1f1;
      cursor: pointer;
      transition: 0.3s;
    }

    .answer:hover {
      background: #e3f2fd;
      transform: scale(1.03);
    }

    .correct {
      background: #4caf50 !important;
      color: white;
    }

    .wrong {
      background: #f44336 !important;
      color: white;
    }

    /* ПРОГРЕСС */
    #progress,
    #math-progress {
      margin-top: 10px;
      font-size: 14px;
      color: #666;
    }

    /* КРЕСТИКИ-НОЛИКИ */
    #tic-tac-toe {
      display: grid;
      grid-template-columns: repeat(3, 90px);
      gap: 10px;
      justify-content: center;
      margin-top: 20px;
    }

    .ttt-cell {
      width: 90px;
      height: 90px;
      background: #f9f9f9;
      border-radius: 10px;
      font-size: 30px;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      transition: 0.2s;
    }

    .ttt-cell:hover {
      background: #e3f2fd;
    }

    .ttt-cell.win {
      background: #4caf50;
      color: white;
    }

    #ttt-result {
      margin-top: 15px;
      font-size: 18px;
      font-weight: bold;
    }

    /* КНОПКА СТАРТА */
    button {
      margin-top: 10px;
      padding: 10px 20px;
      font-size: 16px;
      border-radius: 8px;
      border: none;
      background: #2196f3;
      color: white;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      background: #1976d2;
    }

    .selected {
      background: orange !important;
      color: black !important;
      transform: scale(1.05);
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
    let lives = 3;
    let correctMath = 0;
    let totalMath = 0;
    // ===== Навигация по вкладкам =====
    function updateProgress() {
  let percent = (current / questions.length) * 100;
  document.getElementById("progress-bar").style.width = percent + "%";
}
    function showTab(tabId) {
      document.querySelectorAll('section').forEach(sec => sec.classList.remove('active'));
      document.getElementById(tabId).classList.add('active');
    }
    function updateLives() {
      document.getElementById("lives").textContent = "❤️".repeat(lives);
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
      const q = questions[current];

      const buttons = document.getElementById("answers").children;

      // подсветка выбранного ответа (ОРАНЖЕВЫЙ)
      btn.classList.add("selected");

      // отключаем все кнопки
      for (let b of buttons) b.disabled = true;

      setTimeout(() => {
        // показываем правильный/неправильный
        Array.from(buttons).forEach((b, idx) => {
          if (idx === q.c) b.classList.add("correct");
          else if (idx === i) b.classList.add("wrong");
        });


        const result = document.getElementById("result");

        if (i === q.c) {
          score++;
          result.textContent = "✅ Правильно";
        } else {
          result.textContent = "❌ Неправильно";
        }

        current++;

        setTimeout(() => {
          if (current < questions.length) {
            loadQuestion();
          } else {
            nextLevel();
          }
        }, 700);

      }, 300);
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

      // ===== УРОВЕНЬ 1 =====
      { q: "1 + 1 = ?", a: ["3", "2", "4"], c: 1, l: 1 },
      { q: "2 + 3 = ?", a: ["6", "4", "5"], c: 2, l: 1 },
      { q: "4 - 1 = ?", a: ["3", "2", "5"], c: 0, l: 1 },
      { q: "5 - 3 = ?", a: ["3", "1", "2"], c: 2, l: 1 },
      { q: "3 + 2 = ?", a: ["4", "6", "5"], c: 2, l: 1 },
      { q: "6 - 4 = ?", a: ["3", "2", "1"], c: 1, l: 1 },
      { q: "2 + 6 = ?", a: ["8", "9", "7"], c: 0, l: 1 },
      { q: "7 - 5 = ?", a: ["3", "2", "1"], c: 1, l: 1 },
      { q: "3 + 4 = ?", a: ["7", "6", "8"], c: 0, l: 1 },
      { q: "8 - 3 = ?", a: ["6", "5", "4"], c: 1, l: 1 },

      // ===== УРОВЕНЬ 2 =====
      { q: "10 - 4 = ?", a: ["7", "5", "6"], c: 2, l: 2 },
      { q: "3 × 3 = ?", a: ["9", "6", "12"], c: 0, l: 2 },
      { q: "8 ÷ 2 = ?", a: ["5", "4", "3"], c: 1, l: 2 },
      { q: "9 + 1 = ?", a: ["10", "11", "9"], c: 0, l: 2 },
      { q: "12 - 5 = ?", a: ["6", "8", "7"], c: 2, l: 2 },
      { q: "4 × 3 = ?", a: ["12", "10", "14"], c: 0, l: 2 },
      { q: "6 ÷ 3 = ?", a: ["3", "2", "1"], c: 1, l: 2 },
      { q: "7 + 5 = ?", a: ["11", "13", "12"], c: 2, l: 2 },
      { q: "15 - 7 = ?", a: ["9", "8", "7"], c: 1, l: 2 },
      { q: "5 × 2 = ?", a: ["10", "12", "8"], c: 0, l: 2 },

      // ===== УРОВЕНЬ 3 =====
      { q: "14 + 6 = ?", a: ["22", "20", "18"], c: 1, l: 3 },
      { q: "18 - 9 = ?", a: ["9", "11", "7"], c: 0, l: 3 },
      { q: "6 × 4 = ?", a: ["24", "20", "28"], c: 0, l: 3 },
      { q: "20 ÷ 5 = ?", a: ["5", "4", "3"], c: 1, l: 3 },
      { q: "9 × 3 = ?", a: ["30", "27", "24"], c: 1, l: 3 },
      { q: "16 ÷ 4 = ?", a: ["6", "4", "2"], c: 1, l: 3 },
      { q: "25 - 10 = ?", a: ["20", "15", "10"], c: 1, l: 3 },
      { q: "7 × 5 = ?", a: ["35", "40", "30"], c: 0, l: 3 },
      { q: "21 ÷ 3 = ?", a: ["8", "7", "6"], c: 1, l: 3 },
      { q: "13 + 7 = ?", a: ["22", "18", "20"], c: 2, l: 3 },

      // ===== УРОВЕНЬ 4 =====
      { q: "12 × 3 = ?", a: ["42", "36", "30"], c: 1, l: 4 },
      { q: "40 ÷ 5 = ?", a: ["10", "8", "6"], c: 1, l: 4 },
      { q: "28 + 14 = ?", a: ["44", "40", "42"], c: 2, l: 4 },
      { q: "50 - 25 = ?", a: ["30", "25", "20"], c: 1, l: 4 },
      { q: "9 × 6 = ?", a: ["60", "54", "48"], c: 1, l: 4 },
      { q: "72 ÷ 8 = ?", a: ["11", "9", "7"], c: 1, l: 4 },
      { q: "33 + 17 = ?", a: ["45", "55", "50"], c: 2, l: 4 },
      { q: "81 ÷ 9 = ?", a: ["10", "8", "9"], c: 2, l: 4 },
      { q: "45 - 18 = ?", a: ["27", "30", "25"], c: 0, l: 4 },
      { q: "11 × 4 = ?", a: ["48", "40", "44"], c: 2, l: 4 },

      // ===== УРОВЕНЬ 5 =====
      { q: "15 × 3 = ?", a: ["60", "45", "30"], c: 1, l: 5 },
      { q: "100 ÷ 4 = ?", a: ["30", "20", "25"], c: 2, l: 5 },
      { q: "64 ÷ 8 = ?", a: ["10", "6", "8"], c: 2, l: 5 },
      { q: "12 × 5 = ?", a: ["70", "60", "50"], c: 1, l: 5 },
      { q: "90 - 45 = ?", a: ["50", "40", "45"], c: 2, l: 5 },
      { q: "14 × 4 = ?", a: ["56", "60", "52"], c: 0, l: 5 },
      { q: "81 + 19 = ?", a: ["110", "90", "100"], c: 2, l: 5 },
      { q: "144 ÷ 12 = ?", a: ["14", "12", "10"], c: 1, l: 5 },
      { q: "25 × 4 = ?", a: ["120", "80", "100"], c: 2, l: 5 },
      { q: "200 ÷ 10 = ?", a: ["30", "10", "20"], c: 2, l: 5 }

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

      if (btn.textContent == q.a[q.c]) {
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
    function playErrorSound() {
      let audio = new Audio("https://actions.google.com/sounds/v1/cartoon/wood_plank_flicks.ogg");
      audio.play();
    }
    // перемешка массива
    function shuffle(array) {
      for (let i = array.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
      }
      return array;
    }
    function botMove() {
      let empty = board.map((v, i) => v == "" ? i : null).filter(v => v !== null);
      let move = empty[Math.floor(Math.random() * empty.length)];

      if (move !== undefined) {
        let cell = document.querySelectorAll(".ttt-cell")[move];
        board[move] = turn;
        cell.textContent = turn;
      }
    }
    // перемешка ответов
    function shuffleAnswers(question) {
      let correct = question.a[question.c];
      let shuffled = shuffle([...question.a]);
      let newIndex = shuffled.indexOf(correct);

      return {
        q: question.q,
        a: shuffled,
        c: newIndex,
        l: question.l
      };
    }
    let usedMathQuestions = [];




    function nextMathLevel() {
      mathLevel++;


      function shuffleAnswers(question) {
        let answers = question.a.map((text, index) => ({
          text,
          correct: index === question.c
        }));

        // перемешивание
        answers.sort(() => Math.random() - 0.5);

        // обновляем индексы
        question.a = answers.map(a => a.text);
        question.c = answers.findIndex(a => a.correct);
      }
      function loadMath() {
        const q = mathList[mathCurrent];

        // создаём копию ответов + отмечаем правильный
        let answers = q.a.map((text, index) => ({
          text: text,
          correct: index === q.c
        }));

        // перемешиваем
        answers.sort(() => Math.random() - 0.5);

        document.getElementById("math-question").textContent =
          "Уровень " + mathLevel + ": " + q.q;

        const answersDiv = document.getElementById("math-answers");
        answersDiv.innerHTML = "";

        answers.forEach((ans) => {
          const btn = document.createElement("button");
          btn.textContent = ans.text;
          btn.className = "answer";

          btn.onclick = () => {
            const buttons = answersDiv.children;

            // блокируем все кнопки
            for (let b of buttons) b.disabled = true;

            if (ans.correct) {
              btn.classList.add("correct");
              mathScore++;
            } else {
              btn.classList.add("wrong");

              // подсветить правильный
              Array.from(buttons).forEach((b, i) => {
                if (answers[i].correct) b.classList.add("correct");
              });
            }

            mathCurrent++;

            setTimeout(() => {
              if (mathCurrent < mathList.length) {
                loadMath();
              } else {
                nextMathLevel();
              }
            }, 700);
          };

          answersDiv.appendChild(btn);
        });

        document.getElementById("math-progress").textContent =
          `Вопрос ${mathCurrent + 1} из ${mathList.length}`;
      }
    }


  </script>

</body>

</html>
instagram:https://www.instagram.com/uvaysiddin_22/#
telegram:https://t.me/EFOOTBALSTART_10
