<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Blox Fruit Profile</title>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;800&family=JetBrains+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg-main: #0f0f13;
            --bg-card: #1a1a21;
            --bg-card-hover: #22222c;
            --accent: #5865F2;
            --accent-hover: #4752c4;
            --text-main: #f2f3f5;
            --text-muted: #a3a6aa;
            --success: #23a55a;
            --danger: #f23f43;
            --warning: #f0b232;
            --border: #2b2d31;
            --fruit: #ff6b6b;
            --sword: #4ecdc4;
            --style: #ffe66d;
            --gun: #a8e6cf;
            --other: #95a5a6;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Inter', sans-serif;
            background: var(--bg-main);
            color: var(--text-main);
            min-height: 100vh;
            padding: 20px;
            background-image: 
                radial-gradient(circle at 15% 50%, rgba(88, 101, 242, 0.08), transparent 25%),
                radial-gradient(circle at 85% 30%, rgba(242, 63, 67, 0.05), transparent 25%);
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        /* ─── HEADER ─── */
        .profile-header {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 16px;
            padding: 30px;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 20px;
            flex-wrap: wrap;
            box-shadow: 0 8px 32px rgba(0,0,0,0.4);
        }

        .avatar {
            width: 80px;
            height: 80px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--accent), #eb459e);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 32px;
            font-weight: 800;
            color: white;
            flex-shrink: 0;
            box-shadow: 0 4px 20px rgba(88, 101, 242, 0.4);
        }

        .header-info { flex: 1; min-width: 200px; }
        .username {
            font-size: 28px;
            font-weight: 800;
            margin-bottom: 4px;
            background: linear-gradient(90deg, #fff, #a3a6aa);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .session-id {
            font-family: 'JetBrains Mono', monospace;
            color: var(--text-muted);
            font-size: 13px;
        }

        .status-badge {
            padding: 8px 16px;
            border-radius: 20px;
            font-size: 13px;
            font-weight: 700;
            display: flex;
            align-items: center;
            gap: 8px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        .status-online { background: rgba(35, 165, 90, 0.15); color: var(--success); border: 1px solid var(--success); }
        .status-offline { background: rgba(242, 63, 67, 0.15); color: var(--danger); border: 1px solid var(--danger); }
        .status-dot {
            width: 8px; height: 8px; border-radius: 50%; background: currentColor;
            animation: pulse 2s infinite;
        }
        @keyframes pulse {
            0%, 100% { opacity: 1; transform: scale(1); }
            50% { opacity: 0.5; transform: scale(1.2); }
        }

        /* ─── STATS GRID ─── */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
            gap: 16px;
            margin-bottom: 20px;
        }

        .stat-card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 20px;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }
        .stat-card:hover {
            background: var(--bg-card-hover);
            transform: translateY(-4px);
            box-shadow: 0 8px 24px rgba(0,0,0,0.4);
        }
        .stat-card::before {
            content: '';
            position: absolute;
            top: 0; left: 0; right: 0; height: 3px;
            background: var(--accent);
        }
        .stat-card.fruit::before { background: var(--fruit); }
        .stat-card.sword::before { background: var(--sword); }
        .stat-card.style::before { background: var(--style); }
        .stat-card.gun::before { background: var(--gun); }

        .stat-icon { font-size: 28px; margin-bottom: 8px; }
        .stat-label { font-size: 12px; color: var(--text-muted); text-transform: uppercase; letter-spacing: 0.5px; margin-bottom: 4px; font-weight: 600; }
        .stat-value { font-size: 32px; font-weight: 800; line-height: 1; }
        .stat-sub { font-size: 11px; color: var(--text-muted); margin-top: 4px; font-family: 'JetBrains Mono', monospace; }

        /* ─── INVENTORY SECTION ─── */
        .section {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 16px;
            padding: 24px;
            margin-bottom: 20px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
        }

        .section-title {
            font-size: 18px;
            font-weight: 700;
            margin-bottom: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            padding-bottom: 12px;
            border-bottom: 1px solid var(--border);
        }

        .item-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 10px;
        }

        .item {
            background: rgba(255,255,255,0.03);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 12px 14px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.2s;
        }
        .item:hover {
            background: rgba(88, 101, 242, 0.1);
            border-color: var(--accent);
        }
        .item-name { font-size: 13px; font-weight: 600; }
        .item-count {
            font-family: 'JetBrains Mono', monospace;
            background: var(--accent);
            color: white;
            padding: 2px 10px;
            border-radius: 12px;
            font-size: 12px;
            font-weight: 700;
        }

        .empty-state {
            text-align: center;
            padding: 40px;
            color: var(--text-muted);
            font-style: italic;
        }

        /* ─── LOADING & ERROR ─── */
        .loading {
            text-align: center;
            padding: 60px 20px;
            color: var(--text-muted);
        }
        .spinner {
            width: 40px; height: 40px;
            border: 3px solid var(--border);
            border-top-color: var(--accent);
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto 16px;
        }
        @keyframes spin { to { transform: rotate(360deg); } }

        .error-box {
            background: rgba(242, 63, 67, 0.1);
            border: 1px solid var(--danger);
            color: var(--danger);
            padding: 20px;
            border-radius: 12px;
            text-align: center;
        }

        /* ─── FOOTER ─── */
        .footer {
            text-align: center;
            padding: 20px;
            color: var(--text-muted);
            font-size: 12px;
            margin-top: 20px;
        }

        /* ─── RESPONSIVE ─── */
        @media (max-width: 768px) {
            .profile-header { padding: 20px; }
            .username { font-size: 22px; }
            .avatar { width: 60px; height: 60px; font-size: 24px; }
            .stat-value { font-size: 24px; }
            .item-grid { grid-template-columns: 1fr; }
        }
    </style>
</head>
<body>
    <div class="container">
        <div id="app">
            <div class="loading">
                <div class="spinner"></div>
                <div>Đang tải dữ liệu tài khoản...</div>
            </div>
        </div>
        <div class="footer">
            Powered by <strong>Blox Fruit Monitor v6.0</strong>
        </div>
    </div>

    <script>
        // ─── CẤU HÌNH ─────────────────────────────────────────
        const API_BASE = window.location.origin; // Dùng chính domain hiện tại
        const OFFLINE_THRESHOLD = 3 * 60 * 1000;  // 3 phút
        // ──────────────────────────────────────────────────────

        // Lấy username từ URL: /profile?user=TenNhanVat
        const params = new URLSearchParams(window.location.search);
        const username = params.get('user');

        if (!username) {
            document.getElementById('app').innerHTML = `
                <div class="error-box">
                    ❌ Thiếu tham số <code>?user=TenNhanVat</code> trên URL.<br>
                    Ví dụ: <code>${window.location.origin}/profile?user=PlayerName</code>
                </div>`;
        } else {
            loadProfile(username);
        }

        async function loadProfile(user) {
            try {
                const res = await fetch(`${API_BASE}/api/get-inventory/${encodeURIComponent(user)}`);
                if (!res.ok) throw new Error(`HTTP ${res.status}`);
                const json = await res.json();
                if (!json.ok) throw new Error(json.error || 'Unknown error');
                renderProfile(json.data);
            } catch (err) {
                document.getElementById('app').innerHTML = `
                    <div class="error-box">
                        ❌ Không tải được dữ liệu cho <strong>${user}</strong><br>
                        <small>${err.message}</small>
                    </div>`;
            }
        }

        function classifyItem(name) {
            const FRUITS = ["Rocket","Spin","Chop","Spring","Bomb","Smoke","Spike","Flame","Falcon","Ice","Sand","Dark","Diamond","Light","Rubber","Barrier","Ghost","Magma","Door","Quake","Human","Buddha","Love","Spider","Sound","Phoenix","Portal","Rumble","Pain","Blizzard","Gravity","Mammoth","T-Rex","Dough","Shadow","Venom","Control","Spirit","Dragon","Leopard","Kitsune","Yeti","Gas"];
            const SWORDS = ["Cutlass","Katana","Iron Mace","Dual Katana","Triple Katana","Wando","Saddi","Longsword","Shisui","Rengoku","Dark Blade","Buddy Sword","Hallow Scythe","Hollow Scythe","True Triple Katana","Cursed Dual Katana","Yama","Tushita","Koko","Trident","Shark Saw","Midnight Blade","Dragonheart","Soul Cane","Fox Lamp","Twin Hooks","Serpent Bow"];
            const STYLES = ["Combat","Dark Step","Electric Claw","Fishman Karate","Dragon Talon","Superhuman","Death Step","Sharkman Karate","Godhuman","Sanguine Art"];
            const GUNS = ["Flintlock","Slingshot","Cannon","Musket","Cursed Dual Pistols","Kabucha","Bizarre Rifle","Dragonstorm"];

            const n = name.toLowerCase();
            if (FRUITS.includes(name) || n.includes("fruit")) return "Fruit";
            if (SWORDS.includes(name) || /sword|katana|blade|scythe/.test(n)) return "Sword";
            if (STYLES.includes(name)) return "FightingStyle";
            if (GUNS.includes(name) || /gun|rifle|pistol/.test(n)) return "Gun";
            return "Other";
        }

        function timeAgo(ms) {
            const diff = Date.now() - ms;
            const sec = Math.floor(diff / 1000);
            if (sec < 60) return `${sec}s trước`;
            const min = Math.floor(sec / 60);
            if (min < 60) return `${min} phút trước`;
            const hr = Math.floor(min / 60);
            if (hr < 24) return `${hr} giờ trước`;
            return `${Math.floor(hr / 24)} ngày trước`;
        }

        function renderProfile(data) {
            const now = Date.now();
            const isOnline = (now - (data.lastSeen || 0)) < OFFLINE_THRESHOLD;
            const statusClass = isOnline ? 'status-online' : 'status-offline';
            const statusText = isOnline ? 'Online' : 'Offline';

            // Phân loại
            const groups = { Fruit: [], Sword: [], FightingStyle: [], Gun: [], Other: [] };
            let totalItems = 0;
            for (const [name, count] of Object.entries(data.inventory || {})) {
                if (count > 0) {
                    groups[classifyItem(name)].push({ name, count });
                    totalItems += count;
                }
            }
            for (const g of Object.values(groups)) {
                g.sort((a, b) => b.count - a.count);
            }

            const initial = (data.username || "?")[0].toUpperCase();
            const lastSeen = data.lastSeen ? new Date(data.lastSeen).toLocaleString('vi-VN') : 'N/A';
            const sessionStart = data.sessionStart ? new Date(data.sessionStart).toLocaleString('vi-VN') : 'N/A';
            const durationMin = data.sessionStart && data.lastSeen
                ? Math.floor((data.lastSeen - data.sessionStart) / 60000)
                : 0;

            let html = `
                <div class="profile-header">
                    <div class="avatar">${initial}</div>
                    <div class="header-info">
                        <div class="username">${data.username}</div>
                        <div class="session-id">Session: ${data.sessionId || 'N/A'}</div>
                        <div style="font-size:12px;color:var(--text-muted);margin-top:8px;">
                            Lần cuối online: ${lastSeen} · Thời lượng: ${durationMin} phút
                        </div>
                    </div>
                    <div class="status-badge ${statusClass}">
                        <span class="status-dot"></span>
                        ${statusText}
                    </div>
                </div>

                <div class="stats-grid">
                    <div class="stat-card fruit">
                        <div class="stat-icon">🍎</div>
                        <div class="stat-label">Trái</div>
                        <div class="stat-value">${groups.Fruit.length}</div>
                        <div class="stat-sub">${groups.Fruit.reduce((s,i)=>s+i.count,0)} mục</div>
                    </div>
                    <div class="stat-card sword">
                        <div class="stat-icon">⚔️</div>
                        <div class="stat-label">Kiếm</div>
                        <div class="stat-value">${groups.Sword.length}</div>
                        <div class="stat-sub">${groups.Sword.reduce((s,i)=>s+i.count,0)} mục</div>
                    </div>
                    <div class="stat-card style">
                        <div class="stat-icon">🥋</div>
                        <div class="stat-label">Võ thuật</div>
                        <div class="stat-value">${groups.FightingStyle.length}</div>
                        <div class="stat-sub">${groups.FightingStyle.reduce((s,i)=>s+i.count,0)} mục</div>
                    </div>
                    <div class="stat-card gun">
                        <div class="stat-icon">🔫</div>
                        <div class="stat-label">Súng</div>
                        <div class="stat-value">${groups.Gun.length}</div>
                        <div class="stat-sub">${groups.Gun.reduce((s,i)=>s+i.count,0)} mục</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-icon">📦</div>
                        <div class="stat-label">Tổng cộng</div>
                        <div class="stat-value">${totalItems}</div>
                        <div class="stat-sub">mục trong kho</div>
                    </div>
                </div>
            `;

            // Render từng danh mục
            const sections = [
                { key: 'Fruit',        title: '🍎 Trái (Fruits)',       class: 'fruit' },
                { key: 'Sword',        title: '⚔️ Kiếm (Swords)',       class: 'sword' },
                { key: 'FightingStyle',title: '🥋 Võ thuật (Styles)',   class: 'style' },
                { key: 'Gun',          title: '🔫 Súng (Guns)',         class: 'gun' },
                { key: 'Other',        title: '📦 Khác',                class: 'other' },
            ];

            for (const sec of sections) {
                const items = groups[sec.key];
                if (items.length === 0) continue;
                html += `
                    <div class="section">
                        <div class="section-title">
                            ${sec.title}
                            <span style="font-size:12px;color:var(--text-muted);font-weight:400;">
                                (${items.length} loại)
                            </span>
                        </div>
                        <div class="item-grid">
                            ${items.map(i => `
                                <div class="item">
                                    <span class="item-name">${i.name}</span>
                                    <span class="item-count">×${i.count}</span>
                                </div>
                            `).join('')}
                        </div>
                    </div>
                `;
            }

            if (totalItems === 0) {
                html += `<div class="section"><div class="empty-state">📭 Kho đồ trống</div></div>`;
            }

            document.getElementById('app').innerHTML = html;
        }

        // Auto refresh mỗi 60s nếu đang online
        if (username) {
            setInterval(() => loadProfile(username), 60000);
        }
    </script>
</body>
</html>
<!-- ═══════════════════════════════════════════════════════════════════ -->
<!-- TEMPLATE README CHO TỪNG TÀI KHOẢN BLOX FRUIT                    -->
<!-- Thay [USERNAME] và các số liệu bằng dữ liệu thật của bạn          -->
<!-- ═══════════════════════════════════════════════════════════════════ -->

<div align="center">

<h1>🍇 Blox Fruit Profile</h1>

### 🎮 [USERNAME]

![Status](https://img.shields.io/badge/Status-🟢_Online-23a55a?style=for-the-badge)
![Session](https://img.shields.io/badge/Session-123456-5865F2?style=for-the-badge)
![Last%20Seen](https://img.shields.io/badge/Last_Seen-2_phút_trước-a3a6aa?style=for-the-badge)

**Last updated:** `2024-11-05 14:30:00`

</div>

---

## 📊 Tổng quan

<table>
<tr>
<td align="center" width="20%">
<img src="https://img.shields.io/badge/🍎_TRÁI-5_loại-ff6b6b?style=for-the-badge" />
<br><sub><b>5</b> mục</sub>
</td>
<td align="center" width="20%">
<img src="https://img.shields.io/badge/⚔️_KIẾM-12_loại-4ecdc4?style=for-the-badge" />
<br><sub><b>15</b> mục</sub>
</td>
<td align="center" width="20%">
<img src="https://img.shields.io/badge/🥋_VÕ_THUẬT-8_loại-ffe66d?style=for-the-badge" />
<br><sub><b>8</b> mục</sub>
</td>
<td align="center" width="20%">
<img src="https://img.shields.io/badge/🔫_SÚNG-3_loại-a8e6cf?style=for-the-badge" />
<br><sub><b>3</b> mục</sub>
</td>
<td align="center" width="20%">
<img src="https://img.shields.io/badge/📦_TỔNG-28_loại-5865F2?style=for-the-badge" />
<br><sub><b>31</b> mục</sub>
</td>
</tr>
</table>

---

## 🍎 Trái (Fruits) — 5 loại

| # | Tên | Số lượng | Hiếm |
|:-:|-----|:--------:|:----:|
| 1 | 🐉 **Dragon Fruit** | ×1 | ⭐⭐⭐⭐⭐ |
| 2 | 🐆 **Leopard Fruit** | ×1 | ⭐⭐⭐⭐⭐ |
| 3 | 🦊 **Kitsune Fruit** | ×1 | ⭐⭐⭐⭐⭐ |
| 4 | 💨 **Dough Fruit** | ×2 | ⭐⭐⭐⭐ |
| 5 | ☀️ **Light Fruit** | ×1 | ⭐⭐⭐ |

---

## ⚔️ Kiếm (Swords) — 12 loại

| # | Tên | Số lượng | Yêu cầu |
|:-:|-----|:--------:|---------|
| 1 | 🗡️ **Cursed Dual Katana** | ×1 | Godhuman + 3000 Ectoplasm |
| 2 | 🗡️ **Yama** | ×1 | Level 2200+ |
| 3 | 🗡️ **Tushita** | ×1 | Level 2000+ |
| 4 | 🗡️ **True Triple Katana** | ×1 | 3 × Legendary Sword |
| 5 | 🌸 **Hallow Scythe** | ×1 | Halloween Event |
| 6 | 🔮 **Dark Blade** | ×1 | Gamepass / Trade |
| 7 | 🌊 **Shark Saw** | ×1 | Level 1000+ |
| 8 | 🍃 **Koko** | ×1 | Level 400+ |
| 9 | 💧 **Longsword** | ×1 | Level 400+ |
| 10 | ⚡ **Rengoku** | ×1 | Level 1000+ |
| 11 | 🔪 **Dual Katana** | ×1 | Level 300+ |
| 12 | 🗡️ **Katana** | ×1 | Starter |

---

## 🥋 Võ thuật (Fighting Styles) — 8 loại

| # | Tên | Số lượng | Yêu cầu |
|:-:|-----|:--------:|---------|
| 1 | 👊 **Godhuman** | ×1 | 5000 fragments + 20 mastery mỗi style |
| 2 | 🩸 **Sanguine Art** | ×1 | Level 2400+ |
| 3 | 🦈 **Sharkman Karate** | ×1 | 2500 fragments |
| 4 | ⚡ **Electric Claw** | ×1 | 5000 fragments |
| 5 | 🐉 **Dragon Talon** | ×1 | 3000 fragments |
| 6 | 🐟 **Fishman Karate** | ×1 | 750 fragments |
| 7 | 💀 **Death Step** | ×1 | 2500 fragments |
| 8 | 💪 **Superhuman** | ×1 | 3000 fragments |

---

## 🔫 Súng (Guns) — 3 loại

| # | Tên | Số lượng | Nguồn |
|:-:|-----|:--------:|-------|
| 1 | 🎯 **Cursed Dual Pistols** | ×1 | Cursed Ship |
| 2 | 🔫 **Kabucha** | ×1 | Weapon Dealer |
| 3 | 🔫 **Flintlock** | ×1 | Starter |

---

## 📈 Thống kê phiên

| Thuộc tính | Giá trị |
|------------|---------|
| 🎮 **Tài khoản** | `[USERNAME]` |
| 🆔 **User ID** | `123456789` |
| 🔑 **Session ID** | `123456` |
| 🌐 **Server** | `JobId: abc-xyz-123` |
| 🗺️ **Sea** | Third Sea |
| ⏰ **Bắt đầu** | `2024-11-05 14:00:00` |
| 🕐 **Kết thúc** | `2024-11-05 14:30:00` |
| ⏱️ **Thời lượng** | **30 phút** |

---

<div align="center">

### 🔗 Links

[🌐 Xem Dashboard](https://your-app.up.railway.app/u/USERNAME) · 
[📊 API Data](https://your-app.up.railway.app/api/get-inventory/USERNAME) · 
[🏠 Trang chủ](https://github.com/YOUR_USERNAME/bloxfruit-monitor)

<sub>🤖 Generated automatically by <b>Blox Fruit Monitor v6.0</b></sub>

</div>
// Tự động tạo README.md cho từng tài khoản từ database.json
const fs = require('fs');
const path = require('path');

const DB_FILE   = path.join(__dirname, '..', 'database.json');
const OUTPUT_DIR = path.join(__dirname, '..', 'docs');

if (!fs.existsSync(OUTPUT_DIR)) fs.mkdirSync(OUTPUT_DIR, { recursive: true });

const db = JSON.parse(fs.readFileSync(DB_FILE, 'utf8'));

const FRUITS = new Set(["Rocket","Spin","Chop","Spring","Bomb","Smoke","Spike","Flame","Falcon","Ice","Sand","Dark","Diamond","Light","Rubber","Barrier","Ghost","Magma","Door","Quake","Human","Buddha","Love","Spider","Sound","Phoenix","Portal","Rumble","Pain","Blizzard","Gravity","Mammoth","T-Rex","Dough","Shadow","Venom","Control","Spirit","Dragon","Leopard","Kitsune","Yeti","Gas"]);
const SWORDS = new Set(["Cutlass","Katana","Iron Mace","Dual Katana","Triple Katana","Wando","Saddi","Longsword","Shisui","Rengoku","Dark Blade","Buddy Sword","Hallow Scythe","Hollow Scythe","True Triple Katana","Cursed Dual Katana","Yama","Tushita","Koko","Trident","Shark Saw","Midnight Blade","Dragonheart","Soul Cane","Fox Lamp","Twin Hooks","Serpent Bow"]);
const STYLES = new Set(["Combat","Dark Step","Electric Claw","Fishman Karate","Dragon Talon","Superhuman","Death Step","Sharkman Karate","Godhuman","Sanguine Art"]);
const GUNS   = new Set(["Flintlock","Slingshot","Cannon","Musket","Cursed Dual Pistols","Kabucha","Bizarre Rifle","Dragonstorm"]);

function classify(name) {
    const n = name.toLowerCase();
    if (FRUITS.has(name) || n.includes("fruit")) return "Fruit";
    if (SWORDS.has(name) || /sword|katana|blade|scythe/.test(n)) return "Sword";
    if (STYLES.has(name)) return "FightingStyle";
    if (GUNS.has(name) || /gun|rifle|pistol/.test(n)) return "Gun";
    return "Other";
}

function fmtDate(ms) {
    return ms ? new Date(ms).toISOString().replace('T', ' ').slice(0, 19) : 'N/A';
}

for (const [username, record] of Object.entries(db)) {
    const groups = { Fruit: [], Sword: [], FightingStyle: [], Gun: [], Other: [] };
    let total = 0;
    for (const [name, count] of Object.entries(record.inventory || {})) {
        if (count > 0) {
            groups[classify(name)].push({ name, count });
            total += count;
        }
    }
    for (const g of Object.values(groups)) g.sort((a, b) => b.count - a.count);

    const durationMin = record.sessionStart && record.lastSeen
        ? Math.floor((record.lastSeen - record.sessionStart) / 60000)
        : 0;

    let md = `# 🍇 Blox Fruit Profile — ${username}\n\n`;
    md += `> Auto-generated at \`${new Date().toISOString()}\`\n\n`;
    md += `## 📊 Tổng quan\n\n`;
    md += `| 🍎 Trái | ⚔️ Kiếm | 🥋 Võ thuật | 🔫 Súng | 📦 Khác | 📊 Tổng |\n`;
    md += `|:-------:|:-------:|:-----------:|:-------:|:-------:|:-------:|\n`;
    md += `| ${groups.Fruit.length} loại | ${groups.Sword.length} loại | ${groups.FightingStyle.length} loại | ${groups.Gun.length} loại | ${groups.Other.length} loại | **${total}** mục |\n\n`;

    const sections = [
        { key: 'Fruit',         title: '🍎 Trái (Fruits)' },
        { key: 'Sword',         title: '⚔️ Kiếm (Swords)' },
        { key: 'FightingStyle', title: '🥋 Võ thuật (Styles)' },
        { key: 'Gun',           title: '🔫 Súng (Guns)' },
        { key: 'Other',         title: '📦 Khác' }
    ];

    for (const sec of sections) {
        const items = groups[sec.key];
        if (items.length === 0) continue;
        md += `## ${sec.title} — ${items.length} loại\n\n`;
        md += `| # | Tên | Số lượng |\n|:-:|-----|:--------:|\n`;
        items.forEach((item, i) => {
            md += `| ${i + 1} | **${item.name}** | ×${item.count} |\n`;
        });
        md += `\n`;
    }

    md += `---\n\n## 📈 Thông tin phiên\n\n`;
    md += `| Thuộc tính | Giá trị |\n|------------|---------|\n`;
    md += `| 🎮 Tài khoản | \`${username}\` |\n`;
    md += `| 🔑 Session ID | \`${record.sessionId || 'N/A'}\` |\n`;
    md += `| ⏰ Bắt đầu | \`${fmtDate(record.sessionStart)}\` |\n`;
    md += `| 🕐 Kết thúc | \`${fmtDate(record.lastSeen)}\` |\n`;
    md += `| ⏱️ Thời lượng | **${durationMin} phút** |\n\n`;
    md += `---\n\n<div align="center"><sub>🤖 Auto-generated by Blox Fruit Monitor v6.0</sub></div>\n`;

    const outFile = path.join(OUTPUT_DIR, `${username}.md`);
    fs.writeFileSync(outFile, md);
    console.log(`✅ Đã tạo: ${outFile}`);
}

console.log(`\n🎉 Xong! ${Object.keys(db).length} file README đã được tạo trong /docs`);
