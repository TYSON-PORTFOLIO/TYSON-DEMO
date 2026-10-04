<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>🎮Tyson Games Demo Dashboard</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', Tahoma, sans-serif; }

  body {
    background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
    min-height: 100vh;
    padding: 20px;
    color: #fff;
  }

  /* ---------------- HEADER ---------------- */
  .header {
    text-align: center;
    margin-bottom: 25px;
    padding: 20px 15px 10px;
  }

  .header-title-row {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 14px;
    flex-wrap: wrap;
    margin-bottom: 12px;
  }

  .header-icon {
    width: 52px;
    height: 52px;
    border-radius: 50%;
    object-fit: cover;
    border: 2px solid rgba(0, 210, 255, 0.6);
    box-shadow: 0 0 18px rgba(0, 210, 255, 0.55);
    flex: 0 0 auto;
    background: #111;
    transition: transform 0.3s;
  }

  .header-icon:hover { transform: scale(1.08) rotate(3deg); }

  .header h1 {
    font-size: 2.5rem;
    background: linear-gradient(90deg, #00d2ff, #3a7bd5, #ff00cc);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    text-shadow: 0 0 30px rgba(0, 210, 255, 0.3);
    line-height: 1.2;
  }

  .header p { color: #b0b0d0; font-size: 1rem; }

  /* ---------------- OWNER CREDIT ---------------- */
  .owner-card {
    max-width: 720px;
    margin: 0 auto 30px;
    padding: 18px 22px;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(0, 210, 255, 0.25);
    border-radius: 18px;
    backdrop-filter: blur(12px);
    text-align: center;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.25);
  }

  .owner-name {
    font-size: 1.05rem;
    font-weight: 700;
    background: linear-gradient(90deg, #00d2ff, #ff00cc);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
    margin-bottom: 6px;
    letter-spacing: 0.5px;
  }

  .owner-tag {
    font-size: 0.85rem;
    color: #b0b0d0;
    margin-bottom: 14px;
    line-height: 1.5;
  }

  .owner-tag b { color: #00d2ff; font-weight: 700; }

  .owner-links {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
  }

  .owner-btn {
    display: inline-flex;
    align-items: center;
    gap: 7px;
    padding: 9px 16px;
    border-radius: 30px;
    font-size: 13px;
    font-weight: 600;
    text-decoration: none;
    color: #fff;
    transition: 0.3s;
    border: 1px solid rgba(255, 255, 255, 0.15);
    white-space: nowrap;
  }

  .owner-btn:hover {
    transform: translateY(-2px);
    filter: brightness(1.15);
    box-shadow: 0 8px 18px rgba(0, 0, 0, 0.35);
  }

  .owner-btn.call    { background: linear-gradient(90deg, #00d2ff, #3a7bd5); }
  .owner-btn.whatsapp{ background: linear-gradient(90deg, #11998e, #38ef7d); color: #04231a; }
  .owner-btn.telegram{ background: linear-gradient(90deg, #2196f3, #00bcd4); }

  /* ---------------- CONTROLS ---------------- */
  .controls {
    display: flex; flex-wrap: wrap; gap: 12px;
    justify-content: center; margin-bottom: 30px;
  }

  .search-box { flex: 1; min-width: 250px; max-width: 500px; position: relative; }

  .search-box input {
    width: 100%;
    padding: 14px 45px 14px 20px;
    border-radius: 30px;
    border: 2px solid rgba(0, 210, 255, 0.3);
    background: rgba(255, 255, 255, 0.05);
    color: #fff; font-size: 15px; outline: none;
    transition: 0.3s; backdrop-filter: blur(10px);
  }

  .search-box input:focus {
    border-color: #00d2ff;
    box-shadow: 0 0 20px rgba(0, 210, 255, 0.4);
  }

  .search-box input::placeholder { color: #888; }

  .search-box::after {
    content: "🔍"; position: absolute; right: 18px; top: 50%;
    transform: translateY(-50%); font-size: 16px; pointer-events: none;
  }

  .filter-btn {
    padding: 12px 24px; border-radius: 30px;
    border: 2px solid rgba(255, 255, 255, 0.2);
    background: rgba(255, 255, 255, 0.05);
    color: #fff; cursor: pointer; font-size: 14px; font-weight: 600;
    transition: 0.3s; backdrop-filter: blur(10px);
  }

  .filter-btn:hover, .filter-btn.active {
    background: linear-gradient(90deg, #00d2ff, #3a7bd5);
    border-color: transparent;
    transform: translateY(-2px);
    box-shadow: 0 8px 20px rgba(0, 210, 255, 0.4);
  }

  .filter-btn:focus-visible,
  .link-btn:focus-visible,
  .copy-btn:focus-visible,
  .owner-btn:focus-visible,
  .search-box input:focus-visible {
    outline: 2px solid #00d2ff;
    outline-offset: 3px;
  }

  /* ---------------- STATS ---------------- */
  .stats {
    display: flex; gap: 15px; justify-content: center;
    flex-wrap: wrap; margin-bottom: 30px;
  }

  .stat-card {
    padding: 15px 25px; background: rgba(255, 255, 255, 0.05);
    border-radius: 15px; border: 1px solid rgba(255, 255, 255, 0.1);
    text-align: center; backdrop-filter: blur(10px); min-width: 120px;
  }

  .stat-card .num {
    font-size: 1.8rem; font-weight: bold;
    background: linear-gradient(90deg, #00d2ff, #ff00cc);
    -webkit-background-clip: text; background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .stat-card .lbl {
    font-size: 12px; color: #b0b0d0;
    text-transform: uppercase; letter-spacing: 1px;
  }

  /* ---------------- GRID / CARDS ---------------- */
  .grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
    gap: 20px; max-width: 1400px; margin: 0 auto;
  }

  .card {
    background: rgba(255, 255, 255, 0.05);
    border-radius: 20px; padding: 22px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(15px);
    transition: 0.4s; position: relative; overflow: hidden;
  }

  .card::before {
    content: ""; position: absolute; top: 0; left: 0; right: 0; height: 4px;
    background: linear-gradient(90deg, #00d2ff, #3a7bd5, #ff00cc);
    opacity: 0.7;
  }

  .card:hover {
    transform: translateY(-8px);
    border-color: rgba(0, 210, 255, 0.5);
    box-shadow: 0 20px 40px rgba(0, 210, 255, 0.2);
  }

  .card-header {
    display: flex; justify-content: space-between;
    align-items: flex-start; margin-bottom: 18px; gap: 10px;
  }

  .card-title { font-size: 1.2rem; font-weight: 700; color: #fff; line-height: 1.3; }

  .badge {
    padding: 5px 12px; border-radius: 20px;
    font-size: 11px; font-weight: 700; text-transform: uppercase;
    letter-spacing: 0.5px; white-space: nowrap;
  }

  .badge.color-prediction {
    background: linear-gradient(90deg, #ff512f, #dd2476);
    box-shadow: 0 0 15px rgba(255, 81, 47, 0.4);
  }

  .badge.casino {
    background: linear-gradient(90deg, #11998e, #38ef7d);
    color: #000;
    box-shadow: 0 0 15px rgba(56, 239, 125, 0.4);
  }

  .info-row {
    display: flex; justify-content: space-between; align-items: center;
    padding: 8px 0; font-size: 13px;
    border-bottom: 1px dashed rgba(255, 255, 255, 0.1);
  }

  .info-row:last-of-type { border-bottom: none; }

  .info-label { color: #888; flex: 0 0 auto; }

  .info-value {
    color: #00d2ff;
    font-family: 'Courier New', monospace;
    font-weight: 600;
    display: flex; align-items: center; gap: 5px;
    min-width: 0; max-width: 62%;
  }

  .val-text { overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }

  .links { display: flex; gap: 10px; margin-top: 18px; }

  .link-btn {
    flex: 1; padding: 10px; text-align: center;
    border-radius: 10px; text-decoration: none;
    font-size: 13px; font-weight: 600; transition: 0.3s;
  }

  .link-btn.user { background: linear-gradient(90deg, #00d2ff, #3a7bd5); color: #fff; }
  .link-btn.admin { background: linear-gradient(90deg, #ff512f, #dd2476); color: #fff; }

  .link-btn:hover { transform: scale(1.05); filter: brightness(1.2); }

  .copy-btn {
    flex: 0 0 auto;
    background: rgba(255, 255, 255, 0.1);
    border: none; color: #00d2ff;
    padding: 2px 6px; border-radius: 4px;
    font-size: 11px; cursor: pointer; transition: 0.2s;
  }

  .copy-btn:hover { background: rgba(0, 210, 255, 0.2); }

  .empty {
    grid-column: 1 / -1; text-align: center;
    padding: 60px 20px; color: #888; font-size: 1.1rem;
  }

  /* ---------------- FOOTER ---------------- */
  .footer {
    text-align: center;
    margin-top: 40px;
    padding: 22px 15px 10px;
    color: #8a8ab0;
    font-size: 13px;
    border-top: 1px solid rgba(255, 255, 255, 0.08);
    max-width: 1400px;
    margin-left: auto;
    margin-right: auto;
    line-height: 1.8;
  }

  .footer .brand {
    font-weight: 700;
    background: linear-gradient(90deg, #00d2ff, #ff00cc);
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;
  }

  .footer a { color: #00d2ff; text-decoration: none; }
  .footer a:hover { text-decoration: underline; }

  /* ---------------- TOAST ---------------- */
  .toast {
    position: fixed; bottom: 30px; left: 50%;
    transform: translateX(-50%) translateY(100px);
    background: linear-gradient(90deg, #11998e, #38ef7d);
    color: #000; padding: 12px 25px; border-radius: 30px;
    font-weight: 600; opacity: 0; transition: 0.4s;
    z-index: 999; box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
    max-width: 90vw; text-align: center;
  }

  .toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }
  .toast.error { background: linear-gradient(90deg, #ff512f, #dd2476); color: #fff; }

  @media (max-width: 600px) {
    .header h1 { font-size: 1.55rem; }
    .header-icon { width: 42px; height: 42px; }
    .header-title-row { gap: 10px; }
    .grid { grid-template-columns: 1fr; }
    .stat-card { flex: 1; padding: 12px 15px; min-width: 90px; }
    .info-value { max-width: 55%; }
    .owner-btn { font-size: 12px; padding: 8px 13px; }
  }
</style>
</head>
<body>

<!-- ================= HEADER ================= -->
<div class="header">
  <div class="header-title-row">
    <img class="header-icon"
         src="https://www.image2url.com/r2/default/images/1782060674321-f50f86c8-f27d-41cf-b670-8910cd19d5b1.jpg"
         alt="Tyson Owner Logo"
         onerror="this.style.display='none'">
    <h1>🎮 Games Demo Dashboard</h1>
  </div>
  <p>All gaming platforms - User &amp; Admin access at your fingertips</p>
</div>

<!-- ================= OWNER CREDIT ================= -->
<div class="owner-card">
  <div class="owner-name">⚡ Tyson_Owner Team • Hack</div>
  <div class="owner-tag">
    Add owner credit <b>@TYSON_OWNER</b>
  </div>
  <div class="owner-links">
    <a class="owner-btn call" href="tel:+918092043236">📞 Call 8092043236</a>
    <a class="owner-btn whatsapp" href="https://wa.me/918092043236" target="_blank" rel="noopener noreferrer">💬 WhatsApp 8092043236</a>
    <a class="owner-btn telegram" href="https://t.me/pluginxpertcode" target="_blank" rel="noopener noreferrer">✈️ Telegram @pluginxpertcode</a>
  </div>
</div>

<!-- ================= STATS ================= -->
<div class="stats">
  <div class="stat-card">
    <div class="num" id="totalCount">0</div>
    <div class="lbl">Total</div>
  </div>
  <div class="stat-card">
    <div class="num" id="colorCount">0</div>
    <div class="lbl">Color Prediction</div>
  </div>
  <div class="stat-card">
    <div class="num" id="casinoCount">0</div>
    <div class="lbl">Casino</div>
  </div>
</div>

<!-- ================= CONTROLS ================= -->
<div class="controls">
  <div class="search-box">
    <input type="text" id="searchInput" placeholder="Search games..." aria-label="Search games">
  </div>
  <button class="filter-btn active" data-filter="all">All</button>
  <button class="filter-btn" data-filter="color-prediction">Color Prediction</button>
  <button class="filter-btn" data-filter="casino">Casino</button>
</div>

<!-- ================= GRID ================= -->
<div class="grid" id="gamesGrid"></div>

<!-- ================= FOOTER ================= -->
<div class="footer">
  <div>© <span id="year"></span> <span class="brand">Tyson_Owner Team</span> — All Rights Reserved</div>
  <div>
    📞 <a href="tel:+918092043236">8092043236</a> &nbsp;•&nbsp;
    💬 <a href="https://wa.me/918092043236" target="_blank" rel="noopener noreferrer">WhatsApp</a> &nbsp;•&nbsp;
    ✈️ <a href="https://t.me/pluginxpertcode" target="_blank" rel="noopener noreferrer">Telegram</a>
  </div>
  <div style="margin-top:6px;font-size:12px;opacity:0.75;">Hack &amp; Add Owner Credit — @TYSON_OWNER</div>
</div>

<!-- ================= TOAST ================= -->
<div class="toast" id="toast" role="status" aria-live="polite">✅ Copied!</div>

<script>
/* ------------------------------------------------------------------
   DATA
   NOTE: credentials are hard-coded and shipped to every visitor.
   If these are real, anyone can read them. Move to a backend + auth.
------------------------------------------------------------------ */
const gamesData = [
  { name: "Mudiclub Demo", category: "color-prediction", userUrl: "https://dmzones.top/#/register?invitationCode=926677022481", username: "9898989898", password: "9898989898", adminUrl: "https://dmzones.top/main", adminUser: "9898989898", adminPass: "9898989898" },
  { name: "Dkwin BDT Demo", category: "color-prediction", userUrl: "https://bitbox.space/#/register?invitationCode=official", username: "9898989898", password: "9898989898", adminUrl: "https://bitbox.space/Adminxxx/", adminUser: "9898989898", adminPass: "9898989898" },
  { name: "BANGLADESH", category: "casino", userUrl: "https://bdgbdt.site/", username: "9898989898", password: "9898989898", adminUrl: "https://bdgbdt.site/Chub94", adminUser: "9898989898", adminPass: "9898989898" },
  { name: "JEETOSHOP", category: "color-prediction", userUrl: "https://jeetoshop.site", username: "9898989898", password: "9898989898", adminUrl: "https://jeetoshop.site/24gameadmin", adminUser: "9898989898", adminPass: "9898989898" },
  { name: "DIUWIN", category: "color-prediction", userUrl: "https://sixclubzones.top", username: "9898989898", password: "9898989898", adminUrl: "https://sixclubzones.top/admin", adminUser: "9898989898", adminPass: "9898989898" },
  { name: "Satka matka Result Demo", category: "color-prediction", userUrl: "https://coursemandi.in/", username: "admin", password: "12345678", adminUrl: "https://coursemandi.in/admin", adminUser: "admin", adminPass: "12345678" },
  { name: "Satka matka App Demo", category: "color-prediction", userUrl: "https://jalwagagamer.shop", username: "admin", password: "12345678", adminUrl: "https://jalwagagamer.shop/admin", adminUser: "admin", adminPass: "12345678" },
  { name: "Satta matka Website Demo", category: "color-prediction", userUrl: "https://jackpotonline.shop/", username: "admin", password: "12345678", adminUrl: "https://jackpotonline.shop/", adminUser: "admin", adminPass: "12345678" },
  { name: "64 Trading Demo", category: "casino", userUrl: "https://64trade.site/", username: "admin", password: "12345678", adminUrl: "https://64trade.site/", adminUser: "admin", adminPass: "12345678" },
  { name: "Ludo Tournament Demo", category: "casino", userUrl: "https://tejbit.sbs/", username: "mereram@gmail.com", password: "12345678", adminUrl: "https://tejbit.sbs/master", adminUser: "mereram@gmail.com", adminPass: "12345678" },
];

const CATEGORY_LABEL = {
  'color-prediction': 'Color',
  'casino': 'Casino'
};

const grid = document.getElementById('gamesGrid');
const searchInput = document.getElementById('searchInput');
const toastEl = document.getElementById('toast');
let currentFilter = 'all';
let toastTimer = null;

/* ------------------------------------------------------------------
   HELPERS
------------------------------------------------------------------ */
const escapeHtml = (value) => String(value).replace(/[&<>"']/g, (ch) => ({
  '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;'
}[ch]));

const safeUrl = (url) => {
  try {
    const parsed = new URL(url, window.location.origin);
    return (parsed.protocol === 'http:' || parsed.protocol === 'https:') ? parsed.href : '#';
  } catch {
    return '#';
  }
};

function showToast(msg, isError = false) {
  toastEl.textContent = msg;
  toastEl.classList.toggle('error', isError);
  toastEl.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => toastEl.classList.remove('show'), 1800);
}

async function copyText(text) {
  try {
    if (navigator.clipboard && window.isSecureContext) {
      await navigator.clipboard.writeText(text);
    } else {
      const ta = document.createElement('textarea');
      ta.value = text;
      ta.setAttribute('readonly', '');
      ta.style.cssText = 'position:fixed;top:-1000px;opacity:0;';
      document.body.appendChild(ta);
      ta.select();
      document.execCommand('copy');
      ta.remove();
    }
    showToast('✅ Copied: ' + text);
  } catch {
    showToast('❌ Copy failed', true);
  }
}

/* ------------------------------------------------------------------
   STATS
------------------------------------------------------------------ */
const countBy = (cat) => gamesData.filter(g => g.category === cat).length;
document.getElementById('totalCount').textContent = gamesData.length;
document.getElementById('colorCount').textContent = countBy('color-prediction');
document.getElementById('casinoCount').textContent = countBy('casino');
document.getElementById('year').textContent = new Date().getFullYear();

/* ------------------------------------------------------------------
   RENDER
------------------------------------------------------------------ */
function credentialRow(label, value) {
  return `
    <div class="info-row">
      <span class="info-label">${label}</span>
      <span class="info-value">
        <span class="val-text" title="${escapeHtml(value)}">${escapeHtml(value)}</span>
        <button class="copy-btn" type="button"
                data-copy="${escapeHtml(value)}"
                aria-label="Copy ${label}">📋</button>
      </span>
    </div>`;
}

function renderGames() {
  const query = searchInput.value.toLowerCase().trim();

  const filtered = gamesData.filter((g) => {
    const matchFilter = currentFilter === 'all' || g.category === currentFilter;
    if (!matchFilter) return false;
    if (!query) return true;
    return [g.name, g.category, g.username, g.adminUser, g.userUrl, g.adminUrl]
      .some(field => String(field).toLowerCase().includes(query));
  });

  if (filtered.length === 0) {
    grid.innerHTML = '<div class="empty">🔍 No games found</div>';
    return;
  }

  grid.innerHTML = filtered.map((g) => `
    <div class="card">
      <div class="card-header">
        <div class="card-title">${escapeHtml(g.name)}</div>
        <span class="badge ${escapeHtml(g.category)}">
          ${escapeHtml(CATEGORY_LABEL[g.category] || g.category)}
        </span>
      </div>

      ${credentialRow('👤 User', g.username)}
      ${credentialRow('🔑 Pass', g.password)}
      ${credentialRow('🛡️ Admin', g.adminUser)}
      ${credentialRow('🔐 Admin Pass', g.adminPass)}

      <div class="links">
        <a href="${escapeHtml(safeUrl(g.userUrl))}" target="_blank"
           rel="noopener noreferrer" class="link-btn user">🎮 User Login</a>
        <a href="${escapeHtml(safeUrl(g.adminUrl))}" target="_blank"
           rel="noopener noreferrer" class="link-btn admin">⚙️ Admin Panel</a>
      </div>
    </div>
  `).join('');
}

/* ------------------------------------------------------------------
   EVENTS
------------------------------------------------------------------ */
grid.addEventListener('click', (e) => {
  const btn = e.target.closest('.copy-btn');
  if (!btn) return;
  copyText(btn.dataset.copy);
});

let searchTimer = null;
searchInput.addEventListener('input', () => {
  clearTimeout(searchTimer);
  searchTimer = setTimeout(renderGames, 120);
});

document.querySelectorAll('.filter-btn').forEach((btn) => {
  btn.addEventListener('click', () => {
    document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
    btn.classList.add('active');
    currentFilter = btn.dataset.filter;
    renderGames();
  });
});

renderGames();
</script>

</body>
</html>
