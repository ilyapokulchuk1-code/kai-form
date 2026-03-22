<!DOCTYPE html>

<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ReelsCRM — Учёт проектов</title>
<link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0a0a0f;
    --surface: #13131a;
    --card: #1a1a24;
    --border: #2a2a38;
    --accent: #ff3c5f;
    --accent2: #ffb800;
    --accent3: #00e5a0;
    --text: #f0f0f8;
    --muted: #7a7a9a;
    --tag-bg: #22223a;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'DM Sans', sans-serif; background: var(--bg); color: var(--text); min-height: 100vh; }

/* HEADER */
header {
background: var(–surface);
border-bottom: 1px solid var(–border);
padding: 0 24px;
display: flex; align-items: center; justify-content: space-between;
height: 64px; position: sticky; top: 0; z-index: 100;
}
.logo { font-family: ‘Bebas Neue’, cursive; font-size: 28px; letter-spacing: 2px; color: var(–accent); }
.logo span { color: var(–text); }
.header-right { display: flex; align-items: center; gap: 12px; }
.user-badge {
background: var(–tag-bg); border: 1px solid var(–border);
border-radius: 20px; padding: 6px 14px; font-size: 13px; font-weight: 500; cursor: pointer;
transition: all .2s;
}
.user-badge:hover { border-color: var(–accent); color: var(–accent); }
.user-badge.active { background: var(–accent); border-color: var(–accent); color: #fff; }
#notif-btn {
background: var(–tag-bg); border: 1px solid var(–border);
border-radius: 20px; padding: 6px 14px; font-size: 13px; cursor: pointer;
transition: all .2s; position: relative;
}
#notif-btn:hover { border-color: var(–accent2); color: var(–accent2); }
.notif-dot {
position: absolute; top: 4px; right: 4px;
width: 8px; height: 8px; border-radius: 50%; background: var(–accent); display: none;
}

/* MAIN LAYOUT */
.container { max-width: 1400px; margin: 0 auto; padding: 24px; }

/* STATS BAR */
.stats-bar {
display: grid; grid-template-columns: repeat(5, 1fr); gap: 12px; margin-bottom: 24px;
}
.stat-card {
background: var(–surface); border: 1px solid var(–border); border-radius: 12px;
padding: 16px; text-align: center; transition: transform .2s;
}
.stat-card:hover { transform: translateY(-2px); }
.stat-num { font-family: ‘Bebas Neue’, cursive; font-size: 36px; color: var(–accent); line-height: 1; }
.stat-label { font-size: 11px; color: var(–muted); text-transform: uppercase; letter-spacing: 1px; margin-top: 4px; }

/* TOOLBAR */
.toolbar {
display: flex; gap: 10px; margin-bottom: 20px; flex-wrap: wrap; align-items: center;
}
.btn-primary {
background: var(–accent); color: #fff; border: none; border-radius: 8px;
padding: 10px 20px; font-family: ‘DM Sans’, sans-serif; font-size: 14px; font-weight: 600;
cursor: pointer; transition: all .2s;
}
.btn-primary:hover { background: #ff1a44; transform: translateY(-1px); }
.filter-btn {
background: var(–surface); border: 1px solid var(–border); color: var(–muted);
border-radius: 8px; padding: 9px 16px; font-family: ‘DM Sans’, sans-serif;
font-size: 13px; cursor: pointer; transition: all .2s;
}
.filter-btn:hover, .filter-btn.active { border-color: var(–accent); color: var(–text); }
.filter-btn.active { background: rgba(255,60,95,0.1); }
.search-box {
flex: 1; min-width: 200px; background: var(–surface); border: 1px solid var(–border);
color: var(–text); border-radius: 8px; padding: 9px 16px;
font-family: ‘DM Sans’, sans-serif; font-size: 13px; outline: none; transition: border-color .2s;
}
.search-box:focus { border-color: var(–accent); }
.search-box::placeholder { color: var(–muted); }

/* KANBAN */
.kanban { display: grid; grid-template-columns: repeat(7, minmax(190px, 1fr)); gap: 14px; overflow-x: auto; padding-bottom: 12px; }
.column {
background: var(–surface); border: 1px solid var(–border); border-radius: 14px;
min-height: 400px; display: flex; flex-direction: column;
}
.col-header {
padding: 14px 14px 10px; border-bottom: 1px solid var(–border);
display: flex; align-items: center; justify-content: space-between;
}
.col-title { font-size: 12px; font-weight: 600; text-transform: uppercase; letter-spacing: 1px; }
.col-count {
background: var(–tag-bg); border-radius: 10px; padding: 2px 8px;
font-size: 11px; color: var(–muted); font-weight: 600;
}
.col-body { padding: 10px; display: flex; flex-direction: column; gap: 8px; flex: 1; }

/* PROJECT CARD */
.proj-card {
background: var(–card); border: 1px solid var(–border); border-radius: 10px;
padding: 12px; cursor: pointer; transition: all .2s; position: relative; overflow: hidden;
}
.proj-card::before {
content: ‘’; position: absolute; left: 0; top: 0; bottom: 0;
width: 3px; background: var(–accent); border-radius: 10px 0 0 10px;
}
.proj-card:hover { border-color: var(–accent); transform: translateY(-2px); box-shadow: 0 8px 24px rgba(255,60,95,.15); }
.proj-name { font-size: 13px; font-weight: 600; margin-bottom: 6px; line-height: 1.3; }
.proj-meta { font-size: 11px; color: var(–muted); margin-bottom: 8px; }
.proj-tags { display: flex; gap: 4px; flex-wrap: wrap; margin-bottom: 8px; }
.tag {
background: var(–tag-bg); border-radius: 4px; padding: 2px 7px;
font-size: 10px; font-weight: 600; text-transform: uppercase; letter-spacing: .5px;
}
.tag-reel { color: var(–accent2); }
.tag-paid { color: var(–accent3); }
.tag-nopay { color: var(–accent); }
.proj-footer { display: flex; align-items: center; justify-content: space-between; }
.assignees { display: flex; gap: -4px; }
.avatar {
width: 22px; height: 22px; border-radius: 50%; border: 2px solid var(–card);
display: flex; align-items: center; justify-content: center;
font-size: 9px; font-weight: 700; margin-left: -4px; first:margin-left: 0;
}
.av-0 { background: #ff3c5f; color: #fff; }
.av-1 { background: #ffb800; color: #000; }
.av-2 { background: #00e5a0; color: #000; }
.av-3 { background: #7c5cfc; color: #fff; }
.due-date { font-size: 10px; color: var(–muted); }
.due-date.overdue { color: var(–accent); }
.due-date.soon { color: var(–accent2); }

/* STAGE COLORS */
.stage-0::before { background: #7c5cfc; }
.stage-1::before { background: #00b4ff; }
.stage-2::before { background: #ffb800; }
.stage-3::before { background: #ff7a00; }
.stage-4::before { background: #ff3c5f; }
.stage-5::before { background: #a855f7; }
.stage-6::before { background: #00e5a0; }

.col-0 .col-title { color: #7c5cfc; }
.col-1 .col-title { color: #00b4ff; }
.col-2 .col-title { color: #ffb800; }
.col-3 .col-title { color: #ff7a00; }
.col-4 .col-title { color: #ff3c5f; }
.col-5 .col-title { color: #a855f7; }
.col-6 .col-title { color: #00e5a0; }

/* MODAL */
.overlay {
position: fixed; inset: 0; background: rgba(0,0,0,.7); z-index: 200;
display: none; align-items: center; justify-content: center; padding: 20px;
backdrop-filter: blur(4px);
}
.overlay.open { display: flex; }
.modal {
background: var(–card); border: 1px solid var(–border); border-radius: 18px;
width: 100%; max-width: 640px; max-height: 90vh; overflow-y: auto;
padding: 28px; position: relative;
box-shadow: 0 24px 80px rgba(0,0,0,.6);
}
.modal-title { font-family: ‘Bebas Neue’, cursive; font-size: 28px; letter-spacing: 1px; margin-bottom: 20px; }
.close-btn {
position: absolute; top: 20px; right: 20px; background: var(–tag-bg);
border: 1px solid var(–border); color: var(–muted); border-radius: 8px;
width: 32px; height: 32px; cursor: pointer; font-size: 18px;
display: flex; align-items: center; justify-content: center; transition: all .2s;
}
.close-btn:hover { border-color: var(–accent); color: var(–accent); }

.form-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 14px; }
.form-full { grid-column: 1 / -1; }
label { font-size: 11px; text-transform: uppercase; letter-spacing: 1px; color: var(–muted); display: block; margin-bottom: 6px; font-weight: 600; }
input, select, textarea {
width: 100%; background: var(–surface); border: 1px solid var(–border);
color: var(–text); border-radius: 8px; padding: 10px 12px;
font-family: ‘DM Sans’, sans-serif; font-size: 13px; outline: none; transition: border-color .2s;
}
input:focus, select:focus, textarea:focus { border-color: var(–accent); }
textarea { resize: vertical; min-height: 80px; }
select option { background: var(–card); }

.checkbox-group { display: flex; flex-wrap: wrap; gap: 8px; }
.checkbox-item {
display: flex; align-items: center; gap: 6px;
background: var(–surface); border: 1px solid var(–border);
border-radius: 8px; padding: 7px 12px; cursor: pointer; transition: all .2s;
}
.checkbox-item input[type=checkbox] { width: auto; }
.checkbox-item:has(input:checked) { border-color: var(–accent3); background: rgba(0,229,160,.08); color: var(–accent3); }
.checkbox-item label { margin: 0; color: inherit; cursor: pointer; text-transform: none; letter-spacing: 0; font-size: 12px; }

.form-actions { display: flex; gap: 10px; margin-top: 20px; justify-content: flex-end; }
.btn-secondary {
background: transparent; border: 1px solid var(–border); color: var(–muted);
border-radius: 8px; padding: 10px 20px; font-family: ‘DM Sans’, sans-serif;
font-size: 14px; cursor: pointer; transition: all .2s;
}
.btn-secondary:hover { border-color: var(–muted); color: var(–text); }
.btn-danger {
background: transparent; border: 1px solid #ff3c5f33; color: var(–accent);
border-radius: 8px; padding: 10px 20px; font-family: ‘DM Sans’, sans-serif;
font-size: 14px; cursor: pointer; transition: all .2s; margin-right: auto;
}
.btn-danger:hover { background: rgba(255,60,95,.1); }

/* CHECKLIST IN CARD DETAIL */
.checklist { margin-top: 16px; }
.check-row {
display: flex; align-items: center; gap: 10px; padding: 8px 0;
border-bottom: 1px solid var(–border);
}
.check-row:last-child { border-bottom: none; }
.check-row input[type=checkbox] { width: 16px; height: 16px; accent-color: var(–accent3); cursor: pointer; }
.check-label { font-size: 13px; flex: 1; }
.check-label.done { text-decoration: line-through; color: var(–muted); }
.check-who { font-size: 11px; color: var(–muted); }

/* NOTIFICATIONS PANEL */
.notif-panel {
position: fixed; top: 72px; right: 24px; width: 340px;
background: var(–card); border: 1px solid var(–border); border-radius: 14px;
box-shadow: 0 20px 60px rgba(0,0,0,.5); z-index: 150; display: none;
padding: 16px; max-height: 500px; overflow-y: auto;
}
.notif-panel.open { display: block; }
.notif-title { font-size: 12px; text-transform: uppercase; letter-spacing: 1px; color: var(–muted); margin-bottom: 12px; font-weight: 700; }
.notif-item {
padding: 10px 12px; border-radius: 8px; margin-bottom: 8px;
background: var(–surface); border-left: 3px solid var(–accent2);
font-size: 12px; line-height: 1.5;
}
.notif-item.urgent { border-color: var(–accent); }
.notif-item.ok { border-color: var(–accent3); }
.notif-project { font-weight: 700; color: var(–text); }
.notif-msg { color: var(–muted); margin-top: 2px; }

/* PROGRESS BAR */
.progress-wrap { margin: 16px 0; }
.progress-label { display: flex; justify-content: space-between; font-size: 11px; color: var(–muted); margin-bottom: 6px; }
.progress-bar { height: 4px; background: var(–border); border-radius: 2px; overflow: hidden; }
.progress-fill { height: 100%; background: linear-gradient(90deg, var(–accent), var(–accent2)); transition: width .4s; }

/* RESPONSIVE */
@media (max-width: 900px) {
.stats-bar { grid-template-columns: repeat(3, 1fr); }
.kanban { grid-template-columns: repeat(3, minmax(200px, 1fr)); }
}
@media (max-width: 600px) {
.stats-bar { grid-template-columns: repeat(2, 1fr); }
.form-grid { grid-template-columns: 1fr; }
.kanban { grid-template-columns: repeat(2, minmax(180px, 1fr)); }
}

/* ANIMATIONS */
.proj-card { animation: fadeIn .3s ease; }
@keyframes fadeIn { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: translateY(0); } }

/* HISTORY LOG */
.history-log { margin-top: 16px; }
.log-entry { display: flex; gap: 10px; padding: 8px 0; border-bottom: 1px solid var(–border); font-size: 12px; }
.log-entry:last-child { border-bottom: none; }
.log-time { color: var(–muted); white-space: nowrap; min-width: 90px; }
.log-user { font-weight: 600; }
.log-msg { color: var(–muted); }

.empty-col { text-align: center; padding: 30px 10px; color: var(–muted); font-size: 12px; }
.empty-icon { font-size: 28px; margin-bottom: 8px; opacity: .4; }
</style>

</head>
<body>

<header>
  <div class="logo">Reels<span>CRM</span></div>
  <div class="header-right">
    <div style="font-size:12px;color:var(--muted);">Вы:</div>
    <div class="user-badge active" data-user="Я (Автор)" onclick="setUser(this)">Я (Автор)</div>
    <div class="user-badge" data-user="Ян" onclick="setUser(this)">Ян</div>
    <div class="user-badge" data-user="Влад" onclick="setUser(this)">Влад</div>
    <div class="user-badge" data-user="Элвин" onclick="setUser(this)">Элвин</div>
    <button id="notif-btn" onclick="toggleNotif()">🔔 Напоминания <div class="notif-dot" id="notif-dot"></div></button>
  </div>
</header>

<div class="notif-panel" id="notif-panel">
  <div class="notif-title">⚡ Требуют внимания</div>
  <div id="notif-list"></div>
</div>

<div class="container">
  <div class="stats-bar">
    <div class="stat-card">
      <div class="stat-num" id="stat-total">0</div>
      <div class="stat-label">Всего проектов</div>
    </div>
    <div class="stat-card">
      <div class="stat-num" id="stat-active" style="color:var(--accent2)">0</div>
      <div class="stat-label">В работе</div>
    </div>
    <div class="stat-card">
      <div class="stat-num" id="stat-paid" style="color:var(--accent3)">0</div>
      <div class="stat-label">Оплачено</div>
    </div>
    <div class="stat-card">
      <div class="stat-num" id="stat-done" style="color:var(--accent3)">0</div>
      <div class="stat-label">Готово</div>
    </div>
    <div class="stat-card">
      <div class="stat-num" id="stat-overdue" style="color:var(--accent)">0</div>
      <div class="stat-label">Просрочено</div>
    </div>
  </div>

  <div class="toolbar">
    <button class="btn-primary" onclick="openNew()">+ Новый клиент</button>
    <input class="search-box" placeholder="🔍 Поиск по клиенту..." oninput="filterCards(this.value)" id="search-input">
    <button class="filter-btn active" onclick="filterStage(null, this)">Все</button>
    <button class="filter-btn" onclick="filterStage('Ян', this)">Ян</button>
    <button class="filter-btn" onclick="filterStage('Влад', this)">Влад</button>
    <button class="filter-btn" onclick="filterStage('Элвин', this)">Элвин</button>
    <button class="filter-btn" onclick="filterStage('Я (Автор)', this)">Мои</button>
  </div>

  <div class="kanban" id="kanban">
    <!-- columns rendered by JS -->
  </div>
</div>

<!-- ADD/EDIT MODAL -->

<div class="overlay" id="modal-overlay" onclick="closeModal(event)">
  <div class="modal" id="modal">
    <button class="close-btn" onclick="closeModalBtn()">✕</button>
    <div class="modal-title" id="modal-heading">Новый клиент</div>

```
<div class="form-grid">
  <div class="form-full">
    <label>Название клиента / компании *</label>
    <input id="f-name" placeholder="Например: Cafe Bliss">
  </div>
  <div>
    <label>Контакт (телефон / Instagram)</label>
    <input id="f-contact" placeholder="+373 xxx xxx">
  </div>
  <div>
    <label>Ответственный</label>
    <select id="f-owner">
      <option>Я (Автор)</option>
      <option>Ян</option>
      <option>Влад</option>
      <option>Элвин</option>
    </select>
  </div>
  <div>
    <label>Этап</label>
    <select id="f-stage">
      <option value="0">📞 Переговоры</option>
      <option value="1">💡 Обсуждение идеи</option>
      <option value="2">💰 Оплата</option>
      <option value="3">🎬 Съёмка</option>
      <option value="4">✂️ Монтаж</option>
      <option value="5">👁️ Проверка</option>
      <option value="6">✅ Готово</option>
    </select>
  </div>
  <div>
    <label>Дата съёмки</label>
    <input type="date" id="f-shoot-date">
  </div>
  <div>
    <label>Дедлайн сдачи</label>
    <input type="date" id="f-deadline">
  </div>
  <div>
    <label>Бюджет (леев)</label>
    <input type="number" id="f-budget" placeholder="5000">
  </div>
  <div>
    <label>Оплата</label>
    <select id="f-paid">
      <option value="no">❌ Не оплачено</option>
      <option value="partial">🔄 Частично</option>
      <option value="yes">✅ Оплачено</option>
    </select>
  </div>
  <div class="form-full">
    <label>Идея / Концепция ролика</label>
    <textarea id="f-idea" placeholder="Кратко опишите идею..."></textarea>
  </div>
  <div class="form-full">
    <label>Сценарий</label>
    <textarea id="f-script" placeholder="Сценарий или ссылка на документ..."></textarea>
  </div>
  <div class="form-full">
    <label>Команда на проекте</label>
    <div class="checkbox-group">
      <label class="checkbox-item"><input type="checkbox" id="t-me" value="Я (Автор)"> <label for="t-me">Я (Автор)</label></label>
      <label class="checkbox-item"><input type="checkbox" id="t-yan" value="Ян"> <label for="t-yan">Ян</label></label>
      <label class="checkbox-item"><input type="checkbox" id="t-vlad" value="Влад"> <label for="t-vlad">Влад</label></label>
      <label class="checkbox-item"><input type="checkbox" id="t-elvin" value="Элвин"> <label for="t-elvin">Элвин</label></label>
    </div>
  </div>
  <div class="form-full">
    <label>Чеклист задач</label>
    <div style="display:flex;flex-direction:column;gap:6px;">
      <div class="check-row"><input type="checkbox" id="ck-idea"> <span class="check-label">Идея / Концепция утверждена</span></div>
      <div class="check-row"><input type="checkbox" id="ck-script"> <span class="check-label">Сценарий написан</span></div>
      <div class="check-row"><input type="checkbox" id="ck-scriptok"> <span class="check-label">Сценарий одобрен клиентом</span></div>
      <div class="check-row"><input type="checkbox" id="ck-date"> <span class="check-label">День съёмки назначен</span></div>
      <div class="check-row"><input type="checkbox" id="ck-shot"> <span class="check-label">Съёмка проведена</span></div>
      <div class="check-row"><input type="checkbox" id="ck-edit"> <span class="check-label">Отдано в монтаж</span></div>
      <div class="check-row"><input type="checkbox" id="ck-draft"> <span class="check-label">Черновик готов</span></div>
      <div class="check-row"><input type="checkbox" id="ck-review"> <span class="check-label">Клиент посмотрел / правки</span></div>
      <div class="check-row"><input type="checkbox" id="ck-final"> <span class="check-label">Финал сдан клиенту</span></div>
    </div>
  </div>
  <div class="form-full">
    <label>Комментарий / Заметки</label>
    <textarea id="f-notes" placeholder="Пожелания клиента, правки, важные детали..."></textarea>
  </div>
</div>
<div class="form-actions">
  <button class="btn-danger" id="btn-delete" onclick="deleteProject()" style="display:none">🗑 Удалить</button>
  <button class="btn-secondary" onclick="closeModalBtn()">Отмена</button>
  <button class="btn-primary" onclick="saveProject()">Сохранить</button>
</div>
```

  </div>
</div>

<script>
const STAGES = [
  { name: '📞 Переговоры', color: '#7c5cfc' },
  { name: '💡 Идея', color: '#00b4ff' },
  { name: '💰 Оплата', color: '#ffb800' },
  { name: '🎬 Съёмка', color: '#ff7a00' },
  { name: '✂️ Монтаж', color: '#ff3c5f' },
  { name: '👁️ Проверка', color: '#a855f7' },
  { name: '✅ Готово', color: '#00e5a0' },
];

const MEMBERS = ['Я (Автор)', 'Ян', 'Влад', 'Элвин'];
const AV_INITIALS = { 'Я (Автор)': 'Я', 'Ян': 'Я', 'Влад': 'В', 'Элвин': 'Э' };
const AV_CLASS = { 'Я (Автор)': 'av-0', 'Ян': 'av-1', 'Влад': 'av-2', 'Элвин': 'av-3' };

let projects = JSON.parse(localStorage.getItem('reelscrm_v2') || '[]');
let editingId = null;
let currentUser = 'Я (Автор)';
let filterMember = null;
let searchQuery = '';

if (projects.length === 0) {
  projects = [
    { id: 1, name: 'Cafe Primavara', contact: '@cafeprimavara', stage: 2, owner: 'Я (Автор)', team: ['Я (Автор)', 'Ян'], budget: 8000, paid: 'yes', shootDate: '', deadline: '', idea: 'Ролик с атмосферой утреннего кофе', script: '', notes: 'Клиент хочет тёплые тона', checks: { idea:true, script:true, scriptok:true, date:false, shot:false, edit:false, draft:false, review:false, final:false }, log: [{time:'22.03 10:00', user:'Я (Автор)', msg:'Создан проект'}] },
    { id: 2, name: 'FitZone Moldova', contact: '+373 60 000 111', stage: 3, owner: 'Ян', team: ['Ян', 'Влад'], budget: 5000, paid: 'partial', shootDate: '2024-03-25', deadline: '2024-04-01', idea: 'Динамичный ролик тренировок', script: 'Сцена 1: Вход в зал...', notes: '', checks: { idea:true, script:true, scriptok:true, date:true, shot:false, edit:false, draft:false, review:false, final:false }, log: [{time:'20.03 14:00', user:'Ян', msg:'Назначена дата съёмки 25 марта'}] },
    { id: 3, name: 'Floraria Lux', contact: '@florialux', stage: 0, owner: 'Я (Автор)', team: ['Я (Автор)'], budget: 3000, paid: 'no', shootDate: '', deadline: '', idea: '', script: '', notes: 'Первый созвон прошёл хорошо', checks: { idea:false, script:false, scriptok:false, date:false, shot:false, edit:false, draft:false, review:false, final:false }, log: [{time:'22.03 09:00', user:'Я (Автор)', msg:'Создан проект'}] },
    { id: 4, name: 'AutoPlus Service', contact: '+373 79 123 456', stage: 4, owner: 'Влад', team: ['Влад', 'Элвин'], budget: 12000, paid: 'yes', shootDate: '2024-03-18', deadline: '2024-03-28', idea: 'До/после ремонта авто', script: 'Монолог мастера + B-roll', notes: 'Срочно нужен черновик', checks: { idea:true, script:true, scriptok:true, date:true, shot:true, edit:true, draft:false, review:false, final:false }, log: [{time:'18.03 08:00', user:'Влад', msg:'Съёмка завершена'}, {time:'19.03 12:00', user:'Элвин', msg:'Начат монтаж'}] },
  ];
  save();
}

function save() {
  localStorage.setItem('reelscrm_v2', JSON.stringify(projects));
}

function setUser(el) {
  document.querySelectorAll('.user-badge').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
  currentUser = el.dataset.user;
}

function render(filter) {
  const kb = document.getElementById('kanban');
  kb.innerHTML = '';
  STAGES.forEach((s, si) => {
    let cards = projects.filter(p => p.stage == si);
    if (filterMember) cards = cards.filter(p => p.team && p.team.includes(filterMember));
    if (searchQuery) cards = cards.filter(p => p.name.toLowerCase().includes(searchQuery));

    const col = document.createElement('div');
    col.className = `column col-${si}`;
    col.innerHTML = `<div class="col-header"><span class="col-title">${s.name}</span><span class="col-count">${cards.length}</span></div><div class="col-body" id="col-${si}"></div>`;
    kb.appendChild(col);

    const body = col.querySelector('.col-body');
    if (cards.length === 0) {
      body.innerHTML = `<div class="empty-col"><div class="empty-icon">📭</div>Пусто</div>`;
    }
    cards.forEach(p => {
      const el = document.createElement('div');
      el.className = `proj-card stage-${si}`;
      const dueClass = getDueClass(p.deadline);
      const dueText = p.deadline ? formatDate(p.deadline) : '—';
      const paidTag = p.paid === 'yes' ? `<span class="tag tag-paid">Оплачено</span>` : p.paid === 'partial' ? `<span class="tag" style="color:#ff7a00">Частично</span>` : `<span class="tag tag-nopay">Не оплачено</span>`;
      const progress = calcProgress(p.checks);
      const teamAv = (p.team || []).map(m => `<span class="avatar ${AV_CLASS[m]}">${AV_INITIALS[m]}</span>`).join('');
      el.innerHTML = `
        <div class="proj-name">${p.name}</div>
        <div class="proj-meta">${p.contact || 'Контакт не указан'}</div>
        <div class="proj-tags">${paidTag}${p.budget ? `<span class="tag" style="color:var(--muted)">${p.budget} MDL</span>` : ''}</div>
        <div class="progress-wrap"><div class="progress-label"><span>Прогресс</span><span>${progress}%</span></div><div class="progress-bar"><div class="progress-fill" style="width:${progress}%"></div></div></div>
        <div class="proj-footer"><div class="assignees">${teamAv}</div><span class="due-date ${dueClass}">📅 ${dueText}</span></div>
      `;
      el.onclick = () => openEdit(p.id);
      body.appendChild(el);
    });
  });
  updateStats();
  updateNotifs();
}

function calcProgress(checks) {
  if (!checks) return 0;
  const keys = Object.keys(checks);
  const done = keys.filter(k => checks[k]).length;
  return Math.round((done / keys.length) * 100);
}

function getDueClass(date) {
  if (!date) return '';
  const d = new Date(date), now = new Date();
  const diff = (d - now) / 86400000;
  if (diff < 0) return 'overdue';
  if (diff < 3) return 'soon';
  return '';
}

function formatDate(d) {
  if (!d) return '—';
  const [y,m,day] = d.split('-');
  return `${day}.${m}.${y.slice(2)}`;
}

function updateStats() {
  const total = projects.length;
  const active = projects.filter(p => p.stage < 6).length;
  const paid = projects.filter(p => p.paid === 'yes').length;
  const done = projects.filter(p => p.stage === 6).length;
  const overdue = projects.filter(p => p.deadline && getDueClass(p.deadline) === 'overdue').length;
  document.getElementById('stat-total').textContent = total;
  document.getElementById('stat-active').textContent = active;
  document.getElementById('stat-paid').textContent = paid;
  document.getElementById('stat-done').textContent = done;
  document.getElementById('stat-overdue').textContent = overdue;
}

function updateNotifs() {
  const notifs = [];
  const today = new Date();
  projects.forEach(p => {
    if (p.stage === 6) return;
    if (p.deadline) {
      const diff = (new Date(p.deadline) - today) / 86400000;
      if (diff < 0) notifs.push({ project: p.name, msg: `Просрочен дедлайн (${formatDate(p.deadline)})`, type: 'urgent' });
      else if (diff < 2) notifs.push({ project: p.name, msg: `Дедлайн через ${Math.ceil(diff)} дн. (${formatDate(p.deadline)})`, type: 'warn' });
    }
    if (p.shootDate) {
      const diff = (new Date(p.shootDate) - today) / 86400000;
      if (diff >= 0 && diff < 2) notifs.push({ project: p.name, msg: `Съёмка через ${diff < 1 ? 'сегодня' : Math.ceil(diff)+' дн.'} (${formatDate(p.shootDate)})`, type: 'ok' });
    }
    if (p.stage >= 1 && !p.checks?.script) notifs.push({ project: p.name, msg: 'Сценарий ещё не написан', type: 'warn' });
    if (p.stage >= 3 && !p.checks?.shot) notifs.push({ project: p.name, msg: 'Съёмка не отмечена как завершена', type: 'warn' });
    if (p.paid === 'no' && p.stage >= 2) notifs.push({ project: p.name, msg: 'Оплата не получена', type: 'urgent' });
  });
  const list = document.getElementById('notif-list');
  list.innerHTML = notifs.length === 0 ? '<div style="color:var(--muted);font-size:13px;text-align:center;padding:20px">Всё в порядке 🎉</div>' :
    notifs.map(n => `<div class="notif-item ${n.type==='urgent'?'urgent':n.type==='ok'?'ok':''}"><div class="notif-project">${n.project}</div><div class="notif-msg">${n.msg}</div></div>`).join('');
  const dot = document.getElementById('notif-dot');
  const urgent = notifs.filter(n => n.type === 'urgent').length;
  dot.style.display = urgent > 0 ? 'block' : 'none';
}

function toggleNotif() {
  document.getElementById('notif-panel').classList.toggle('open');
}

function openNew() {
  editingId = null;
  document.getElementById('modal-heading').textContent = 'Новый клиент';
  document.getElementById('btn-delete').style.display = 'none';
  clearForm();
  document.getElementById('modal-overlay').classList.add('open');
}

function openEdit(id) {
  const p = projects.find(x => x.id === id);
  if (!p) return;
  editingId = id;
  document.getElementById('modal-heading').textContent = p.name;
  document.getElementById('btn-delete').style.display = '';
  fillForm(p);
  document.getElementById('modal-overlay').classList.add('open');
}

function clearForm() {
  ['f-name','f-contact','f-budget','f-notes','f-idea','f-script','f-shoot-date','f-deadline'].forEach(id => document.getElementById(id).value = '');
  document.getElementById('f-stage').value = '0';
  document.getElementById('f-paid').value = 'no';
  document.getElementById('f-owner').value = currentUser;
  ['t-me','t-yan','t-vlad','t-elvin'].forEach(id => document.getElementById(id).checked = false);
  ['idea','script','scriptok','date','shot','edit','draft','review','final'].forEach(k => { const el = document.getElementById('ck-'+k); if(el) el.checked = false; });
}

function fillForm(p) {
  document.getElementById('f-name').value = p.name || '';
  document.getElementById('f-contact').value = p.contact || '';
  document.getElementById('f-budget').value = p.budget || '';
  document.getElementById('f-notes').value = p.notes || '';
  document.getElementById('f-idea').value = p.idea || '';
  document.getElementById('f-script').value = p.script || '';
  document.getElementById('f-shoot-date').value = p.shootDate || '';
  document.getElementById('f-deadline').value = p.deadline || '';
  document.getElementById('f-stage').value = p.stage;
  document.getElementById('f-paid').value = p.paid || 'no';
  document.getElementById('f-owner').value = p.owner || 'Я (Автор)';
  const teamMap = { 'Я (Автор)':'t-me','Ян':'t-yan','Влад':'t-vlad','Элвин':'t-elvin' };
  ['t-me','t-yan','t-vlad','t-elvin'].forEach(id => document.getElementById(id).checked = false);
  (p.team||[]).forEach(m => { if(teamMap[m]) document.getElementById(teamMap[m]).checked = true; });
  const checks = p.checks || {};
  ['idea','script','scriptok','date','shot','edit','draft','review','final'].forEach(k => { const el = document.getElementById('ck-'+k); if(el) el.checked = !!checks[k]; });
}

function saveProject() {
  const name = document.getElementById('f-name').value.trim();
  if (!name) { alert('Введите название клиента!'); return; }
  const team = [];
  if (document.getElementById('t-me').checked) team.push('Я (Автор)');
  if (document.getElementById('t-yan').checked) team.push('Ян');
  if (document.getElementById('t-vlad').checked) team.push('Влад');
  if (document.getElementById('t-elvin').checked) team.push('Элвин');
  const checks = {};
  ['idea','script','scriptok','date','shot','edit','draft','review','final'].forEach(k => { checks[k] = document.getElementById('ck-'+k).checked; });
  const now = new Date();
  const timeStr = `${now.getDate().toString().padStart(2,'0')}.${(now.getMonth()+1).toString().padStart(2,'0')} ${now.getHours().toString().padStart(2,'0')}:${now.getMinutes().toString().padStart(2,'0')}`;

  if (editingId) {
    const idx = projects.findIndex(x => x.id === editingId);
    const old = projects[idx];
    const logEntry = { time: timeStr, user: currentUser, msg: `Обновлён этап → ${STAGES[+document.getElementById('f-stage').value].name.replace(/[^\w\s]/g,'')}` };
    projects[idx] = { ...old, name, contact: document.getElementById('f-contact').value, stage: +document.getElementById('f-stage').value, owner: document.getElementById('f-owner').value, team, budget: document.getElementById('f-budget').value, paid: document.getElementById('f-paid').value, shootDate: document.getElementById('f-shoot-date').value, deadline: document.getElementById('f-deadline').value, idea: document.getElementById('f-idea').value, script: document.getElementById('f-script').value, notes: document.getElementById('f-notes').value, checks, log: [...(old.log||[]), logEntry] };
  } else {
    projects.push({ id: Date.now(), name, contact: document.getElementById('f-contact').value, stage: +document.getElementById('f-stage').value, owner: document.getElementById('f-owner').value, team, budget: document.getElementById('f-budget').value, paid: document.getElementById('f-paid').value, shootDate: document.getElementById('f-shoot-date').value, deadline: document.getElementById('f-deadline').value, idea: document.getElementById('f-idea').value, script: document.getElementById('f-script').value, notes: document.getElementById('f-notes').value, checks, log: [{ time: timeStr, user: currentUser, msg: 'Создан проект' }] });
  }
  save();
  closeModalBtn();
  render();
}

function deleteProject() {
  if (!confirm('Удалить проект?')) return;
  projects = projects.filter(x => x.id !== editingId);
  save();
  closeModalBtn();
  render();
}

function closeModal(e) { if (e.target === document.getElementById('modal-overlay')) closeModalBtn(); }
function closeModalBtn() { document.getElementById('modal-overlay').classList.remove('open'); }

function filterCards(q) {
  searchQuery = q.toLowerCase();
  render();
}

function filterStage(member, el) {
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  el.classList.add('active');
  filterMember = member;
  render();
}

// Close notif panel on outside click
document.addEventListener('click', e => {
  const panel = document.getElementById('notif-panel');
  const btn = document.getElementById('notif-btn');
  if (!panel.contains(e.target) && !btn.contains(e.target)) panel.classList.remove('open');
});

render();
</script>

</body>
</html>
