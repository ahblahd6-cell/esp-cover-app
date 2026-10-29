const coverScreen = document.getElementById('coverScreen');
const dashboard = document.getElementById('dashboard');
const startBtn = document.getElementById('startBtn');
const demoBtn = document.getElementById('demoBtn');
const backBtn = document.getElementById('backBtn');
const espToggle = document.getElementById('espToggle');
const themeToggle = document.getElementById('themeToggle');

const hpValue = document.getElementById('hpValue');
const armorValue = document.getElementById('armorValue');
const xpValue = document.getElementById('xpValue');
const lvlValue = document.getElementById('lvlValue');

const lifeStat = document.getElementById('lifeStat');
const shieldStat = document.getElementById('shieldStat');
const ammoStat = document.getElementById('ammoStat');
const timeStat = document.getElementById('timeStat');

const logList = document.getElementById('logList');

function showDashboard() {
  coverScreen.classList.add('hidden');
  dashboard.classList.remove('hidden');
}

function showCover() {
  dashboard.classList.add('hidden');
  coverScreen.classList.remove('hidden');
}

startBtn.addEventListener('click', showDashboard);
demoBtn.addEventListener('click', showDashboard);
backBtn.addEventListener('click', showCover);

espToggle.addEventListener('click', () => {
  const active = espToggle.classList.contains('active');

  if (active) {
    espToggle.classList.remove('active');
    espToggle.classList.add('inactive');
    espToggle.textContent = 'ESP OFF';
  } else {
    espToggle.classList.add('active');
    espToggle.classList.remove('inactive');
    espToggle.textContent = 'ESP ON';
  }
});

themeToggle.addEventListener('click', () => {
  document.body.classList.toggle('light');
});

function updateStats() {
  const hp = Math.floor(Math.random() * 31) + 70;
  const armor = Math.floor(Math.random() * 21) + 75;
  const ammo = Math.floor(Math.random() * 18) + 12;
  const xp = `${(Math.random() * 10 + 12).toFixed(1)}k`;
  const level = Math.floor(Math.random() * 10) + 18;

  hpValue.textContent = `${hp}%`;
  armorValue.textContent = `${armor}%`;
  xpValue.textContent = xp;
  lvlValue.textContent = String(level);

  lifeStat.textContent = String(hp);
  shieldStat.textContent = String(armor);
  ammoStat.textContent = String(ammo);

  const time = new Date();
  const formatted = time.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
  timeStat.textContent = formatted;
}

function addLogEntry() {
  const time = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
  const message = [
    'Status verificado.',
    'Alvo em movimento.',
    'Novo ponto de coleta detectado.',
    'Escudo em nível ótimo.',
    'Sincronização concluída.',
    'Rede estável.'
  ];

  const entry = document.createElement('p');
  entry.innerHTML = `<span>${time}</span> ${message[Math.floor(Math.random() * message.length)]}`;
  logList.prepend(entry);

  while (logList.children.length > 5) {
    logList.removeChild(logList.lastChild);
  }
}

updateStats();
setInterval(updateStats, 3000);
setInterval(addLogEntry, 5000);
