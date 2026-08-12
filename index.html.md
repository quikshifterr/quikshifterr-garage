<!doctype html>  
<html lang="tr">  
<head>  
<meta charset="utf-8">  
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">  
<meta name="theme-color" content="#111111">  
<title>QUIKSHIFTERR Garage V11</title>  
  
<!-- Firebase SDKs (Compat) -->  
<script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-app-compat.js"></script>  
<script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-auth-compat.js"></script>  
<script src="https://www.gstatic.com/firebasejs/10.8.0/firebase-firestore-compat.js"></script>  
  
<style>  
:root {  
  --bg: #08090a;  
  --panel: #111315;  
  --line: #292d31;  
  --orange: #ff6a00;  
  --orange2: #ff8a2a;  
  --text: #f6f7f8;  
  --muted: #8e949b;  
}  
  
*, *::before, *::after { box-sizing: border-box; }  
  
body {  
  margin: 0;  
  padding: 0;  
  background: radial-gradient(circle at 50% -10%, #24201c 0, #0b0c0d 32%, #08090a 65%);  
  color: var(--text);  
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;  
}  
  
.app {  
  max-width: 540px;  
  margin: 0 auto;  
  min-height: 100vh;  
  padding-bottom: 90px;  
}  
  
header {  
  background: rgba(8, 9, 10, .92);  
  backdrop-filter: blur(18px);  
  -webkit-backdrop-filter: blur(18px);  
  border-bottom: 1px solid rgba(255, 255, 255, .07);  
  padding: 20px 18px 14px;  
  position: sticky;  
  top: 0;  
  z-index: 10;  
  display: flex;  
  justify-content: space-between;  
  align-items: center;  
}  
  
.brand { font-size: 21px; font-weight: 900; }  
.brand .orange-text { color: var(--orange); }  
.brand .white-text { color: #ffffff; }  
.brand .garage-tag {  
  font-size: 11px;  
  color: var(--orange);  
  font-weight: 700;  
  margin-left: 4px;  
  background: rgba(255,106,0,0.15);  
  padding: 2px 6px;  
  border-radius: 6px;  
  border: 1px solid rgba(255,106,0,0.3);  
}  
  
.subtitle { font-size: 10px; text-transform: uppercase; color: #777d84; margin-top: 2px; }  
  
.user-badge {  
  background: #1c2024;  
  border: 1px solid #2d3238;  
  padding: 6px 12px;  
  border-radius: 20px;  
  font-size: 11px;  
  font-weight: 700;  
  color: var(--orange);  
  cursor: pointer;  
}  
  
.page { display: none; padding: 18px; }  
.page.active { display: block; }  
  
.hero, .card {  
  background: linear-gradient(145deg, rgba(28, 31, 34, .96), rgba(15, 17, 19, .98));  
  border: 1px solid #2a2e32;  
  box-shadow: 0 14px 35px rgba(0, 0, 0, .28);  
  border-radius: 20px;  
  padding: 16px;  
  margin-bottom: 14px;  
}  
  
h1 { font-size: 26px; margin: 4px 0; }  
h2 { font-size: 18px; margin: 0 0 10px 0; }  
.muted { color: var(--muted); font-size: 12px; }  
  
.stats { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; margin-top: 14px; }  
.stat { background: #101214; border: 1px solid #262a2e; border-radius: 14px; padding: 12px; }  
.stat small { color: var(--muted); font-size: 11px; display: block; }  
.stat strong { display: block; font-size: 17px; margin-top: 4px; }  
  
button {  
  border: 0;  
  border-radius: 12px;  
  padding: 12px 14px;  
  background: linear-gradient(135deg, var(--orange2), var(--orange));  
  color: #fff;  
  font-weight: 800;  
  font-size: 13px;  
  cursor: pointer;  
}  
button.secondary { background: #24282c; color: var(--text); }  
button.danger { background: #812d2d; color: #fff; }  
  
.row { display: flex; gap: 8px; flex-wrap: wrap; }  
.between { display: flex; justify-content: space-between; align-items: center; gap: 10px; }  
  
input, select {  
  width: 100%;  
  padding: 12px;  
  background: #0c0e10;  
  color: #fff;  
  border: 1px solid #30353a;  
  border-radius: 12px;  
  margin: 6px 0 10px;  
  font-size: 14px;  
}  
  
label { display: block; font-size: 11px; font-weight: 700; color: #a6abb1; text-transform: uppercase; margin-top: 8px; }  
.grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 10px; }  
  
.item { padding: 12px 0; border-bottom: 1px solid #2a2e32; }  
.item:last-child { border: 0; }  
  
.badge { padding: 5px 8px; border-radius: 20px; background: #343434; font-size: 11px; }  
.warn { background: #7d551b; }  
.good { background: #245a38; }  
.empty { text-align: center; color: var(--muted); padding: 20px 4px; }  
  
.notice {  
  font-size: 12px;  
  color: #b8bdc3;  
  background: #101214;  
  border-left: 3px solid var(--orange);  
  padding: 12px;  
  border-radius: 12px;  
  margin-top: 10px;  
}  
  
.nav {  
  position: fixed;  
  bottom: 0;  
  left: 50%;  
  transform: translateX(-50%);  
  width: min(540px, 100%);  
  background: rgba(10, 11, 12, .95);  
  backdrop-filter: blur(18px);  
  -webkit-backdrop-filter: blur(18px);  
  border-top: 1px solid #262a2e;  
  display: grid;  
  grid-template-columns: repeat(5, 1fr);  
  padding: 6px 4px calc(6px + env(safe-area-inset-bottom));  
  z-index: 20;  
}  
  
.nav button {  
  background: transparent;  
  color: #8e949b;  
  padding: 6px 2px;  
  font-size: 10px;  
  display: flex;  
  flex-direction: column;  
  align-items: center;  
  gap: 2px;  
}  
  
.nav button.active { color: var(--orange); }  
  
.more-menu-overlay {  
  display: none;  
  position: fixed;  
  top: 0; left: 0; width: 100vw; height: 100vh;  
  background: rgba(0, 0, 0, 0.75);  
  backdrop-filter: blur(4px);  
  z-index: 90;  
}  
.more-menu-overlay.active { display: block; }  
  
.more-menu {  
  display: none;  
  position: fixed;  
  bottom: 60px;  
  left: 50%;  
  transform: translateX(-50%);  
  width: min(500px, 92%);  
  background: #14171a;  
  border: 1px solid #2a2e32;  
  border-radius: 20px;  
  padding: 18px;  
  z-index: 100;  
  max-height: 80vh;  
  overflow-y: auto;  
}  
.more-menu.active { display: block; }  
  
.more-menu-item {  
  display: flex; align-items: center; gap: 12px; width: 100%;  
  padding: 12px 16px; background: #1c2024; border: 1px solid #282c30;  
  border-radius: 12px; color: #fff; font-size: 14px; font-weight: 700; margin-bottom: 8px;  
}  
  
.speedometer-box {  
  text-align: center;  
  padding: 20px 10px;  
  background: radial-gradient(circle, #1a1d21 0%, #0d0f11 100%);  
  border-radius: 16px;  
  border: 1px solid #2d3238;  
  margin-bottom: 14px;  
}  
  
.speed-display { font-size: 56px; font-weight: 900; color: var(--orange); line-height: 1; }  
.speed-unit { font-size: 13px; color: var(--muted); text-transform: uppercase; margin-top: 4px; }  
</style>  
</head>  
<body>  
<div class="app">  
  <header>  
    <div>  
      <div class="brand">  
        <span class="orange-text">QUİK</span><span class="white-text">SHİFTERR</span>  
        <span class="garage-tag">V11</span>  
      </div>  
      <div class="subtitle">Motor bakım • yakıt • gps • masraf takip</div>  
    </div>  
    <div class="user-badge" id="userHeaderBadge" onclick="openAuthModal()">  
      <span>👤</span> <span id="userStatusText">Giriş Yap</span>  
    </div>  
  </header>  
  
  <!-- HOME PAGE -->  
  <section id="home" class="page active">  
    <div class="hero">  
      <div class="muted">MOTOSİKLETİM</div>  
      <h1 id="bikeName">Motorunu ekle</h1>  
      <div id="bikeInfo" class="muted">Marka/model ve kilometreni kaydet.</div>  
      <div class="stats">  
        <div class="stat"><small>Bu ay</small><strong id="monthTotal">0 TL</strong></div>  
        <div class="stat"><small>Toplam gider</small><strong id="total">0 TL</strong></div>  
        <div class="stat"><small>Ort. tüketim</small><strong id="avgConsumption">— L/100 km</strong></div>  
        <div class="stat"><small>Max GPS Hız</small><strong id="homeMaxSpeed">0 km/h</strong></div>  
      </div>  
    </div>  
    <div class="card">  
      <div class="between">  
        <h2>Yaklaşan Bakımlar</h2>  
        <button onclick="show('maintenance')">Tümü</button>  
      </div>  
      <div id="upcoming"></div>  
    </div>  
    <div class="card">  
      <div class="between">  
        <div>  
          <div class="muted">GÖSTERGE</div>  
          <h2 style="margin:4px 0">📡 GPS Hız Ölçer</h2>  
          <div class="muted">Anlık, ortalama ve son hız kaydı.</div>  
        </div>  
        <button onclick="show('gps')">Aç</button>  
      </div>  
    </div>  
  </section>  
  
  <!-- GPS PAGE -->  
  <section id="gps" class="page">  
    <h2>📡 GPS Hız & Performans</h2>  
    <div class="speedometer-box">  
      <div class="speed-display" id="currentSpeed">0</div>  
      <div class="speed-unit">KM/H (ANLIK HIZ)</div>  
      <div class="row" style="justify-content:center; margin-top:16px;">  
        <button id="startGpsBtn" onclick="toggleGps()">▶️ GPS Başlat</button>  
        <button class="secondary" onclick="resetGpsSession()">↺ Sıfırla</button>  
      </div>  
    </div>  
  
    <div class="card">  
      <h2>Mevcut Sürüş Verileri</h2>  
      <div class="stats">  
        <div class="stat"><small>Anlık Max Hız</small><strong id="sessionMax">0 km/h</strong></div>  
        <div class="stat"><small>Süre</small><strong id="sessionTime">00:00</strong></div>  
      </div>  
    </div>  
  </section>  
  
  <!-- FUEL PAGE -->  
  <section id="fuel" class="page">  
    <h2>⛽ Yakıt Takibi</h2>  
    <div class="card">  
      <div class="grid">  
        <div><label>Tarih</label><input id="fDate" type="date"></div>  
        <div><label>KM</label><input id="fKm" type="number"></div>  
        <div><label>Litre</label><input id="fLiters" type="number" step=".01"></div>  
        <div><label>Tutar (TL)</label><input id="fCost" type="number" step=".01"></div>  
      </div>  
      <button onclick="addFuel()" style="width:100%; margin-top:6px;">Yakıtı Kaydet</button>  
    </div>  
    <div class="card"><div id="fuelList"></div></div>  
  </section>  
  
  <!-- MAINTENANCE PAGE -->  
  <section id="maintenance" class="page">  
    <h2>🔧 Bakım & Hatırlatıcı</h2>  
    <div class="card">  
      <label>Bakım / Parça</label>  
      <input id="mName" placeholder="Örn. Motor yağı">  
      <div class="grid">  
        <div><label>Bakım tarihi</label><input id="mDate" type="date"></div>  
        <div><label>Bakım KM</label><input id="mKm" type="number"></div>  
      </div>  
      <button class="secondary" onclick="addMaintenance()" style="width:100%; margin-top:8px;">Bakımı Kaydet</button>  
    </div>  
    <div class="card"><div id="maintenanceList"></div></div>  
  </section>  
  
  <!-- EXPENSES PAGE -->  
  <section id="expenses" class="page">  
    <h2>💸 Masraflar</h2>  
    <div class="card">  
      <div class="grid">  
        <div>  
          <label>Kategori</label>  
          <select id="eCat">  
            <option>Bakım</option>  
            <option>Parça</option>  
            <option>Yakıt</option>  
            <option>Sigorta</option>  
            <option>Ekipman</option>  
          </select>  
        </div>  
        <div><label>Tutar (TL)</label><input id="eCost" type="number" step=".01"></div>  
      </div>  
      <button onclick="addExpense()" style="width:100%;">Masrafı Kaydet</button>  
    </div>  
    <div class="card"><div id="expenseList"></div></div>  
  </section>  
  
  <!-- BIKE PAGE -->  
  <section id="bike" class="page">  
    <h2>🏍️ Motorum</h2>  
    <div class="card">  
      <label>Marka / Model</label>  
      <input id="bName" placeholder="KTM Duke 250">  
      <div class="grid">  
        <div><label>Model yılı</label><input id="bYear" type="number"></div>  
        <div><label>Güncel KM</label><input id="bKm" type="number"></div>  
      </div>  
      <button onclick="saveBike()" style="width:100%; margin-top:8px;">Motoru Kaydet</button>  
    </div>  
  </section>  
  
  <!-- BOTTOM NAV -->  
  <nav class="nav">  
    <button onclick="show('home')" id="n-home" class="active"><span>⌂</span><span>Ana Sayfa</span></button>  
    <button onclick="show('fuel')" id="n-fuel"><span>⛽</span><span>Yakıt</span></button>  
    <button onclick="show('gps')" id="n-gps"><span>📡</span><span>GPS Hız</span></button>  
    <button onclick="show('maintenance')" id="n-maintenance"><span>🔧</span><span>Bakım</span></button>  
    <button onclick="toggleMoreMenu()" id="n-more"><span>•••</span><span>Menü</span></button>  
  </nav>  
  
  <!-- OVERLAYS -->  
  <div class="more-menu-overlay" id="moreOverlay" onclick="closeAllModals()"></div>  
    
  <div class="more-menu" id="moreMenu">  
    <button class="more-menu-item" onclick="selectMoreNav('expenses')"><span>💸</span> <span>Masraflar</span></button>  
    <button class="more-menu-item" onclick="selectMoreNav('bike')"><span>🏍️</span> <span>Motor Garajım</span></button>  
  </div>  
  
  <div class="more-menu" id="authModal">  
    <div id="authLoggedOut">  
      <h2>👤 Giriş Yap / Kayıt Ol</h2>  
      <label>E-posta Adresi</label>  
      <input id="authEmail" type="email">  
      <label>Şifre</label>  
      <input id="authPassword" type="password">  
      <div class="row" style="margin-top:10px;">  
        <button onclick="handleLogin()" style="flex:1;">Giriş Yap</button>  
        <button class="secondary" onclick="handleRegister()" style="flex:1;">Kayıt Ol</button>  
      </div>  
    </div>  
    <div id="authLoggedIn" style="display:none;">  
      <h2>👤 Hesabım</h2>  
      <p id="userEmailDisplay"></p>  
      <button class="danger" onclick="handleLogout()" style="width:100%;">Çıkış Yap</button>  
    </div>  
  </div>  
</div>  
  
<script>  
// --- YOUR REAL FIREBASE CONFIGURATION ---  
const firebaseConfig = {  
  apiKey: "AIzaSyBpKCbF2SgCiQ5BT7yGNEgpvMptnG7WMTc",  
  authDomain: "quikshifterr.firebaseapp.com",  
  projectId: "quikshifterr",  
  storageBucket: "quikshifterr.firebasestorage.app",  
  messagingSenderId: "507874811786",  
  appId: "1:507874811786:web:056b74e2df314aeba53273",  
  measurementId: "G-72YWKGTHDR"  
};  
  
let db = null;  
let currentUser = null;  
  
try {  
  firebase.initializeApp(firebaseConfig);  
  db = firebase.firestore();  
} catch(e) { console.log(e); }  
  
const KEY = 'qsGarageV11';  
let data = JSON.parse(localStorage.getItem(KEY) || '{"bike":{},"fuel":[],"expenses":[],"maintenance":[],"maxSpeed":0}');  
  
function save() {  
  localStorage.setItem(KEY, JSON.stringify(data));  
  if (db && currentUser) {  
    db.collection("garages").doc(currentUser.uid).set(data).catch(err => console.error(err));  
  }  
  render();  
}  
  
function money(n) { return Number(n || 0).toLocaleString('tr-TR', { minimumFractionDigits: 2 }) + ' TL'; }  
  
function closeAllModals() {  
  document.querySelectorAll('.more-menu').forEach(m => m.classList.remove('active'));  
  document.getElementById('moreOverlay').classList.remove('active');  
}  
  
function toggleMoreMenu() {  
  const menu = document.getElementById('moreMenu');  
  const overlay = document.getElementById('moreOverlay');  
  const isActive = menu.classList.contains('active');  
  closeAllModals();  
  if (!isActive) { menu.classList.add('active'); overlay.classList.add('active'); }  
}  
  
function openAuthModal() {  
  closeAllModals();  
  document.getElementById('authModal').classList.add('active');  
  document.getElementById('moreOverlay').classList.add('active');  
}  
  
if (window.firebase && firebase.auth) {  
  firebase.auth().onAuthStateChanged(user => {  
    currentUser = user;  
    if (user) {  
      document.getElementById('userStatusText').textContent = user.email ? user.email.split('@')[0] : "Giriş Yapıldı";  
      document.getElementById('authLoggedOut').style.display = 'none';  
      document.getElementById('authLoggedIn').style.display = 'block';  
      document.getElementById('userEmailDisplay').textContent = user.email || '';  
      if (db) {  
        db.collection("garages").doc(user.uid).get().then(doc => {  
          if (doc.exists) { data = doc.data(); localStorage.setItem(KEY, JSON.stringify(data)); render(); }  
        });  
      }  
    } else {  
      document.getElementById('userStatusText').textContent = "Giriş Yap";  
      document.getElementById('authLoggedOut').style.display = 'block';  
      document.getElementById('authLoggedIn').style.display = 'none';  
    }  
  });  
}  
  
function handleLogin() {  
  firebase.auth().signInWithEmailAndPassword(authEmail.value.trim(), authPassword.value)  
    .then(() => closeAllModals()).catch(e => alert(e.message));  
}  
  
function handleRegister() {  
  firebase.auth().createUserWithEmailAndPassword(authEmail.value.trim(), authPassword.value)  
    .then(() => { save(); closeAllModals(); }).catch(e => alert(e.message));  
}  
  
function handleLogout() { firebase.auth().signOut().then(() => closeAllModals()); }  
  
function selectMoreNav(id) { closeAllModals(); show(id); }  
  
function show(id) {  
  document.querySelectorAll('.page').forEach(x => x.classList.remove('active'));  
  document.getElementById(id).classList.add('active');  
  document.querySelectorAll('.nav button').forEach(x => x.classList.remove('active'));  
  let btn = document.getElementById('n-' + id);  
  if (btn) btn.classList.add('active');  
  else document.getElementById('n-more').classList.add('active');  
  render();  
}  
  
function saveBike() {  
  data.bike = { name: bName.value.trim(), year: bYear.value, km: Number(bKm.value || 0) };  
  save(); show('home');  
}  
  
function addFuel() {  
  let liters = +fLiters.value, cost = +fCost.value, km = +fKm.value;  
  if (!liters || !cost || !km) return alert('Litre, tutar ve KM gir.');  
  data.fuel.push({ date: fDate.value || new Date().toISOString().slice(0, 10), km, liters, cost });  
  data.expenses.unshift({ cat: 'Yakıt', cost, note: `${liters} L`, date: new Date().toISOString().slice(0, 10) });  
  data.bike.km = km;  
  save(); fLiters.value = fCost.value = fKm.value = '';  
}  
  
function addExpense() {  
  if (!+eCost.value) return;  
  data.expenses.unshift({ cat: eCat.value, cost: +eCost.value, date: new Date().toISOString().slice(0, 10) });  
  save(); eCost.value = '';  
}  
  
function addMaintenance() {  
  if (!mName.value || !mDate.value) return;  
  data.maintenance.push({ name: mName.value.trim(), date: mDate.value, km: +mKm.value || 0 });  
  save(); mName.value = mDate.value = mKm.value = '';  
}  
  
function render() {  
  bikeName.textContent = data.bike.name || 'Motorunu ekle';  
  bikeInfo.textContent = data.bike.name ? `${data.bike.year || ''} • ${(data.bike.km || 0).toLocaleString('tr-TR')} km` : 'Marka/model ve kilometreni kaydet.';  
    
  let total = data.expenses.reduce((a, x) => a + Number(x.cost || 0), 0);  
  document.getElementById('total').textContent = money(total);  
  document.getElementById('homeMaxSpeed').textContent = (data.maxSpeed || 0) + ' km/h';  
  
  upcoming.innerHTML = data.maintenance.length ? data.maintenance.slice(-5).reverse().map(x => `<div class="item between"><span>🔧 ${x.name}<br><small class="muted">${x.date}</small></span></div>`).join('') : '<div class="empty">Bakım kaydı yok.</div>';  
  fuelList.innerHTML = data.fuel.length ? data.fuel.map(x => `<div class="item between"><span>⛽ ${x.liters} L • ${x.km} km</span><b>${money(x.cost)}</b></div>`).join('') : '<div class="empty">Yakıt kaydı yok.</div>';  
  expenseList.innerHTML = data.expenses.length ? data.expenses.map(x => `<div class="item between"><span>${x.cat}</span><b>${money(x.cost)}</b></div>`).join('') : '<div class="empty">Masraf kaydı yok.</div>';  
}  
  
render();  
  
/* GPS ENGINE */  
let watchId = null, gpsActive = false, sessionMaxSpeed = 0;  
  
function toggleGps() { gpsActive ? stopGps() : startGps(); }  
  
function startGps() {  
  gpsActive = true;  
  document.getElementById('startGpsBtn').textContent = "⏹️ GPS Durdur";  
  watchId = navigator.geolocation.watchPosition(pos => {  
    let speedKm = pos.coords.speed ? Math.round(pos.coords.speed * 3.6) : 0;  
    document.getElementById('currentSpeed').textContent = speedKm;  
    if (speedKm > sessionMaxSpeed) {  
      sessionMaxSpeed = speedKm;  
      if (sessionMaxSpeed > (data.maxSpeed || 0)) { data.maxSpeed = sessionMaxSpeed; save(); }  
    }  
    document.getElementById('sessionMax').textContent = sessionMaxSpeed + " km/h";  
  }, err => {}, { enableHighAccuracy: true });  
}  
  
function stopGps() {  
  if (watchId !== null) navigator.geolocation.clearWatch(watchId);  
  gpsActive = false;  
  document.getElementById('startGpsBtn').textContent = "▶️ GPS Başlat";  
}  
  
function resetGpsSession() {  
  stopGps(); sessionMaxSpeed = 0;  
  document.getElementById('currentSpeed').textContent = "0";  
  document.getElementById('sessionMax').textContent = "0 km/h";  
}  
</script>  
</body>  
</html>  
