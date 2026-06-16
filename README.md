<html lang="zh-CN"><head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>澳门六合彩 · 智慧数据台 · 马年旗舰版</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Noto+Serif+SC:wght@300;400;600;700&family=JetBrains+Mono:wght@400;600;700&display=swap" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/echarts@5.4.3/dist/echarts.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/hls.js@latest"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
<style>
:root {
    --bg: #07080f;
    --bg2: #0a0c18;
    --surface: rgba(12, 18, 40, 0.96);
    --surface2: rgba(18, 24, 52, 0.90);
    --border: rgba(196, 164, 36, 0.18);
    --border2: rgba(255, 255, 255, 0.07);
    --gold: #c8a724;
    --gold-l: #f0cc52;
    --gold-dim: rgba(200, 167, 36, 0.13);
    --cyan: #22d3ee;
    --red: #f87171;
    --red-dim: rgba(248, 113, 113, 0.10);
    --blue: #60a5fa;
    --blue-dim: rgba(96, 165, 250, 0.10);
    --green: #4ade80;
    --green-dim: rgba(74, 222, 128, 0.10);
    --purple: #c084fc;
    --purp-dim: rgba(192, 132, 252, 0.10);
    --text: #dde2f0;
    --text-muted: rgba(221, 226, 240, 0.45);
    --text-dim: rgba(221, 226, 240, 0.22);
    --radius: 18px;
    --radius-s: 10px;
    --shadow: 0 8px 32px rgba(0, 0, 0, 0.55), 0 2px 6px rgba(0, 0, 0, 0.30);
}
* { margin: 0; padding: 0; box-sizing: border-box; }
body {
    font-family: 'Noto Serif SC', 'Segoe UI', system-ui;
    background: var(--bg);
    color: var(--text);
    height: 100dvh;
    display: flex;
    flex-direction: column;
    overflow: hidden;
}
body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: radial-gradient(ellipse 60% 40% at 15% 10%, rgba(200, 167, 36, 0.05) 0%, transparent 60%),
        radial-gradient(ellipse 50% 50% at 85% 85%, rgba(34, 211, 238, 0.04) 0%, transparent 60%),
        url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='3' height='3'%3E%3Crect width='1' height='1' fill='rgba(255,255,255,0.012)'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
}
.app-wrapper {
    flex: 1;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    position: relative;
    z-index: 1;
}
.quick-bar {
    background: linear-gradient(180deg, rgba(7, 8, 14, 0.995), rgba(9, 11, 22, 0.98));
    border-bottom: 1px solid var(--border);
    padding: 0 16px;
    height: 36px;
    display: flex;
    align-items: center;
    gap: 10px;
    flex-shrink: 0;
    backdrop-filter: blur(16px);
    position: relative;
    z-index: 11;
}
.quick-bar::after {
    content: '';
    position: absolute;
    bottom: -1px;
    left: 5%;
    right: 5%;
    height: 1px;
    background: linear-gradient(90deg, transparent, rgba(200, 167, 36, 0.25), transparent);
    pointer-events: none;
}
.quick-bar .actions {
    margin-left: auto;
    display: flex;
    align-items: center;
    gap: 6px;
    flex-shrink: 0;
}
.top-bar {
    background: linear-gradient(180deg, rgba(7, 8, 14, 0.995), rgba(9, 11, 22, 0.98));
    border-bottom: 1px solid var(--border);
    padding: 0 16px;
    height: 52px;
    display: flex;
    align-items: center;
    gap: 10px;
    flex-shrink: 0;
    backdrop-filter: blur(16px);
    position: relative;
    z-index: 10;
}
.top-bar::after {
    content: '';
    position: absolute;
    bottom: -1px;
    left: 5%;
    right: 5%;
    height: 1px;
    background: linear-gradient(90deg, transparent, rgba(200, 167, 36, 0.25), transparent);
    pointer-events: none;
}
.logo {
    display: flex;
    align-items: center;
    gap: 7px;
    font-family: 'Noto Serif SC', serif;
    font-size: 0.78rem;
    font-weight: 700;
    color: var(--gold-l);
    white-space: nowrap;
    letter-spacing: 0.05em;
    flex-shrink: 0;
    padding-right: 4px;
}
.logo-icon {
    width: 26px;
    height: 26px;
    background: linear-gradient(135deg, var(--gold), var(--gold-l));
    border-radius: 7px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.8rem;
    box-shadow: 0 0 12px rgba(200, 167, 36, 0.35);
    flex-shrink: 0;
}
.vline {
    width: 1px;
    height: 22px;
    background: var(--border);
    flex-shrink: 0;
    opacity: 0.7;
}
/* 只显示最新期 */
.live-strip {
    display: flex;
    align-items: center;
    gap: 6px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    flex-shrink: 0;
    background: rgba(255, 255, 255, 0.015);
    border-radius: 20px;
    padding: 4px 12px;
    border: 1px solid rgba(255, 255, 255, 0.04);
}
.dot-pulse {
    width: 5px;
    height: 5px;
    border-radius: 50%;
    background: var(--green);
    box-shadow: 0 0 5px var(--green);
    animation: pulse 2s ease-in-out infinite;
}
@keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: .45; transform: scale(.75); }
}
.live-lbl {
    color: var(--text-muted);
    font-size: 0.66rem;
}
.live-exp {
    color: var(--gold-l);
    font-weight: 700;
    font-size: 0.73rem;
}
/* 最新开奖 / 手动入录区域 */
.sync-area {
    display: flex;
    align-items: center;
    gap: 8px;
    background: rgba(255, 255, 255, .03);
    border: 1px solid rgba(255, 255, 255, 0.09);
    border-radius: 24px;
    padding: 4px 12px;
    flex-shrink: 0;
}
.sync-area .sync-label {
    font-size: 0.65rem;
    color: var(--text-muted);
    white-space: nowrap;
}
.sync-area .sync-nums {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    font-weight: 700;
    color: var(--gold-l);
    max-width: 180px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
}
.sync-area .sync-special {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.7rem;
    font-weight: 700;
    color: var(--cyan);
}
.btn-sync-live {
    background: var(--gold-dim);
    border: 1px solid rgba(200, 167, 36, .25);
    color: var(--gold-l);
    padding: 4px 10px;
    border-radius: 20px;
    font-size: 0.68rem;
    font-weight: 700;
    cursor: pointer;
    transition: all .12s;
    line-height: 1;
}
.btn-sync-live:hover {
    background: rgba(200, 167, 36, .22);
    box-shadow: 0 0 14px rgba(200, 167, 36, .18);
}
.actions {
    margin-left: auto;
    display: flex;
    align-items: center;
    gap: 6px;
    flex-shrink: 0;
}
.btn {
    background: var(--gold-dim);
    border: 1px solid rgba(200, 167, 36, .25);
    color: var(--gold-l);
    padding: 4px 10px;
    border-radius: 20px;
    font-size: 0.68rem;
    font-weight: 700;
    cursor: pointer;
    font-family: 'Noto Serif SC', serif;
    transition: all .12s;
    white-space: nowrap;
    letter-spacing: .02em;
    line-height: 1;
}
.btn:hover {
    background: rgba(200, 167, 36, .22);
    box-shadow: 0 0 14px rgba(200, 167, 36, .18);
}
.btn:active { transform: scale(.95); }
.btn-danger {
    background: var(--red-dim);
    border-color: rgba(248, 113, 113, .2);
    color: var(--red);
}
.btn-danger:hover {
    background: rgba(248, 113, 113, .18);
}
.fb {
    font-size: .6rem;
    color: var(--green);
    white-space: nowrap;
    min-width: 50px;
    text-align: center;
}
.manual-input {
    background: rgba(255,255,255,.03);
    border: 1px solid rgba(255,255,255,.09);
    color: var(--text);
    border-radius: 14px;
    padding: 4px 10px;
    font-size: .68rem;
    font-family: 'JetBrains Mono', monospace;
    outline: none;
}
.manual-input::placeholder { color: var(--text-dim); }
.manual-input:focus { border-color: rgba(200,167,36,.4); }
/* 复制按钮 */
.copy-btn {
    background: rgba(34,211,238,.08);
    border: 1px solid rgba(34,211,238,.22);
    color: var(--cyan);
    padding: 2px 9px;
    border-radius: 12px;
    font-size: .6rem;
    font-weight: 700;
    cursor: pointer;
    font-family: 'Noto Serif SC', serif;
    transition: all .12s;
    white-space: nowrap;
    line-height: 1.6;
    display: inline-flex;
    align-items: center;
    gap: 4px;
}
.copy-btn:hover { background: rgba(34,211,238,.2); box-shadow: 0 0 10px rgba(34,211,238,.15); }
.copy-btn:active { transform: scale(.94); }
.copy-btn.copied { color: var(--green); border-color: rgba(74,222,128,.3); background: rgba(74,222,128,.1); }
.title-with-copy {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 8px;
    flex-wrap: wrap;
}
.tab-nav {
    background: rgba(7, 8, 14, .97);
    border-bottom: 1px solid var(--border);
    display: flex;
    padding: 0 16px;
    gap: 1px;
    flex-shrink: 0;
    overflow-x: auto;
    scrollbar-width: none;
}
.tab-nav::-webkit-scrollbar { display: none; }
.tab-btn {
    background: none;
    border: none;
    border-bottom: 2px solid transparent;
    color: var(--text-muted);
    padding: 8px 12px;
    font-size: 0.71rem;
    font-family: 'Noto Serif SC', serif;
    font-weight: 600;
    cursor: pointer;
    white-space: nowrap;
    transition: all .12s;
    display: flex;
    align-items: center;
    gap: 4px;
}
.tab-btn:hover { color: var(--text); }
.tab-btn.active {
    color: var(--gold-l);
    border-bottom-color: var(--gold);
}
.main-scroll {
    flex: 1;
    overflow-y: auto;
    padding: 16px 18px;
    scroll-behavior: smooth;
}
.main-scroll::-webkit-scrollbar {
    width: 3px;
}
.main-scroll::-webkit-scrollbar-thumb {
    background: rgba(200, 167, 36, .2);
    border-radius: 2px;
}
.tab-panel { display: none; }
.tab-panel.active { display: block; }
.card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: var(--radius);
    margin-bottom: 12px;
    box-shadow: var(--shadow);
    overflow: hidden;
    backdrop-filter: blur(8px);
}
.card-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px 16px;
    background: rgba(255, 255, 255, .02);
    border-bottom: 1px solid var(--border2);
    cursor: pointer;
    font-weight: 700;
    font-size: 0.78rem;
    letter-spacing: .03em;
    transition: background .1s;
}
.card-header:hover { background: rgba(255, 255, 255, .04); }
.chevron {
    transition: transform .2s;
    color: var(--text-dim);
    font-size: .68rem;
}
.card.collapsed .chevron { transform: rotate(-90deg); }
.card.collapsed .card-body { display: none; }
.card-body { padding: 14px 16px; }
.card-gold {
    border-color: rgba(200, 167, 36, .22);
    background: linear-gradient(145deg, rgba(12, 18, 38, .98), rgba(18, 12, 4, .96));
}
.card-gold .card-header {
    background: linear-gradient(90deg, rgba(200, 167, 36, .07), transparent);
}
.stats-row {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
    margin-bottom: 12px;
}
.stat-card-large {
    min-height: 180px !important;
    padding: 14px 16px !important;
}
.stat-card-large .stat-lbl {
    font-size: .68rem !important;
    margin-bottom: 4px !important;
}
.stat-card-large .stat-val {
    font-size: .72rem !important;
    line-height: 1.6 !important;
    padding: 6px 0 !important;
}
.stat-card-large .stat-sub {
    font-size: .62rem !important;
    margin-top: 4px !important;
}
.stat-card-large .stat-feedback {
    font-size: .6rem !important;
    margin-top: 6px !important;
    padding-top: 6px !important;
}
.zone-dup-display {
    display: flex;
    flex-direction: column;
    gap: 6px;
    width: 100%;
    padding: 4px 0;
}
.zone-dup-row {
    display: flex;
    align-items: center;
    gap: 6px;
    flex-wrap: wrap;
    justify-content: center;
}
.zone-dup-label {
    font-size: .65rem;
    font-weight: 700;
    white-space: nowrap;
    flex-shrink: 0;
}
.zone-dup-nums {
    display: flex;
    flex-wrap: wrap;
    gap: 3px;
    justify-content: center;
}
.stat-card {
    background: var(--surface2);
    border: 1px solid var(--border2);
    border-radius: var(--radius-s);
    padding: 11px 12px;
    text-align: center;
    position: relative;
    overflow: hidden;
    min-height: 120px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
}
.stat-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 2px;
    border-radius: 2px 2px 0 0;
}
.sc-gold::before { background: linear-gradient(90deg, var(--gold), var(--gold-l)); }
.sc-cyan::before { background: linear-gradient(90deg, var(--cyan), #38bdf8); }
.sc-red::before { background: linear-gradient(90deg, var(--red), #fb923c); }
.sc-purple::before { background: linear-gradient(90deg, var(--purple), #818cf8); }
.stat-lbl {
    font-size: .6rem;
    color: var(--text-muted);
    margin-bottom: 2px;
    letter-spacing: .06em;
    text-transform: uppercase;
    font-family: 'Noto Serif SC', serif;
}
.stat-val {
    font-family: 'JetBrains Mono', monospace;
    font-size: 1.2rem;
    font-weight: 700;
    line-height: 1;
}
.stat-sub {
    font-size: .58rem;
    color: var(--text-muted);
    margin-top: 2px;
}
.stat-feedback {
    font-size: .58rem;
    margin-top: 5px;
    padding-top: 5px;
    border-top: 1px dashed var(--border2);
    line-height: 1.5;
    min-height: 1.4em;
}
.stat-feedback.fb-hit { color: var(--green); }
.stat-feedback.fb-miss { color: var(--red); }
.stat-feedback.fb-pending { color: var(--text-dim); }
.vg { color: var(--gold-l); }
.vc { color: var(--cyan); }
.vr { color: var(--red); }
.vp { color: var(--purple); }
.god-panel {
    background: linear-gradient(145deg, rgba(18, 12, 3, .98), rgba(10, 16, 32, .97));
    border: 1px solid rgba(200, 167, 36, .28);
    border-radius: var(--radius);
    padding: 18px 20px;
    margin-bottom: 12px;
    box-shadow: 0 0 40px rgba(200, 167, 36, .06), var(--shadow);
    position: relative;
    overflow: hidden;
}
.god-panel::after {
    content: '';
    position: absolute;
    top: -60%;
    right: -20%;
    width: 60%;
    height: 200%;
    background: radial-gradient(ellipse, rgba(200, 167, 36, .05) 0%, transparent 60%);
    pointer-events: none;
}
.god-title {
    font-family: 'Noto Serif SC', serif;
    font-size: .88rem;
    font-weight: 700;
    color: var(--gold-l);
    letter-spacing: .08em;
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    gap: 7px;
}
.god-nums {
    display: flex;
    gap: 12px;
    flex-wrap: wrap;
    margin-bottom: 12px;
    align-items: flex-end;
}
.god-ball-wrap { text-align: center; }
.god-ball {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 1.05rem;
    font-weight: 700;
    box-shadow: 0 6px 20px rgba(0, 0, 0, .55), inset 0 1px 0 rgba(255, 255, 255, .12);
    animation: ballIn .45s cubic-bezier(.17, .89, .38, 1.17) both;
    cursor: default;
    transition: transform .15s;
}
.god-ball:hover { transform: scale(1.1); }
@keyframes ballIn {
    from { transform: scale(.3) rotate(-200deg); opacity: 0; }
    to { transform: scale(1) rotate(0); opacity: 1; }
}
.gb-r { background: radial-gradient(circle at 38% 32%, #ff7070, #c02828); color: #fff; border: 1px solid rgba(255,100,100,.25); }
.gb-b { background: radial-gradient(circle at 38% 32%, #72b9ff, #2870b8); color: #fff; border: 1px solid rgba(100,160,255,.25); }
.gb-g { background: radial-gradient(circle at 38% 32%, #52efc0, #00a87a); color: #fff; border: 1px solid rgba(80,210,140,.25); }
.gb-gold { background: radial-gradient(circle at 38% 32%, #f0cc50, #c8a020); color: #2c1900; border: 1px solid rgba(200,167,36,.5); }
.ball-zod {
    font-size: .55rem;
    color: var(--text-muted);
    margin-top: 4px;
    font-family: 'Noto Serif SC', serif;
}
.god-basis {
    font-size: .7rem;
    color: rgba(221, 226, 240, .7);
    line-height: 1.7;
    padding: 9px 12px;
    background: rgba(255, 255, 255, .03);
    border-radius: var(--radius-s);
    border-left: 2px solid var(--gold);
}
.robot-card {
    background: linear-gradient(160deg, rgba(12, 20, 42, .98), rgba(16, 10, 30, .97));
    border: 1px solid rgba(34, 211, 238, 0.22);
    border-radius: var(--radius);
    margin-bottom: 12px;
    box-shadow: 0 0 35px rgba(34, 211, 238, 0.04), var(--shadow);
    overflow: hidden;
    position: relative;
}
.robot-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--cyan), var(--purple), var(--gold-l));
    border-radius: 2px 2px 0 0;
}
.robot-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 12px 18px;
    background: rgba(34, 211, 238, 0.04);
    border-bottom: 1px solid rgba(34, 211, 238, 0.1);
    cursor: pointer;
}
.robot-title {
    font-family: 'Noto Serif SC', serif;
    font-size: 0.84rem;
    font-weight: 700;
    color: var(--cyan);
    display: flex;
    align-items: center;
    gap: 8px;
    letter-spacing: .04em;
}
.robot-badge {
    font-size: 0.6rem;
    background: rgba(34, 211, 238, 0.12);
    color: var(--cyan);
    padding: 3px 10px;
    border-radius: 12px;
    font-family: 'JetBrains Mono', monospace;
    letter-spacing: 0;
}
.robot-body {
    padding: 16px 18px;
}
.robot-prediction-row {
    display: flex;
    align-items: center;
    gap: 16px;
    margin-bottom: 14px;
    flex-wrap: wrap;
}
.robot-main-pred {
    display: flex;
    align-items: center;
    gap: 10px;
    background: rgba(34, 211, 238, 0.06);
    border-radius: 14px;
    padding: 10px 16px;
    border: 1px solid rgba(34, 211, 238, 0.15);
}
.robot-big-ball {
    width: 56px;
    height: 56px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 1.3rem;
    font-weight: 700;
    box-shadow: 0 6px 24px rgba(0, 0, 0, .5), inset 0 1px 0 rgba(255, 255, 255, .15);
    animation: robotGlow 2s ease-in-out infinite;
}
@keyframes robotGlow {
    0%, 100% { box-shadow: 0 6px 24px rgba(0,0,0,.5), 0 0 16px rgba(34,211,238,0.25); }
    50% { box-shadow: 0 6px 24px rgba(0,0,0,.5), 0 0 28px rgba(34,211,238,0.5); }
}
.robot-pred-detail {
    display: flex;
    flex-direction: column;
    gap: 2px;
}
.robot-pred-label {
    font-size: 0.62rem;
    color: var(--text-muted);
    letter-spacing: .06em;
    text-transform: uppercase;
}
.robot-pred-info {
    font-size: 0.78rem;
    font-weight: 700;
    color: var(--text);
}
.robot-confidence {
    display: flex;
    align-items: center;
    gap: 8px;
    background: rgba(192, 132, 252, 0.06);
    border-radius: 12px;
    padding: 8px 14px;
    border: 1px solid rgba(192, 132, 252, 0.14);
}
.conf-bar-wrap {
    width: 60px;
    height: 5px;
    background: rgba(255, 255, 255, 0.06);
    border-radius: 3px;
    overflow: hidden;
}
.conf-bar-fill {
    height: 100%;
    border-radius: 3px;
    background: linear-gradient(90deg, var(--purple), var(--cyan));
    transition: width .6s;
}
.conf-text {
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.75rem;
    font-weight: 700;
    color: var(--purple);
}
.reasoning-chain {
    display: flex;
    flex-direction: column;
    gap: 6px;
}
.reason-step {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    padding: 8px 12px;
    background: rgba(255, 255, 255, 0.015);
    border-radius: 8px;
    border-left: 2px solid transparent;
    transition: all .15s;
}
.reason-step:hover { background: rgba(255, 255, 255, 0.03); }
.rs-step-num {
    width: 22px;
    height: 22px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 0.65rem;
    font-weight: 700;
    flex-shrink: 0;
    margin-top: 1px;
}
.rs-1 { background: rgba(248,113,113,0.18); color: var(--red); border: 1px solid rgba(248,113,113,0.2); }
.rs-2 { background: rgba(96,165,250,0.18); color: var(--blue); border: 1px solid rgba(96,165,250,0.2); }
.rs-3 { background: rgba(74,222,128,0.18); color: var(--green); border: 1px solid rgba(74,222,128,0.2); }
.rs-4 { background: rgba(192,132,252,0.18); color: var(--purple); border: 1px solid rgba(192,132,252,0.2); }
.rs-5 { background: rgba(200,167,36,0.18); color: var(--gold-l); border: 1px solid rgba(200,167,36,0.25); }
.rs-content {
    flex: 1;
    font-size: 0.7rem;
    line-height: 1.6;
    color: rgba(221, 226, 240, 0.78);
}
.rs-content strong { color: var(--text); }
.rs-tag {
    display: inline-block;
    padding: 1px 7px;
    border-radius: 10px;
    font-size: 0.6rem;
    font-weight: 700;
    margin: 0 2px;
    font-family: 'Noto Serif SC', serif;
}
.rs-tag-hot { background: var(--red-dim); color: var(--red); border: 1px solid rgba(248,113,113,0.2); }
.rs-tag-cold { background: var(--blue-dim); color: var(--blue); border: 1px solid rgba(96,165,250,0.2); }
.rs-tag-wave { background: var(--green-dim); color: var(--green); border: 1px solid rgba(74,222,128,0.2); }
.rs-tag-zod { background: var(--purp-dim); color: var(--purple); border: 1px solid rgba(192,132,252,0.2); }
.reason-conclusion {
    margin-top: 6px;
    padding: 10px 14px;
    background: rgba(200, 167, 36, 0.05);
    border-radius: 10px;
    border: 1px solid rgba(200, 167, 36, 0.12);
    font-size: 0.72rem;
    line-height: 1.7;
    color: rgba(221, 226, 240, 0.82);
}
.reason-conclusion .highlight { color: var(--gold-l); font-weight: 700; }
.insight-box {
    background: rgba(200, 167, 36, .05);
    border: 1px solid rgba(200, 167, 36, .12);
    border-left: 3px solid var(--gold);
    border-radius: var(--radius-s);
    padding: 9px 12px;
    margin-top: 8px;
    font-size: .72rem;
    line-height: 1.7;
    color: rgba(221, 226, 240, .82);
}
.insight-cyan {
    border-left-color: var(--cyan);
    background: rgba(34, 211, 238, .04);
    border-color: rgba(34, 211, 238, .1);
}
.insight-red {
    border-left-color: var(--red);
    background: var(--red-dim);
    border-color: rgba(248, 113, 113, .1);
}
.insight-purple {
    border-left-color: var(--purple);
    background: var(--purp-dim);
    border-color: rgba(192, 132, 252, .1);
}
.chart-box {
    height: 240px;
    width: 100%;
    margin-bottom: 2px;
}
.chart-tall { height: 280px; }
/* 开奖记录表格优化 */
.data-table {
    width: 100%;
    font-size: .68rem;
    border-collapse: collapse;
    font-family: 'JetBrains Mono', monospace;
    table-layout: fixed;
}
.data-table th {
    padding: 7px 9px;
    text-align: left;
    color: var(--text-muted);
    font-size: .6rem;
    letter-spacing: .07em;
    text-transform: uppercase;
    border-bottom: 1px solid var(--border2);
    background: rgba(255, 255, 255, .02);
    font-family: 'Noto Serif SC', serif;
}
.data-table td {
    padding: 6px 9px;
    border-bottom: 1px solid rgba(255, 255, 255, .04);
    vertical-align: middle;
    word-break: break-word;
}
.data-table th:nth-child(2), .data-table td:nth-child(2) {
    width: 35%;
}
.data-table tr:hover td { background: rgba(255, 255, 255, .02); }
.data-table tr:last-child td { border-bottom: none; }
.tbl-scroll {
    max-height: none;
    overflow: visible;
}
.tbl-scroll::-webkit-scrollbar { width: 3px; height: 3px; }
.tbl-scroll::-webkit-scrollbar-thumb { background: rgba(200, 167, 36, .18); border-radius: 2px; }
.num-ball {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 26px;
    height: 26px;
    border-radius: 50%;
    font-family: 'JetBrains Mono', monospace;
    font-size: .63rem;
    font-weight: 700;
    flex-shrink: 0;
}
.nb-r { background: rgba(248,113,113,.18); color: var(--red); border: 1px solid rgba(248,113,113,.22); }
.nb-b { background: rgba(96,165,250,.18); color: var(--blue); border: 1px solid rgba(96,165,250,.22); }
.nb-g { background: rgba(74,222,128,.18); color: var(--green); border: 1px solid rgba(74,222,128,.22); }
.wave-pill {
    display: inline-block;
    padding: 2px 9px;
    border-radius: 18px;
    font-size: .6rem;
    font-weight: 700;
    font-family: 'Noto Serif SC', serif;
}
.wp-r { background: var(--red-dim); color: var(--red); border: 1px solid rgba(248,113,113,.18); }
.wp-b { background: var(--blue-dim); color: var(--blue); border: 1px solid rgba(96,165,250,.18); }
.wp-g { background: var(--green-dim); color: var(--green); border: 1px solid rgba(74,222,128,.18); }
.zod-pill {
    display: inline-block;
    padding: 2px 9px;
    border-radius: 18px;
    font-size: .6rem;
    background: var(--purp-dim);
    color: var(--purple);
    border: 1px solid rgba(192,132,252,.18);
    font-family: 'Noto Serif SC', serif;
}
.wave-cols {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
}
.wave-col {
    background: var(--surface2);
    border: 1px solid var(--border2);
    border-radius: var(--radius-s);
    padding: 10px;
}
.wave-col-ttl {
    font-size: .74rem;
    font-weight: 700;
    margin-bottom: 6px;
    display: flex;
    align-items: center;
    gap: 5px;
}
.wave-nms {
    display: flex;
    flex-wrap: wrap;
    gap: 4px;
}
.zod-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 7px;
}
.zod-item {
    background: var(--surface2);
    border: 1px solid var(--border2);
    border-radius: var(--radius-s);
    padding: 8px;
    text-align: center;
}
.zod-name {
    font-size: .7rem;
    font-weight: 700;
    color: var(--purple);
    margin-bottom: 5px;
    font-family: 'Noto Serif SC', serif;
}
.zod-nms {
    display: flex;
    flex-wrap: wrap;
    gap: 3px;
    justify-content: center;
}
.grid-2 {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
}
.grid-4 {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 12px;
}
.note-row {
    display: flex;
    gap: 5px;
    margin-top: 6px;
    align-items: center;
}
.note-row input {
    flex: 1;
    background: rgba(255, 255, 255, .04);
    border: 1px solid var(--border2);
    border-radius: 18px;
    padding: 4px 10px;
    color: var(--text);
    font-size: .65rem;
    font-family: 'Noto Serif SC', serif;
    outline: none;
}
.note-row input::placeholder { color: var(--text-dim); }
.note-row input:focus { border-color: rgba(200, 167, 36, .28); }
.note-ok { font-size: .6rem; color: var(--green); }
.segment {
    border: 1px solid var(--border2);
    border-radius: var(--radius-s);
    margin-bottom: 8px;
    overflow: hidden;
}
.segment-hd {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 12px;
    background: rgba(255, 255, 255, .02);
    cursor: pointer;
    font-weight: 600;
    font-size: .72rem;
    transition: background .1s;
}
.segment-hd:hover { background: rgba(255, 255, 255, .04); }
.segment-body { padding: 12px; }
.segment.collapsed .segment-body { display: none; }
.seg-chev {
    transition: transform .2s;
    color: var(--text-dim);
    font-size: .62rem;
}
.segment.collapsed .seg-chev { transform: rotate(-90deg); }
.zone-summary-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
}
@media(max-width:1024px) {
    .top-bar { height: auto; flex-wrap: wrap; padding: 6px 10px; gap: 6px; min-height: 42px; }
    .stats-row { grid-template-columns: repeat(2, 1fr); }
    .stat-card-large { min-height: 160px !important; }
    .grid-2, .grid-4 { grid-template-columns: 1fr; }
    .wave-cols { grid-template-columns: 1fr; }
    .zod-grid { grid-template-columns: repeat(3, 1fr); }
}
@media(max-width:640px) {
    .top-bar { padding: 5px 8px; gap: 4px; min-height: 38px; }
    .logo { font-size: 0.68rem; gap: 4px; }
    .logo-icon { width: 20px; height: 20px; font-size: 0.6rem; }
    .stats-row { grid-template-columns: 1fr; }
    .stat-card-large { min-height: 140px !important; }
    .zod-grid { grid-template-columns: repeat(2, 1fr); }
    .main-scroll { padding: 10px; }
    .zone-summary-grid { grid-template-columns: 1fr; }
    .robot-prediction-row { flex-direction: column; align-items: stretch; gap: 8px; }
    .robot-main-pred { justify-content: center; }
    .robot-confidence { justify-content: center; }
    .god-nums { justify-content: center; gap: 8px; }
    .god-ball { width: 40px; height: 40px; font-size: 0.85rem; }
}
* {
    scrollbar-width: thin;
    scrollbar-color: rgba(200, 167, 36, .18) transparent;
}
.zone-quantum {
    margin-top: 10px;
    background: linear-gradient(135deg, rgba(10,18,42,.96), rgba(16,10,30,.95));
    border: 1px solid rgba(200,167,36,.18);
    border-radius: 12px;
    padding: 10px 14px;
    position: relative;
    overflow: hidden;
}
.zone-quantum::before {
    content:'';position:absolute;top:0;left:0;right:0;height:2px;
    background:linear-gradient(90deg,var(--gold),var(--cyan),var(--purple));
    border-radius:2px 2px 0 0;
}
.zq-title {
    font-size:.68rem;font-weight:700;color:var(--gold-l);
    letter-spacing:.06em;margin-bottom:8px;
    font-family:'Noto Serif SC',serif;
}
.zq-balls {
    display:flex;gap:8px;flex-wrap:wrap;margin-bottom:6px;align-items:flex-end;
}
.zq-ball-wrap { text-align:center; }
.zq-ball {
    width:36px;height:36px;border-radius:50%;
    display:flex;align-items:center;justify-content:center;
    font-family:'JetBrains Mono',monospace;
    font-size:.78rem;font-weight:700;
    box-shadow:0 4px 12px rgba(0,0,0,.5),inset 0 1px 0 rgba(255,255,255,.12);
    animation:ballIn .4s cubic-bezier(.17,.89,.38,1.17) both;
    transition:transform .15s;cursor:default;
}
.zq-ball:hover{transform:scale(1.12);}
.zq-ball-lbl{font-size:.5rem;color:var(--text-muted);margin-top:3px;font-family:'Noto Serif SC',serif;}
.zq-basis{font-size:.62rem;color:var(--text-muted);line-height:1.5;}
.pi-hero {
    background:linear-gradient(135deg,rgba(8,6,20,.98),rgba(12,18,40,.97));
    border:1px solid rgba(192,132,252,.22);
    border-radius:var(--radius);
    padding:20px 22px;
    margin-bottom:12px;
    display:flex;align-items:center;gap:20px;
    position:relative;overflow:hidden;
    box-shadow:0 0 50px rgba(192,132,252,.04),var(--shadow);
}
.pi-symbol-bg {
    position:absolute;right:16px;top:50%;transform:translateY(-50%);
    font-size:8rem;font-weight:900;
    color:rgba(192,132,252,.06);
    font-family:Georgia,serif;
    pointer-events:none;
    letter-spacing:-0.05em;
}
.pi-hero-content { flex:1; }
.pi-hero-title {
    font-family:'Noto Serif SC',serif;font-size:.95rem;font-weight:700;
    color:var(--purple);letter-spacing:.08em;margin-bottom:4px;
}
.pi-hero-sub { font-size:.68rem;color:var(--text-muted);letter-spacing:.06em; }
.pi-hero-date {
    font-family:'JetBrains Mono',monospace;font-size:.7rem;
    color:rgba(221,226,240,.5);margin-top:6px;
}
.pi-today-seed {
    background:rgba(192,132,252,.08);border:1px solid rgba(192,132,252,.18);
    border-radius:12px;padding:12px 16px;text-align:center;flex-shrink:0;
}
.pi-seed-label { font-size:.6rem;color:var(--text-muted);letter-spacing:.06em;margin-bottom:4px;font-family:'Noto Serif SC',serif; }
.pi-seed-val {
    font-family:'JetBrains Mono',monospace;font-size:1.6rem;font-weight:700;
    color:var(--purple);line-height:1;
}
.pi-seed-sub { font-size:.62rem;color:var(--text-muted);margin-top:3px;font-family:'JetBrains Mono',monospace; }
.pi-eq {
    font-family:'JetBrains Mono',monospace;font-size:.8rem;
    color:rgba(221,226,240,.7);word-break:break-all;line-height:1.9;
}
.pi-digit {
    display:inline-flex;align-items:center;justify-content:center;
    width:24px;height:24px;border-radius:6px;
    font-size:.72rem;font-weight:700;margin:2px;
    transition:all .2s;cursor:default;
}
.pi-digit:hover { transform:scale(1.2); }
.pi-d-r { background:rgba(248,113,113,.15);color:var(--red);border:1px solid rgba(248,113,113,.2); }
.pi-d-b { background:rgba(96,165,250,.15);color:var(--blue);border:1px solid rgba(96,165,250,.2); }
.pi-d-g { background:rgba(74,222,128,.15);color:var(--green);border:1px solid rgba(74,222,128,.2); }
.pi-d-active {
    background:rgba(200,167,36,.25)!important;
    color:var(--gold-l)!important;
    border-color:rgba(200,167,36,.4)!important;
    box-shadow:0 0 8px rgba(200,167,36,.3);
    transform:scale(1.1);
}
.pi-energy-panel {
    background:linear-gradient(145deg,rgba(12,6,24,.98),rgba(8,16,38,.97));
    border:1px solid rgba(192,132,252,.2);
    border-radius:var(--radius);
    padding:18px 20px;
    margin-bottom:12px;
    box-shadow:0 0 40px rgba(192,132,252,.04),var(--shadow);
    position:relative;overflow:hidden;
}
.pi-energy-panel::before {
    content:'';position:absolute;top:0;left:0;right:0;height:2px;
    background:linear-gradient(90deg,var(--purple),var(--cyan),var(--gold-l));
}
.pi-e-title {
    font-family:'Noto Serif SC',serif;font-size:.88rem;font-weight:700;
    color:var(--purple);letter-spacing:.08em;margin-bottom:14px;
}
.pi-e-nums { display:flex;gap:14px;flex-wrap:wrap;margin-bottom:12px;align-items:flex-end; }
.pi-e-ball-wrap { text-align:center; }
.pi-e-ball {
    width:50px;height:50px;border-radius:50%;
    display:flex;align-items:center;justify-content:center;
    font-family:'JetBrains Mono',monospace;font-size:1.05rem;font-weight:700;
    box-shadow:0 6px 20px rgba(0,0,0,.5),inset 0 1px 0 rgba(255,255,255,.12);
    animation:ballIn .45s cubic-bezier(.17,.89,.38,1.17) both;
    transition:transform .15s;cursor:default;
}
.pi-e-ball:hover { transform:scale(1.1); }
.pi-e-ball-lbl { font-size:.56rem;color:var(--text-muted);margin-top:4px;font-family:'Noto Serif SC',serif; }
.pi-e-calc {
    background:rgba(255,255,255,.025);border:1px solid rgba(192,132,252,.1);
    border-left:3px solid var(--purple);
    border-radius:8px;padding:10px 14px;
    font-size:.7rem;line-height:1.75;color:rgba(221,226,240,.75);
    font-family:'Noto Serif SC',serif;
}
.pi-disclaimer {
    font-size:.62rem;color:var(--text-dim);line-height:1.6;
    text-align:center;padding:10px 0 4px;border-top:1px solid var(--border2);
    margin-top:4px;
}
.robot-hub-banner {
    background:linear-gradient(135deg,rgba(10,18,44,.98),rgba(14,8,32,.97));
    border:1px solid rgba(34,211,238,.2);
    border-radius:var(--radius);
    padding:16px 20px;
    margin-bottom:12px;
    display:flex;align-items:center;justify-content:space-between;gap:16px;
    box-shadow:0 0 40px rgba(34,211,238,.04),var(--shadow);
    position:relative;overflow:hidden;
}
.robot-hub-banner::before {
    content:'';position:absolute;top:0;left:0;right:0;height:2px;
    background:linear-gradient(90deg,var(--cyan),var(--purple),var(--gold-l));
}
.rhb-left { display:flex;align-items:center;gap:14px; }
.rhb-icon { font-size:2rem;line-height:1; }
.rhb-title {
    font-family:'Noto Serif SC',serif;font-size:.88rem;font-weight:700;
    color:var(--cyan);letter-spacing:.04em;margin-bottom:3px;
}
.rhb-sub { font-size:.66rem;color:var(--text-muted); }
.rhb-status {
    display:flex;align-items:center;gap:8px;
    font-family:'JetBrains Mono',monospace;font-size:.68rem;
    color:var(--green);background:rgba(74,222,128,.08);
    border:1px solid rgba(74,222,128,.15);
    border-radius:20px;padding:5px 12px;
    flex-shrink:0;
}
.sim-models-grid {
    display:grid;grid-template-columns:repeat(5,1fr);gap:10px;
    margin-bottom:14px;
}
.sim-model {
    background:rgba(255,255,255,.03);
    border:1px solid rgba(255,255,255,.07);
    border-radius:10px;padding:10px;
    transition:border-color .2s;
}
.sim-model.active { border-color:rgba(34,211,238,.3); }
.sim-model.done { border-color:rgba(74,222,128,.25); }
.sm-header {
    display:flex;align-items:center;gap:5px;
    font-size:.66rem;color:var(--text-muted);margin-bottom:8px;
    font-family:'Noto Serif SC',serif;
}
.sm-icon { font-size:.85rem; }
.sm-state {
    margin-left:auto;font-family:'JetBrains Mono',monospace;
    font-size:.58rem;color:var(--text-dim);
    background:rgba(255,255,255,.04);
    padding:1px 6px;border-radius:8px;
}
.sm-state.running { color:var(--cyan);background:rgba(34,211,238,.1); }
.sm-state.done { color:var(--green);background:rgba(74,222,128,.1); }
.sm-result {
    font-family:'JetBrains Mono',monospace;font-size:1rem;font-weight:700;
    color:var(--gold-l);text-align:center;margin-bottom:6px;min-height:22px;
}
.sm-bar { height:3px;background:rgba(255,255,255,.06);border-radius:2px;overflow:hidden; }
.sm-fill {
    height:100%;border-radius:2px;
    background:linear-gradient(90deg,var(--cyan),var(--purple));
    transition:width .8s ease;
}
.btn-robot-run {
    display:block;width:100%;
    background:linear-gradient(135deg,rgba(34,211,238,.12),rgba(192,132,252,.1));
    border:1px solid rgba(34,211,238,.25);
    color:var(--cyan);
    padding:10px 20px;border-radius:10px;
    font-size:.76rem;font-weight:700;
    cursor:pointer;font-family:'Noto Serif SC',serif;
    letter-spacing:.04em;transition:all .15s;
    text-align:center;
}
.btn-robot-run:hover { background:linear-gradient(135deg,rgba(34,211,238,.2),rgba(192,132,252,.18));box-shadow:0 0 20px rgba(34,211,238,.12); }
.btn-robot-run:disabled { opacity:.35;cursor:not-allowed; }
.robot-consensus {
    background:linear-gradient(145deg,rgba(14,20,44,.98),rgba(10,8,24,.97));
    border:1px solid rgba(200,167,36,.25);
    border-radius:var(--radius);
    padding:18px 20px;margin-bottom:12px;
    box-shadow:0 0 40px rgba(200,167,36,.06),var(--shadow);
}
.rc-title {
    font-family:'Noto Serif SC',serif;font-size:.88rem;font-weight:700;
    color:var(--gold-l);letter-spacing:.08em;margin-bottom:14px;
}
.rc-nums { display:flex;gap:12px;flex-wrap:wrap;margin-bottom:12px;align-items:flex-end; }
.rc-reasoning {
    background:rgba(255,255,255,.025);border:1px solid rgba(200,167,36,.1);
    border-left:3px solid var(--gold);
    border-radius:8px;padding:10px 14px;
    font-size:.72rem;line-height:1.75;color:rgba(221,226,240,.8);
    margin-bottom:8px;font-family:'Noto Serif SC',serif;
}
.rc-disclaimer {
    font-size:.62rem;color:var(--text-dim);line-height:1.5;
    padding-top:8px;border-top:1px solid var(--border2);
}
@media(max-width:900px) {
    .sim-models-grid { grid-template-columns:repeat(3,1fr); }
    .pi-hero { flex-direction:column; }
    .pi-today-seed { width:100%; }
}
@media(max-width:640px) {
    .sim-models-grid { grid-template-columns:repeat(2,1fr); }
}
/* 区间数字整合卡片样式 */
.zone-int-cards {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
    margin-bottom: 12px;
}
.zone-int-card {
    background: var(--surface2);
    border: 1px solid var(--border2);
    border-radius: var(--radius-s);
    padding: 12px;
    transition: all .2s;
}
.zone-int-card:hover {
    border-color: rgba(200,167,36,.3);
    background: rgba(18,24,52,.95);
}
.zone-int-title {
    font-size: .78rem;
    font-weight: 700;
    margin-bottom: 10px;
    padding-bottom: 4px;
    border-bottom: 1px solid var(--border2);
    display: flex;
    align-items: center;
    gap: 6px;
}
.zone-stats-row {
    display: flex;
    justify-content: space-between;
    margin-bottom: 8px;
    font-size: .68rem;
    color: var(--text-muted);
}
.zone-stats-row span:first-child { color: var(--text); font-weight: 600; }
.zone-number-list {
    margin-top: 8px;
    background: rgba(200,167,36,.05);
    border-radius: 10px;
    padding: 8px;
    border-left: 2px solid var(--gold);
}
.zone-number-list .list-label {
    font-size: .62rem;
    font-weight: 700;
    color: var(--gold-l);
    margin-bottom: 6px;
}
.zone-number-group {
    margin-bottom: 10px;
}
.zone-number-group .group-name {
    font-size: .6rem;
    color: var(--text-muted);
    margin-bottom: 4px;
    display: inline-block;
    background: rgba(255,255,255,.04);
    padding: 1px 6px;
    border-radius: 10px;
}
.zone-number-group .group-nums {
    display: flex;
    flex-wrap: wrap;
    gap: 4px;
    margin-top: 4px;
}
.zone-number-group .group-nums .num-mini {
    background: rgba(255,255,255,.05);
    padding: 2px 5px;
    border-radius: 12px;
    font-size: .6rem;
    font-family: 'JetBrains Mono', monospace;
    color: var(--text);
}
/* 底部统一展示区域 */
.unified-recommend-section {
    margin-top: 20px;
    background: linear-gradient(145deg, rgba(12, 6, 24, .98), rgba(8, 16, 38, .97));
    border: 1px solid rgba(200, 167, 36, .25);
    border-radius: var(--radius);
    padding: 16px;
}
.unified-title {
    font-size: .85rem;
    font-weight: 700;
    color: var(--gold-l);
    margin-bottom: 12px;
    padding-bottom: 6px;
    border-bottom: 1px solid var(--border);
}
.unified-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 12px;
}
.unified-card {
    background: var(--surface2);
    border: 1px solid var(--border2);
    border-radius: var(--radius-s);
    padding: 10px;
}
.unified-card-title {
    font-size: .7rem;
    font-weight: 700;
    color: var(--cyan);
    margin-bottom: 8px;
    display: flex;
    align-items: center;
    gap: 6px;
}
.unified-nums {
    display: flex;
    flex-wrap: wrap;
    gap: 4px;
}
.unified-nums .num-mini {
    background: rgba(255,255,255,.05);
    padding: 2px 5px;
    border-radius: 12px;
    font-size: .6rem;
    font-family: 'JetBrains Mono', monospace;
    color: var(--text);
}
/* 视频播放器 */
.video-container {
    background: #000;
    border-radius: var(--radius-s);
    overflow: hidden;
    margin-bottom: 12px;
}
.video-container video {
    width: 100%;
    max-height: 300px;
    background: #000;
}

/* 三中三栏兀预测样式 */
.szs-panel {
    background: linear-gradient(145deg, rgba(12, 6, 24, .98), rgba(8, 16, 38, .97));
    border: 1px solid rgba(200, 167, 36, .25);
    border-radius: var(--radius);
    padding: 18px 20px;
    margin-bottom: 12px;
    position: relative;
    overflow: hidden;
}
.szs-panel::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--gold), var(--cyan), var(--purple));
    border-radius: 2px 2px 0 0;
}
.szs-title {
    font-family: 'Noto Serif SC', serif;
    font-size: .9rem; font-weight: 700;
    color: var(--gold-l); letter-spacing: .06em;
    margin-bottom: 14px;
    display: flex; align-items: center; gap: 8px;
}
.szs-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 12px;
    margin-bottom: 14px;
}
.szs-card {
    background: var(--surface2);
    border: 1px solid var(--border2);
    border-radius: var(--radius-s);
    padding: 12px;
    text-align: center;
}
.szs-card-title {
    font-size: .7rem; font-weight: 700;
    color: var(--cyan);
    margin-bottom: 10px;
    font-family: 'Noto Serif SC', serif;
    letter-spacing: .04em;
}
.szs-numbers {
    display: flex; flex-wrap: wrap;
    gap: 6px; justify-content: center;
}
.szs-number {
    display: inline-flex; align-items: center; justify-content: center;
    width: 34px; height: 34px;
    border-radius: 50%;
    font-family: 'JetBrains Mono', monospace;
    font-size: .8rem; font-weight: 700;
    color: #fff;
    box-shadow: 0 3px 10px rgba(0,0,0,.4);
}
.szs-reason {
    background: rgba(255,255,255,.025);
    border: 1px solid rgba(200,167,36,.1);
    border-left: 3px solid var(--gold);
    border-radius: 8px; padding: 10px 14px;
    font-size: .7rem; line-height: 1.75;
    color: rgba(221,226,240,.8);
    font-family: 'Noto Serif SC', serif;
    margin-bottom: 12px;
}
/* 三中三分析方法表格 */
.szs-analysis-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 10px;
    margin-top: 12px;
}
.szs-method-card {
    background: rgba(255,255,255,.02);
    border: 1px solid rgba(200,167,36,.12);
    border-radius: var(--radius-s);
    padding: 10px;
}
.szs-method-title {
    font-size: .68rem; font-weight: 700;
    color: var(--gold-l); margin-bottom: 6px;
    font-family: 'Noto Serif SC', serif;
}
.szs-method-body {
    font-size: .63rem; line-height: 1.65;
    color: rgba(221,226,240,.72);
}
.szs-stats-row {
    display: grid; grid-template-columns: repeat(4, 1fr);
    gap: 8px; margin-top: 12px;
}
.szs-stat {
    background: rgba(34,211,238,.06);
    border: 1px solid rgba(34,211,238,.12);
    border-radius: 8px; padding: 8px;
    text-align: center;
}
.szs-stat-val {
    font-family: 'JetBrains Mono', monospace;
    font-size: .9rem; font-weight: 700;
    color: var(--cyan);
}
.szs-stat-lbl { font-size: .58rem; color: var(--text-muted); margin-top: 2px; }
@media(max-width:640px) {
    .szs-grid { grid-template-columns: 1fr; }
    .szs-analysis-grid { grid-template-columns: 1fr; }
    .szs-stats-row { grid-template-columns: repeat(2, 1fr); }
}
/* 区间整合底部重码分析 */
.zone-dup-section {
    margin-top: 14px;
    background: linear-gradient(145deg, rgba(10,20,40,.98), rgba(14,8,28,.97));
    border: 1px solid rgba(34,211,238,.2);
    border-radius: var(--radius);
    padding: 14px 16px;
}
.zone-dup-title {
    font-size: .82rem; font-weight: 700;
    color: var(--cyan); margin-bottom: 10px;
    font-family: 'Noto Serif SC', serif;
    letter-spacing: .05em;
}
.zone-dup-grid {
    display: grid; grid-template-columns: repeat(2, 1fr);
    gap: 10px;
}
.zone-dup-card {
    background: rgba(255,255,255,.025);
    border: 1px solid rgba(255,255,255,.07);
    border-radius: var(--radius-s); padding: 10px;
}
.zone-dup-card-title {
    font-size: .68rem; font-weight: 700;
    color: var(--text-muted); margin-bottom: 8px;
}
.zone-dup-nums { display: flex; flex-wrap: wrap; gap: 4px; }
.num-dup { background: rgba(248,113,113,.2); color: var(--red); border: 1px solid rgba(248,113,113,.25); }
.num-unique { background: rgba(74,222,128,.12); color: var(--green); border: 1px solid rgba(74,222,128,.2); }
.zone-manual-select { margin-top: 10px; padding-top: 8px; border-top: 1px dashed var(--border2); }
.zone-tier-select { background: var(--surface); border: 1px solid var(--border2); border-radius: 6px; color: var(--text); font-size: .62rem; padding: 3px 6px; cursor: pointer; transition: all .15s; }
.zone-tier-select:hover { border-color: rgba(200,167,36,.4); }
.zone-tier-select:focus { border-color: rgba(200,167,36,.5); outline: none; }
.zone-manual-badge { font-size: .55rem; padding: 1px 6px; border-radius: 8px; background: rgba(200,167,36,.15); color: var(--gold-l); border: 1px solid rgba(200,167,36,.3); }
.zone-auto-badge { font-size: .55rem; padding: 1px 6px; border-radius: 8px; background: rgba(34,211,238,.12); color: var(--cyan); border: 1px solid rgba(34,211,238,.2); }

/* ===== MODAL ===== */
.modal-overlay {
    position: fixed; inset: 0; background: rgba(4,5,12,.72);
    backdrop-filter: blur(4px); display: none; align-items: center; justify-content: center;
    z-index: 999; padding: 20px;
}
.modal-overlay.active { display: flex; }
.modal-box {
    background: var(--surface); border: 1px solid var(--border);
    border-radius: var(--radius); box-shadow: var(--shadow);
    max-width: 600px; width: 100%; max-height: 86vh; overflow-y: auto;
    padding: 20px 22px;
}
.modal-title { font-size: .92rem; font-weight: 700; color: var(--gold-l); margin-bottom: 14px; display:flex; align-items:center; justify-content:space-between; }
.modal-close { cursor:pointer; color: var(--text-muted); font-size: 1rem; }
.modal-close:hover { color: var(--text); }
.modal-section { margin-bottom: 16px; padding-bottom: 14px; border-bottom: 1px solid var(--border2); }
.modal-section:last-child { border-bottom: none; margin-bottom: 0; padding-bottom: 0; }
.modal-section-title { font-size: .76rem; font-weight: 700; color: var(--cyan); margin-bottom: 10px; }
.modal-row { display:flex; align-items:center; justify-content:space-between; gap:10px; margin-bottom:8px; font-size:.7rem; color:var(--text); flex-wrap: wrap; }
.modal-desc { color: var(--text-muted); font-size:.64rem; margin-top:6px; line-height: 1.7; }
.modal-actions { display:flex; gap:8px; justify-content:flex-end; margin-top:14px; flex-wrap: wrap; }
.weight-bar-row { display:flex; align-items:center; gap:8px; margin-bottom:7px; font-size:.62rem; }
.weight-bar-row .wlabel { width: 68px; color: var(--text-muted); flex-shrink:0; }
.weight-bar-row .wval { width: 44px; text-align:right; color: var(--text); flex-shrink:0; font-family:'JetBrains Mono',monospace; }
.weight-bar-track { flex:1; height:6px; border-radius:4px; background: rgba(255,255,255,.06); overflow:hidden; }
.weight-bar-fill { height:100%; background: linear-gradient(90deg, var(--gold), var(--cyan)); border-radius:4px; }
/* toggle switch */
.switch { position:relative; display:inline-block; width:34px; height:18px; flex-shrink:0; }
.switch input { opacity:0; width:0; height:0; }
.switch .slider { position:absolute; cursor:pointer; inset:0; background: rgba(255,255,255,.12); border-radius:18px; transition:.2s; }
.switch .slider:before { content:''; position:absolute; width:14px; height:14px; left:2px; bottom:2px; background:#fff; border-radius:50%; transition:.2s; }
.switch input:checked + .slider { background: var(--gold); }
.switch input:checked + .slider:before { transform: translateX(16px); }
/* toast */
.toast {
    position: fixed; bottom: 24px; left: 50%; transform: translateX(-50%) translateY(20px);
    background: var(--surface2); border: 1px solid var(--border); color: var(--text);
    padding: 10px 20px; border-radius: 30px; font-size: .72rem; box-shadow: var(--shadow);
    opacity: 0; pointer-events: none; transition: all .25s; z-index: 1100; max-width: 90vw; text-align:center;
}
.toast.show { opacity: 1; transform: translateX(-50%) translateY(0); }
/* ===== PROBABILITY HEATMAP ===== */
.prob-legend { display:flex; flex-wrap:wrap; gap:10px; margin-bottom:12px; font-size:.6rem; color:var(--text-muted); align-items:center; }
.prob-legend .lg-dot { display:inline-block; width:11px; height:11px; border-radius:3px; margin-right:4px; vertical-align:middle; }
.prob-grid { display:grid; grid-template-columns: repeat(7, 1fr); gap: 6px; }
.prob-cell {
    border-radius: var(--radius-s); padding: 7px 2px; text-align:center;
    border: 1px solid var(--border2); transition: transform .12s;
}
.prob-cell:hover { transform: scale(1.07); z-index:2; }
.prob-cell .pc-num { font-family:'JetBrains Mono',monospace; font-weight:700; font-size:.8rem; }
.prob-cell .pc-pct { font-size:.58rem; margin-top:3px; opacity:.85; font-family:'JetBrains Mono',monospace; }
.prob-tier-1 { background: rgba(200,167,36,.30); border-color: rgba(200,167,36,.5); color: var(--gold-l); box-shadow: 0 0 10px rgba(200,167,36,.18); }
.prob-tier-2 { background: rgba(34,211,238,.18); border-color: rgba(34,211,238,.35); color: var(--cyan); }
.prob-tier-3 { background: rgba(192,132,252,.13); border-color: rgba(192,132,252,.28); color: var(--purple); }
.prob-tier-4 { background: rgba(255,255,255,.03); border-color: var(--border2); color: var(--text-muted); }
.prob-tier-5 { background: rgba(248,113,113,.05); border-color: rgba(248,113,113,.12); color: var(--text-dim); }

</style>
</head>
<body>
<div class="app-wrapper">

    <!-- TOP BAR -->
    <div class="top-bar">
        <div class="logo">
            <div class="logo-icon">🏆</div>
            <span>澳门六合彩·智慧数据台</span>
        </div>
        <div class="vline"></div>
        <div class="live-strip">
            <div class="dot-pulse"></div>
            <span class="live-lbl">最新期</span>
            <span class="live-exp" id="liveExp">--</span>
        </div>
        <div class="vline"></div>
        <div class="sync-area">
            <span class="sync-label">📌 最新一期</span>
            <span class="sync-nums" id="latestDrawNums">--</span>
            <span class="sync-label">特码</span>
            <span class="sync-special" id="latestDrawSpecial">--</span>
        </div>
        <button class="btn btn-mini btn-danger" id="clearBtn">🗑 清空</button>
        <div class="vline"></div>
        <div class="sync-area">
            <span class="sync-label">📝 手动入录</span>
            <input type="text" id="manualExpect" class="manual-input" placeholder="期号(可空)" style="width:70px;">
            <input type="text" id="manualNums" class="manual-input" placeholder="号码(单个=特码)" style="width:120px;">
            <button class="btn-sync-live" id="manualAddBtn">添加</button>
            <span class="fb" id="manualFb"></span>
        </div>
        <div class="actions">
            <button class="btn btn-mini" id="syncBtn" title="从官方接口同步最新开奖">🔄 同步开奖</button>
            <button class="btn btn-mini" id="historyBtn" onclick="openHistoryAPI()" title="历史开奖接口" style="background:linear-gradient(90deg, #8b5cf6, #a78bfa);color:#fff;border:none;">📜 历史开奖</button>
            <button class="btn btn-mini" id="settingsBtn">⚙ 设置</button>
            <span class="fb" id="syncStatus" style="font-size:.58rem;color:var(--text-muted);"></span>
        </div>
    </div>

    <!-- TAB NAV -->
    <div class="tab-nav">
        <button class="tab-btn active" data-tab="dashboard">📊 仪表盘</button>
        <button class="tab-btn" data-tab="zoneintegrate">📊 区间数字整合</button>
        <button class="tab-btn" data-tab="zones">🎯 区间走势</button>
        <button class="tab-btn" data-tab="pi">π 数能量预测</button>
        <button class="tab-btn" data-tab="szs">🎲 三中三预测</button>
        <button class="tab-btn" data-tab="trend">📈 走势分析</button>
        <button class="tab-btn" data-tab="heatmap">🔥 热冷分析</button>
        <button class="tab-btn" data-tab="zodiacpyramid">🐉 生肖金字塔</button>
        <button class="tab-btn" data-tab="reference">🎨 参考资料</button>
    </div>

    <!-- MAIN SCROLL -->
    <div class="main-scroll">

        <!-- ===== DASHBOARD ===== -->
        <div class="tab-panel active" id="tab-dashboard">
            <div class="stats-row">
                <div class="stat-card sc-cyan stat-card-large" style="grid-column: 1 / -1;">
                    <div class="stat-lbl">🔁 混沌量子推荐档位 · 重码/独码整合分析</div>
                    <div class="stat-val vc" id="stat-zone-pred" style="font-size:.7rem;min-height:70px;display:flex;flex-direction:column;align-items:center;justify-content:center;padding:6px 0;">
                        <div class="zone-dup-display">
                            <div class="zone-dup-row" id="stat-zone-dup"><span class="zone-dup-label" style="color:var(--gold-l);">🔁重码:</span><span class="zone-dup-nums">--</span></div>
                            <div class="zone-dup-row" id="stat-zone-uniq"><span class="zone-dup-label" style="color:var(--cyan);">❄️独码:</span><span class="zone-dup-nums">--</span></div>
                        </div>
                    </div>
                    <div class="stat-sub" id="stat-zone-sub">区间数字整合 · 重码/独码深度分析</div>
                    <div class="stat-feedback" id="stat-zone-feedback"></div>
                </div>
            </div>

            <!-- ===== RECORDS (开奖记录库，已移至仪表盘下方) ===== -->
            <div class="card">
                <div class="card-header" onclick="toggleCard(this)">
                    <span>📋 开奖记录库 · 最近50期 <span id="recCount" style="color:var(--gold-l);">(366期)</span></span>
                    <i class="fas fa-chevron-down chevron"></i>
                </div>
                <div class="card-body">
                    <div class="tbl-scroll">
                        <table class="data-table">
                            <thead><tr><th>期号</th><th>开奖号码 (前六位)</th><th>特码</th><th>生肖</th><th>波色</th></tr></thead>
                            <tbody id="historyTbody"></tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- ===== TREND ===== -->
        <div class="tab-panel" id="tab-trend">
            <div class="grid-2">
                <div class="card">
                    <div class="card-header" onclick="toggleCard(this)"><span>📈 近10期特码走势图</span><i class="fas fa-chevron-down chevron"></i></div>
                    <div class="card-body">
                        <div id="trendNumChart" class="chart-box chart-tall"></div>
                        <div class="insight-box" id="numAnalysis"></div>
                        <div class="note-row">
                            <input type="text" id="input_numNote" placeholder="手动记录笔记...">
                            <button class="btn btn-ghost" onclick="saveNote('numNote')">保存</button>
                            <span class="note-ok" id="note_numNote"></span>
                        </div>
                    </div>
                </div>
                <div class="card">
                    <div class="card-header" onclick="toggleCard(this)"><span>🐾 生肖走势图 · 量子档位建议</span><i class="fas fa-chevron-down chevron"></i></div>
                    <div class="card-body">
                        <div id="trendZodiacChart" class="chart-box chart-tall"></div>
                        <div class="insight-box insight-cyan" id="zodiacAdvice"></div>
                    </div>
                </div>
            </div>
        </div>

        <!-- ===== ZONES ===== -->
        <div class="tab-panel" id="tab-zones">
            <div class="grid-2">
                <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>区间① (1-16 / 17-33 / 34-49)</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div id="zone1Chart" class="chart-box"></div><div class="insight-box" id="zone1Insight"></div><div class="zone-quantum" id="zone1Quantum"><div class="zq-title title-with-copy"><span>⚛️ 混沌量子五码推荐</span><button class="copy-btn" id="zone1CopyBtn" onclick="copyNumsToClipboard(this.dataset.nums||'', this)"><i class="fas fa-copy"></i> 复制</button></div><div class="zq-balls" id="zone1QBalls"></div><div class="zq-basis" id="zone1QBasis"></div></div></div></div>
                <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>区间② (5-21 / 22-37 / 38-49+1-4)</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div id="zone2Chart" class="chart-box"></div><div class="insight-box" id="zone2Insight"></div><div class="zone-quantum" id="zone2Quantum"><div class="zq-title title-with-copy"><span>⚛️ 混沌量子五码推荐</span><button class="copy-btn" id="zone2CopyBtn" onclick="copyNumsToClipboard(this.dataset.nums||'', this)"><i class="fas fa-copy"></i> 复制</button></div><div class="zq-balls" id="zone2QBalls"></div><div class="zq-basis" id="zone2QBasis"></div></div></div></div>
                <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>区间③ (10-26 / 27-42 / 43-49+1-9)</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div id="zone3Chart" class="chart-box"></div><div class="insight-box" id="zone3Insight"></div><div class="zone-quantum" id="zone3Quantum"><div class="zq-title title-with-copy"><span>⚛️ 混沌量子五码推荐</span><button class="copy-btn" id="zone3CopyBtn" onclick="copyNumsToClipboard(this.dataset.nums||'', this)"><i class="fas fa-copy"></i> 复制</button></div><div class="zq-balls" id="zone3QBalls"></div><div class="zq-basis" id="zone3QBasis"></div></div></div></div>
                <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>区间④ (15-31 / 32-47 / 48-49+1-14)</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div id="zone4Chart" class="chart-box"></div><div class="insight-box" id="zone4Insight"></div><div class="zone-quantum" id="zone4Quantum"><div class="zq-title title-with-copy"><span>⚛️ 混沌量子五码推荐</span><button class="copy-btn" id="zone4CopyBtn" onclick="copyNumsToClipboard(this.dataset.nums||'', this)"><i class="fas fa-copy"></i> 复制</button></div><div class="zq-balls" id="zone4QBalls"></div><div class="zq-basis" id="zone4QBasis"></div></div></div></div>
                <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>区间⑤ (3-18 / 19-35 / 36-49+1-2)</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div id="zone5Chart" class="chart-box"></div><div class="insight-box" id="zone5Insight"></div><div class="zone-quantum" id="zone5Quantum"><div class="zq-title title-with-copy"><span>⚛️ 混沌量子五码推荐</span><button class="copy-btn" id="zone5CopyBtn" onclick="copyNumsToClipboard(this.dataset.nums||'', this)"><i class="fas fa-copy"></i> 复制</button></div><div class="zq-balls" id="zone5QBalls"></div><div class="zq-basis" id="zone5QBasis"></div></div></div></div>
                <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>区间⑥ (8-24 / 25-40 / 41-49+1-7)</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div id="zone6Chart" class="chart-box"></div><div class="insight-box" id="zone6Insight"></div><div class="zone-quantum" id="zone6Quantum"><div class="zq-title title-with-copy"><span>⚛️ 混沌量子五码推荐</span><button class="copy-btn" id="zone6CopyBtn" onclick="copyNumsToClipboard(this.dataset.nums||'', this)"><i class="fas fa-copy"></i> 复制</button></div><div class="zq-balls" id="zone6QBalls"></div><div class="zq-basis" id="zone6QBasis"></div></div></div></div>
            </div>
        </div>

        <!-- ===== HEATMAP ===== -->
        <div class="tab-panel" id="tab-heatmap">
            <div class="grid-2"><div class="card"><div class="card-header" onclick="toggleCard(this)"><span>🔥 热号 TOP 8</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div id="hotChart" class="chart-box chart-tall"></div></div></div>
            <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>❄️ 冷号遗漏 TOP 12</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div id="missChart" class="chart-box chart-tall"></div></div></div></div>
            <div class="insight-box insight-red" id="hotMissAnalysis" style="margin-top:0;"></div>
        </div>

        <!-- ===== ZODIAC PYRAMID ===== -->
        <div class="tab-panel" id="tab-zodiacpyramid">
            <div class="card card-gold">
                <div class="card-header" onclick="toggleCard(this)"><span>🐉 12生肖金字塔形态 · 走势分析与预测建议</span><i class="fas fa-chevron-down chevron"></i></div>
                <div class="card-body">
                    <div id="zodiacPyramidChart" class="chart-box chart-tall"></div>
                    <div class="insight-box insight-gold" id="zodiacPyramidAnalysis">加载中...</div>
                    <div class="grid-2" style="margin-top:12px;">
                        <div class="stat-card sc-gold">
                            <div class="stat-lbl">🔥 热门生肖趋势</div>
                            <div class="stat-val vg" id="zodiacHotTrend">--</div>
                            <div class="stat-sub">基于近N期开奖统计</div>
                        </div>
                        <div class="stat-card sc-cyan">
                            <div class="stat-lbl">❄️ 冷门生肖反抽</div>
                            <div class="stat-val vc" id="zodiacColdTrend">--</div>
                            <div class="stat-sub">遗漏期数分析</div>
                        </div>
                    </div>
                    <div class="insight-box insight-cyan" id="zodiacPyramidAdvice" style="margin-top:12px;">
                        📊 生肖金字塔形态分析将基于开奖历史数据，提供形态、规则、惯性、趋势的综合建议...
                    </div>
                </div>
            </div>
        </div>

        <!-- ===== REFERENCE ===== -->
        <div class="tab-panel" id="tab-reference">
            <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>🎨 红·蓝·绿波色号码表</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body" id="waveTableContainer"></div></div>
            <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>🐉 生肖号码网格 (波色高亮)</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body" id="zodiacFullTable"></div></div>
        </div>

        <!-- ===== π ENERGY ===== -->
        <div class="tab-panel" id="tab-pi">
            <div class="pi-hero"><div class="pi-symbol-bg">π</div><div class="pi-hero-content"><div class="pi-hero-title">π 数字能量预测系统</div><div class="pi-hero-sub">圆周率 · 宇宙常数 · 数字共振场</div><div class="pi-hero-date" id="piDateInfo">--</div></div><div class="pi-today-seed"><div class="pi-seed-label">今日π量子种子</div><div class="pi-seed-val" id="piSeedVal">--</div><div class="pi-seed-sub" id="piSeedSub">π[--]</div></div></div>
            <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>π 数字矩阵 · 前50位小数高亮激活图</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div class="pi-eq">π = 3. <span id="piDigitGrid"></span></div><div style="margin-top:8px;font-size:.66rem;color:var(--text-muted);"><span style="color:var(--red);">■</span> 红波数字能量 &nbsp;<span style="color:var(--blue);">■</span> 蓝波数字能量 &nbsp;<span style="color:var(--green);">■</span> 绿波数字能量 &nbsp;<span style="background:rgba(200,167,36,.3);padding:1px 5px;border-radius:4px;color:var(--gold-l);">■</span> 今日激活位</div></div></div>
            <div class="pi-energy-panel"><div class="pi-e-title title-with-copy"><span>✨ 今日 π 能量五码推荐</span><button class="copy-btn" id="piEnergyCopyBtn" onclick="copyNumsToClipboard(this.dataset.nums||'', this)"><i class="fas fa-copy"></i> 复制</button></div><div class="pi-e-nums" id="piEnergyNums"></div><div class="pi-e-calc" id="piCalcSteps"></div></div>
            <div class="grid-2"><div class="card"><div class="card-header" onclick="toggleCard(this)"><span>π 数字频率分布 (0-9各数字出现次数)</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div id="piFreqChart" class="chart-box"></div></div></div><div class="card"><div class="card-header" onclick="toggleCard(this)"><span>π 能量波色共振分析</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div id="piWaveChart" class="chart-box"></div><div class="insight-box insight-purple" id="piWaveAnalysis" style="margin-top:8px;"></div></div></div></div>
            <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>π × 开奖历史共振验证</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body"><div class="insight-box insight-cyan" id="piHistResonance">加载中...</div></div></div>
            <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>🎯 圆周率π恒态矩阵 · 1-49 能量分布场</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body">
                <div class="prob-legend">
                    <span><span class="lg-dot" style="background:rgba(200,167,36,.6);"></span>≥85% 极高概率</span>
                    <span><span class="lg-dot" style="background:rgba(34,211,238,.5);"></span>65-84% 较高概率</span>
                    <span><span class="lg-dot" style="background:rgba(192,132,252,.4);"></span>40-64% 中等概率</span>
                    <span><span class="lg-dot" style="background:rgba(255,255,255,.08);"></span>15-39% 较低概率</span>
                    <span><span class="lg-dot" style="background:rgba(248,113,113,.15);"></span>0-14% 极低概率</span>
                </div>
                <div class="prob-grid" id="probHeatmapGrid"></div>
                <div class="insight-box insight-gold" id="probSummary" style="margin-top:10px;">数据积累中...</div>
                <div class="pi-disclaimer" style="margin-top:10px;">⚠️ π恒态矩阵能量分布场基于七维因子（热号频率、遗漏值、生肖共振、波色均衡、区间共振、π能量、斐波那契）加权评分并按本地历史数据自学习调整，结果为统计娱乐参考，并非真实开奖概率。</div>
            </div></div>
            <div class="pi-disclaimer">⚠️ π数能量预测系统基于圆周率数学特性与彩票号码的数值共振关联模型，属于娱乐性统计分析，彩票结果具有完全随机性，本系统不构成任何投注建议。</div>
        </div>

        <!-- ===== 三中三栏兀预测 ===== -->
        <div class="tab-panel" id="tab-szs">
            <div class="szs-panel">
                <div class="szs-title">
                    <span>🎲</span> 三中三栏兀智能预测
                    <span style="font-size:.6rem; background:rgba(200,167,36,.15); padding:2px 8px; border-radius:12px;">基于历史特码组合推算</span>
                </div>
                <div class="szs-grid" id="szsGrid">
                    <div class="szs-card">
                        <div class="szs-card-title title-with-copy"><span>🔥 组合一（热号主导）</span><button class="copy-btn" id="szsFirstCopyBtn" onclick="copyNumsToClipboard(this.dataset.nums||'', this)"><i class="fas fa-copy"></i> 复制</button></div>
                        <div class="szs-numbers" id="szsFirst"></div>
                    </div>
                    <div class="szs-card">
                        <div class="szs-card-title title-with-copy"><span>❄️ 组合二（冷号反抽）</span><button class="copy-btn" id="szsMiddleCopyBtn" onclick="copyNumsToClipboard(this.dataset.nums||'', this)"><i class="fas fa-copy"></i> 复制</button></div>
                        <div class="szs-numbers" id="szsMiddle"></div>
                    </div>
                    <div class="szs-card">
                        <div class="szs-card-title title-with-copy"><span>🌊 组合三（波色轮动）</span><button class="copy-btn" id="szsLastCopyBtn" onclick="copyNumsToClipboard(this.dataset.nums||'', this)"><i class="fas fa-copy"></i> 复制</button></div>
                        <div class="szs-numbers" id="szsLast"></div>
                    </div>
                </div>
                <div class="szs-reason" id="szsReason">正在加载历史数据，分析特码组合规律...</div>
            </div>

            <!-- 三中三分析方法与统计结果 -->
            <div class="card card-gold" style="margin-top:0;">
                <div class="card-header" onclick="toggleCard(this)"><span>📐 三中三 · 分析方法与历史统计结果</span><i class="fas fa-chevron-down chevron"></i></div>
                <div class="card-body">
                    <div class="szs-stats-row" id="szsStatsRow">
                        <div class="szs-stat"><div class="szs-stat-val" id="szsHitRate">--</div><div class="szs-stat-lbl">近50期命中率</div></div>
                        <div class="szs-stat"><div class="szs-stat-val" id="szsAvgMiss">--</div><div class="szs-stat-lbl">平均遗漏期数</div></div>
                        <div class="szs-stat"><div class="szs-stat-val" id="szsMaxConsec">--</div><div class="szs-stat-lbl">最长连续未中</div></div>
                        <div class="szs-stat"><div class="szs-stat-val" id="szsBestZone">--</div><div class="szs-stat-lbl">最优区间命中</div></div>
                    </div>
                    <div class="szs-analysis-grid" style="margin-top:14px;">
                        <div class="szs-method-card">
                            <div class="szs-method-title">① 热冷交叉法</div>
                            <div class="szs-method-body">取近30期出现频次最高的5个热号与遗漏最久的5个冷号，各取1-2个号码交叉组合。热号代表趋势惯性，冷号代表统计回补。<br><br><span id="szsMethodResult1" style="color:var(--gold-l);font-size:.62rem;">加载中...</span></div>
                        </div>
                        <div class="szs-method-card">
                            <div class="szs-method-title">② 生肖波色矩阵法</div>
                            <div class="szs-method-body">分析近10期出现最少的生肖（冷肖），结合当前出现最少的波色，从交集中筛选3个号码。马年本命生肖（马）享有加权加分。<br><br><span id="szsMethodResult2" style="color:var(--cyan);font-size:.62rem;">加载中...</span></div>
                        </div>
                        <div class="szs-method-card">
                            <div class="szs-method-title">③ 区间档位推演法</div>
                            <div class="szs-method-body">基于四个区间的档位走势预测，找出下期最可能落在哪个号码范围，从预测档位号码池内选取3个号码作为组合候选。<br><br><span id="szsMethodResult3" style="color:var(--purple);font-size:.62rem;">加载中...</span></div>
                        </div>
                    </div>
                    <div class="insight-box insight-cyan" style="margin-top:12px;" id="szsAnalysisSummary">
                        📌 三中三分析方法综合说明：以上三种方法各有侧重，建议结合使用。热冷交叉法偏重频率统计，生肖矩阵法偏重周期规律，区间档位法偏重空间分布。三种方法交集号码具有最高综合参考价值。
                    </div>
                </div>
            </div>
        </div>

        <!-- ===== 区间数字整合面板 ===== -->
        <div class="tab-panel" id="tab-zoneintegrate">
            <div class="card"><div class="card-header" onclick="toggleCard(this)"><span>📊 六个区间数字整合 · 按组全号码展示</span><i class="fas fa-chevron-down chevron"></i></div><div class="card-body" id="zoneIntegrateBody"><div style="text-align:center; padding:20px;">加载数据中...</div></div></div>
            <div class="insight-box insight-cyan">📌 以上为每个区间下三个档位的全部原始号码。每个区间可手动自由选择档位，选择后自动联动到下方「各区间预测档位全部号码」及「混沌量子推荐档位 · 重码/独码整合分析」。</div>
            <!-- 底部统一展示区域 -->
            <div id="unifiedZoneNumbers" class="unified-recommend-section" style="margin-top:16px;"></div>
            <!-- 底部重码/不重码分析 -->
            <div class="zone-dup-section" id="zoneDupSection" style="margin-top:14px;"></div>
        </div>

    </div><!-- /main-scroll -->
</div><!-- /app-wrapper -->

<!-- 通用模态框（设置 / 确认对话框等） -->
<div class="modal-overlay" id="modalOverlay" onclick="if(event.target===this) closeModal()">
    <div class="modal-box" id="modalBox"></div>
</div>
<!-- 轻提示 -->
<div class="toast" id="toast"></div>


<script>
// ============================================================
// DATA MAPS (保持不变)
// ============================================================
const zodiacMapping = { "马":[1,13,25,37,49], "蛇":[2,14,26,38], "龙":[3,15,27,39], "兔":[4,16,28,40], "虎":[5,17,29,41], "牛":[6,18,30,42], "鼠":[7,19,31,43], "猪":[8,20,32,44], "狗":[9,21,33,45], "鸡":[10,22,34,46], "猴":[11,23,35,47], "羊":[12,24,36,48] };
const numToZodiac = {};
for (const [z, ns] of Object.entries(zodiacMapping)) ns.forEach(n => numToZodiac[n] = z);
function getZodiac(n) { return numToZodiac[n] || "未知"; }
const redSet = new Set([1,2,7,8,12,13,18,19,23,24,29,30,34,35,40,45,46]);
const blueSet = new Set([3,4,9,10,14,15,20,25,26,31,36,37,41,42,47,48]);
function getWave(n) { if (redSet.has(n)) return "红波"; if (blueSet.has(n)) return "蓝波"; return "绿波"; }
const zoneRules = [
    n => n <= 16 ? 1 : (n <= 33 ? 2 : 3),
    n => (n >= 5 && n <= 21) ? 1 : (n >= 22 && n <= 37) ? 2 : 3,
    n => (n >= 10 && n <= 26) ? 1 : (n >= 27 && n <= 42) ? 2 : 3,
    n => (n >= 15 && n <= 31) ? 1 : (n >= 32 && n <= 47) ? 2 : 3,
    n => (n >= 3 && n <= 18) ? 1 : (n >= 19 && n <= 35) ? 2 : 3,
    n => (n >= 8 && n <= 24) ? 1 : (n >= 25 && n <= 40) ? 2 : 3
];
const zoneLabels = [ ['1-16','17-33','34-49'], ['5-21','22-37','38-49+1-4'], ['10-26','27-42','43-49+1-9'], ['15-31','32-47','48-49+1-14'], ['3-18','19-35','36-49+1-2'], ['8-24','25-40','41-49+1-7'] ];
function extractSpecial(raw) { if (!raw) return null; const parts = raw.split(/[ ,]+/).filter(p=>p.trim()); if(!parts.length) return null; const n = parseInt(parts[parts.length-1],10); return isNaN(n)?null:n; }
function getDisplayNums(raw) { if(!raw) return ""; const parts = raw.split(/[ ,]+/).filter(p=>p.trim()); return parts.slice(0,-1).join(", "); }
function enrich(r) { return { ...r, zodiac: getZodiac(r.specialNum), wave: getWave(r.specialNum) }; }

// ============================================================
// 复制号码功能
// ============================================================
function showCopied(btnEl) {
    if(!btnEl) return;
    if(btnEl.dataset.copyTimer) clearTimeout(+btnEl.dataset.copyTimer);
    if(!btnEl.dataset.origHtml) btnEl.dataset.origHtml = btnEl.innerHTML;
    btnEl.innerHTML = '<i class="fas fa-check"></i> 已复制';
    btnEl.classList.add('copied');
    const t = setTimeout(()=>{ btnEl.innerHTML = btnEl.dataset.origHtml; btnEl.classList.remove('copied'); }, 1200);
    btnEl.dataset.copyTimer = t;
}
function fallbackCopyText(text, btnEl) {
    try {
        const ta = document.createElement('textarea');
        ta.value = text;
        ta.style.position = 'fixed';
        ta.style.opacity = '0';
        document.body.appendChild(ta);
        ta.focus(); ta.select();
        document.execCommand('copy');
        document.body.removeChild(ta);
    } catch(e) { console.warn('复制失败', e); }
    showCopied(btnEl);
}
window.copyNumsToClipboard = function(text, btnEl) {
    if(!text) { if(btnEl){ btnEl.dataset.origHtml = btnEl.innerHTML; btnEl.innerHTML='<i class="fas fa-times"></i> 无数据'; setTimeout(()=>{btnEl.innerHTML=btnEl.dataset.origHtml;},1200); } return; }
    const clean = String(text).split(',').map(s=>s.trim()).filter(Boolean).join(', ');
    if(navigator.clipboard && navigator.clipboard.writeText) {
        navigator.clipboard.writeText(clean).then(()=>showCopied(btnEl)).catch(()=>fallbackCopyText(clean, btnEl));
    } else {
        fallbackCopyText(clean, btnEl);
    }
};

// ============================================================
// INDEXEDDB + LOCALSTORAGE
// ============================================================
let db = null, allRecords = [];
const DB_NAME = "MacauProV6", STORE_NAME = "records", LS_KEY = "macau_lottery_records_v6";
function loadFromLocalStorage() { try { const data = localStorage.getItem(LS_KEY); if(data) { const parsed = JSON.parse(data); if(Array.isArray(parsed) && parsed.length) { allRecords = parsed; return true; } } } catch(e) { console.warn(e); } return false; }
function saveToLocalStorage(records) { try { localStorage.setItem(LS_KEY, JSON.stringify(records.slice(-500))); } catch(e) { console.warn(e); } }
function openDB() { return new Promise((res,rej)=>{ if(!window.indexedDB) { console.warn("IndexedDB not available"); db=null; loadFromLocalStorage(); res(null); return; } const req = indexedDB.open(DB_NAME,8); req.onupgradeneeded=e=>{ const d=e.target.result; if(!d.objectStoreNames.contains(STORE_NAME)) d.createObjectStore(STORE_NAME,{keyPath:"expect"}); }; req.onsuccess=e=>{ db=e.target.result; res(db); }; req.onerror=()=>{ console.warn("IndexedDB open failed"); db=null; loadFromLocalStorage(); res(null); }; }); }
async function getAllRecords() { if(!db) { loadFromLocalStorage(); return [...allRecords].sort((a,b)=>a.expect.localeCompare(b.expect)); } return new Promise((res,rej)=>{ try { const tx = db.transaction(STORE_NAME,"readonly"); const req = tx.objectStore(STORE_NAME).getAll(); req.onsuccess=()=>{ const records = req.result.sort((a,b)=>a.expect.localeCompare(b.expect)); saveToLocalStorage(records); res(records); }; req.onerror=()=>{ loadFromLocalStorage(); res([...allRecords]); }; } catch(e){ loadFromLocalStorage(); res([...allRecords]); } }); }
async function saveRecord(rec) { if(!db) { const existing = allRecords.findIndex(r=>r.expect===rec.expect); if(existing>=0) allRecords[existing]=rec; else allRecords.push(rec); saveToLocalStorage(allRecords); return true; } return new Promise((res,rej)=>{ try { const tx = db.transaction(STORE_NAME,"readwrite"); const req = tx.objectStore(STORE_NAME).put(rec); req.onsuccess=()=>{ saveToLocalStorage(allRecords); res(true); }; req.onerror=()=>{ saveToLocalStorage(allRecords); res(true); }; } catch(e){ saveToLocalStorage(allRecords); res(true); } }); }
async function deleteAllRecords() { allRecords=[]; saveToLocalStorage([]); if(!db) return; return new Promise((res,rej)=>{ try { const tx = db.transaction(STORE_NAME,"readwrite"); const req = tx.objectStore(STORE_NAME).clear(); req.onsuccess=()=>res(); req.onerror=()=>res(); } catch(e){ res(); } }); }
async function addRecord(expect,raw) { const special = extractSpecial(raw); if(!special || special<1 || special>49) throw new Error("特码无效(1-49)"); const rec = { expect, openCode: raw, specialNum: special, timestamp: Date.now() }; await saveRecord(rec); return rec; }
function nextExpect() { if(!allRecords.length) { const t=new Date(); return `${t.getFullYear()}${String(t.getMonth()+1).padStart(2,'0')}${String(t.getDate()).padStart(2,'0')}`; } const last=allRecords[allRecords.length-1].expect; const n=parseInt(last,10); return isNaN(n) ? String(Date.now()) : String(n+1); }
async function manualAddRecord() {
    const expectInp = document.getElementById("manualExpect");
    const numsInp = document.getElementById("manualNums");
    const fbSpan = document.getElementById("manualFb");
    const raw = numsInp ? numsInp.value.trim() : '';
    if(!raw) { if(fbSpan){ fbSpan.style.color='var(--red)'; fbSpan.textContent='请输入号码'; setTimeout(()=>{fbSpan.textContent='';fbSpan.style.color='var(--green)';},2000); } return; }
    let expect = expectInp ? expectInp.value.trim() : '';
    if(!expect) expect = nextExpect();
    try {
        await addRecord(expect, raw);
        allRecords = await getAllRecords();
        await refreshUI();
        if(expectInp) expectInp.value='';
        if(numsInp) numsInp.value='';
        if(fbSpan) { fbSpan.style.color='var(--green)'; fbSpan.textContent=`✅ 第${expect}期已入录并覆盖全局分析结果`; setTimeout(()=>fbSpan.textContent='',2800); }
    } catch(e) {
        if(fbSpan) { fbSpan.style.color='var(--red)'; fbSpan.textContent='❌ '+e.message; setTimeout(()=>{fbSpan.textContent='';fbSpan.style.color='var(--green)';},2500); }
    }
}

// ============================================================
// 图表 (保持不变)
// ============================================================
let numChart, zodiacChart, zoneCharts=[], hotChart, missChart, zodiacPyramidChart;
const ZONE_COLORS = ['#c8a724','#22d3ee','#f87171','#4ade80','#a78bfa','#fb923c'];
const ZODIAC_ORDER = ['鼠','牛','虎','兔','龙','蛇','马','羊','猴','鸡','狗','猪'];
function darkOpts(chart,opt) { opt.backgroundColor='transparent'; const axOpts={ axisLine:{lineStyle:{color:'rgba(255,255,255,.08)'}}, axisLabel:{color:'rgba(221,226,240,.5)',fontFamily:"'JetBrains Mono',monospace",fontSize:10}, splitLine:{lineStyle:{color:'rgba(255,255,255,.04)',type:'dashed'}} }; [opt.xAxis,opt.yAxis].forEach(ax=>{ if(!ax) return; const axes=Array.isArray(ax)?ax:[ax]; axes.forEach(a=>Object.assign(a,{...axOpts,...a})); }); opt.tooltip={ ...opt.tooltip, backgroundColor:'rgba(7,8,14,.96)', borderColor:'rgba(200,167,36,.22)', textStyle:{color:'#dde2f0',fontSize:11,fontFamily:"'Noto Serif SC',serif"} }; chart.setOption(opt); }
function updateTrendCharts(rec) { const periods=rec.map(r=>r.expect); const specials=rec.map(r=>r.specialNum); const zIdx=rec.map(r=>Object.keys(zodiacMapping).indexOf(r.zodiac)); const c1=document.getElementById("trendNumChart"), c2=document.getElementById("trendZodiacChart"); if(!c1||!c2) return; if(!numChart||numChart.isDisposed()) numChart=echarts.init(c1); darkOpts(numChart,{ tooltip:{trigger:'axis',formatter:p=>{ const i=p[0].dataIndex,r=rec[i]; return `${r.expect}<br/>特码 <b>${r.specialNum}</b><br/>生肖 ${r.zodiac}<br/>波色 ${r.wave}`; } }, xAxis:{type:'category',data:periods,axisLabel:{rotate:20}}, yAxis:{min:1,max:49,name:'号码',nameTextStyle:{color:'rgba(221,226,240,.35)',fontSize:9}}, series:[{type:'line',data:specials,smooth:true,lineStyle:{width:2.5,color:'#c8a724'},symbol:'circle',symbolSize:10,itemStyle:{color:'#f0cc52',borderColor:'rgba(200,167,36,.3)',borderWidth:2},areaStyle:{color:{type:'linear',x:0,y:0,x2:0,y2:1,colorStops:[{offset:0,color:'rgba(200,167,36,.18)'},{offset:1,color:'rgba(200,167,36,.01)'}]}}}] }); if(!zodiacChart||zodiacChart.isDisposed()) zodiacChart=echarts.init(c2); darkOpts(zodiacChart,{ tooltip:{trigger:'axis',formatter:p=>{ const i=p[0].dataIndex,r=rec[i]; return `${r.expect}<br/>生肖 <b>${r.zodiac}</b><br/>特码 ${r.specialNum}`; } }, xAxis:{type:'category',data:periods,axisLabel:{rotate:20}}, yAxis:{type:'category',data:Object.keys(zodiacMapping),name:'生肖',nameTextStyle:{color:'rgba(221,226,240,.35)',fontSize:9}}, series:[{type:'line',data:zIdx,smooth:false,lineStyle:{width:2.5,color:'#c084fc'},symbol:'diamond',symbolSize:10,itemStyle:{color:'#c084fc',borderColor:'rgba(192,132,252,.3)',borderWidth:2}}] }); }
function updateZoneCharts(rec) { const periods=rec.map(r=>r.expect); for(let i=0;i<6;i++) { const zd=rec.map(r=>zoneRules[i](r.specialNum)); const container=document.getElementById(`zone${i+1}Chart`); if(!container) continue; if(!zoneCharts[i]||zoneCharts[i].isDisposed()) zoneCharts[i]=echarts.init(container); darkOpts(zoneCharts[i],{ tooltip:{trigger:'axis',formatter:p=>{ const idx=p[0].dataIndex,r=rec[idx]; const tierName=zd[idx]===1?'一档(低区)':zd[idx]===2?'二档(中区)':'三档(高区)'; return `期号 ${r.expect}<br/>特码 <b>${r.specialNum}</b><br/>档位 <b>${tierName}</b>`; } }, xAxis:{type:'category',data:periods,axisLabel:{rotate:20,interval:0,fontSize:9},axisTick:{alignWithLabel:true}}, yAxis:{min:0.5,max:3.5,interval:1,axisLabel:{formatter:v=>v===1?'一档':v===2?'二档':v===3?'三档':''}}, series:[{type:'line',data:zd,step:'start',lineStyle:{width:2.5,color:ZONE_COLORS[i]},symbol:'circle',symbolSize:10,itemStyle:{color:ZONE_COLORS[i],borderColor:hexToRgba(ZONE_COLORS[i],0.35),borderWidth:3},areaStyle:{color:{type:'linear',x:0,y:0,x2:0,y2:1,colorStops:[{offset:0,color:hexToRgba(ZONE_COLORS[i],0.12)},{offset:1,color:'rgba(0,0,0,0)'}]}},markPoint:{data:[{type:'max',name:'当前档',symbolSize:28,label:{color:'#fff',fontSize:9,fontWeight:700},itemStyle:{color:ZONE_COLORS[i],shadowBlur:8,shadowColor:ZONE_COLORS[i]}}]}}] }); } }
function hexToRgba(hex,alpha) { const r=parseInt(hex.slice(1,3),16); const g=parseInt(hex.slice(3,5),16); const b=parseInt(hex.slice(5,7),16); return `rgba(${r},${g},${b},${alpha})`; }

// ============================================================
// 核心预测增强函数
// ============================================================
function computeZoneQuantumNumsEnhanced(zoneIdx, last10, all) {
    const vals = last10.map(r => zoneRules[zoneIdx](r.specialNum));
    const currTier = vals[vals.length - 1];
    const prevTier = vals.length >= 2 ? vals[vals.length - 2] : currTier;
    const last5 = vals.slice(-5);
    const sameCount = last5.filter(v => v === currTier).length;
    // 档位转换概率分析（基于全部历史）
    const tierTrans = {1:{1:0,2:0,3:0}, 2:{1:0,2:0,3:0}, 3:{1:0,2:0,3:0}};
    for(let i=1;i<vals.length;i++) { tierTrans[vals[i-1]][vals[i]]++; }
    const transTotal = Math.max(1, vals.length-1);
    // 波色分布分析
    const waveDist = {'红波':0,'蓝波':0,'绿波':0};
    last10.forEach(r => waveDist[r.wave]++);
    const minWave = Object.entries(waveDist).sort((a,b)=>a[1]-b[1])[0][0];
    // 生肖热度分析
    const zodHeat = {}; last10.forEach(r => zodHeat[r.zodiac]=(zodHeat[r.zodiac]||0)+1);
    const hotZods = Object.entries(zodHeat).sort((a,b)=>b[1]-a[1]).slice(0,3).map(([z])=>z);
    const coldZods = Object.entries(zodHeat).sort((a,b)=>a[1]-b[1]).slice(0,2).map(([z])=>z);
    let nextTier;
    if (sameCount >= 4) nextTier = currTier === 1 ? 2 : currTier === 3 ? 2 : (tierTrans[currTier][1] > tierTrans[currTier][3] ? 1 : 3);
    else if (sameCount >= 3) nextTier = currTier === 1 ? 2 : currTier === 3 ? 2 : (prevTier === 1 ? 3 : 1);
    else if (sameCount >= 2) nextTier = currTier === 2 ? (tierTrans[2][1] > tierTrans[2][3] ? 1 : 3) : (currTier === 1 ? 2 : 2);
    else nextTier = currTier;
    const upwardTrend = vals.slice(-3).every((v,i,a)=> i===0 || v>=a[i-1]);
    const downwardTrend = vals.slice(-3).every((v,i,a)=> i===0 || v<=a[i-1]);
    if(upwardTrend && nextTier < 3) nextTier++;
    if(downwardTrend && nextTier > 1) nextTier--;
    // 基于转换概率微调
    const transProb = tierTrans[currTier];
    if(transProb[nextTier] / transTotal < 0.15) {
        const alt = Object.entries(transProb).sort((a,b)=>b[1]-a[1]).map(([t])=>+t)[0];
        if(alt !== nextTier && Math.random() > 0.6) nextTier = alt;
    }
    const pool = [];
    for(let n=1; n<=49; n++) { if(zoneRules[zoneIdx](n) === nextTier) pool.push(n); }
    if(pool.length===0) { for(let n=1;n<=49;n++) pool.push(n); }
    const freq = new Array(50).fill(0);
    const safeAll = all && all.length ? all : last10;
    safeAll.forEach(r => { if(r.specialNum) freq[r.specialNum]++; });
    const missMap = new Array(50).fill(0);
    for(let i=1;i<=49;i++) missMap[i] = safeAll.length - (safeAll.findLastIndex(r => r.specialNum === i) + 1);
    // 波色回补权重
    const waveBoost = {};
    for(let n=1;n<=49;n++) { if(getWave(n)===minWave) waveBoost[n]=1.5; else waveBoost[n]=0; }
    // 生肖热度权重
    const zodBoost = {};
    for(let n=1;n<=49;n++) { const z=getZodiac(n); if(hotZods.includes(z)) zodBoost[n]=1.0; else if(coldZods.includes(z)) zodBoost[n]=0.6; else zodBoost[n]=0; }
    const scored = pool.map(n => {
        let score = 0;
        score += freq[n] * 0.6;
        score += Math.min(Math.max(missMap[n], 0) / 6, 4) * 0.8;
        if (zodiacMapping['马'].includes(n)) score += 1.5;
        const lastSpc = last10[last10.length-1].specialNum;
        const diff = Math.abs(n - lastSpc);
        if(diff <= 5) score += 1.2;
        if(diff >= 20) score += 0.6;
        score += waveBoost[n] || 0;
        score += zodBoost[n] || 0;
        score += (Math.sin(n * 0.37 + zoneIdx) + 1) * 0.5;
        // 档位历史命中加成
        const tierHits = safeAll.filter(r => zoneRules[zoneIdx](r.specialNum) === nextTier && Math.abs(r.specialNum - n) <= 3).length;
        score += tierHits * 0.3;
        return { n, score };
    }).sort((a,b) => b.score - a.score);
    return { nums: scored.slice(0,5).map(x=>x.n), nextTier };
}
function computeGodViewEnhanced(last10, all) {
    const freq = new Array(50).fill(0);
    all.forEach(r => { if(r.specialNum) freq[r.specialNum]++; });
    const hot = freq.map((c,n)=>({n,c})).filter(x=>x.n>0).sort((a,b)=>b.c-a.c).slice(0,6).map(h=>h.n);
    const cold = freq.map((c,n)=>({n,c})).filter(x=>x.n<=1 && x.n>0).map(c=>c.n).filter(n=>n>0);
    const lastSpc = last10[last10.length-1].specialNum;
    const qSeed = (lastSpc * 17 + new Date().getMinutes() + new Date().getDate()) % 49 + 1;
    const zodiacTrend = {};
    last10.forEach(r=>{ zodiacTrend[r.zodiac] = (zodiacTrend[r.zodiac]||0)+1; });
    const sortedZod = Object.entries(zodiacTrend).sort((a,b)=>b[1]-a[1]);
    const hotZod = sortedZod.slice(0,2).map(([z])=>z);
    const coldZod = sortedZod.slice(-2).map(([z])=>z);
    const cands = new Set();
    hot.slice(0,3).forEach(n=>cands.add(n));
    cold.slice(0,3).forEach(n=>cands.add(n));
    cands.add(qSeed);
    zodiacMapping["马"].forEach(n=>cands.add(n));
    hotZod.forEach(z=>zodiacMapping[z]?.forEach(n=>cands.add(n)));
    coldZod.forEach(z=>zodiacMapping[z]?.forEach(n=>cands.add(n)));
    while(cands.size < 5) cands.add(Math.floor(Math.random()*49)+1);
    const list = [...cands].slice(0,5);
    const reasoning = `⭐ 热号动量: ${hot.slice(0,3).join('、')} &nbsp;·&nbsp; ❄️ 冷号反抽: ${cold.slice(0,3).join('、')}<br>⚛️ 量子种子: ${qSeed} &nbsp;·&nbsp; 🐎 马年本命: ${zodiacMapping['马'].join('、')}<br>🔥 热门生肖: ${hotZod.join('、')} &nbsp;·&nbsp; 🧊 冷门生肖: ${coldZod.join('、')}<br>📊 综合加权评分筛选，兼顾热度、遗漏、生肖共振及马年效应。`;
    return { list, reasoning };
}
function enhanceQuantumAnalysis(last10) {
    const specials = last10.map(r=>r.specialNum);
    const shape = analyzeWaveform(specials);
    const diffs = [];
    for(let i=1;i<specials.length;i++) diffs.push(specials[i]-specials[i-1]);
    const avgDiff = diffs.reduce((a,b)=>a+b,0)/diffs.length;
    const volatility = Math.sqrt(diffs.map(d=>Math.pow(d-avgDiff,2)).reduce((a,b)=>a+b,0)/diffs.length);
    const lastSpc = specials[specials.length-1];
    const fibs = [0.236,0.382,0.5,0.618,0.786];
    const range = Math.max(...specials) - Math.min(...specials);
    const nextFibs = fibs.map(f => Math.round(Math.min(...specials) + range * f)).filter(v=>v>=1&&v<=49);
    const uniqueNext = [...new Set(nextFibs)];
    const prediction = uniqueNext.length ? uniqueNext[Math.floor(Math.random()*uniqueNext.length)] : lastSpc;
    let trendDesc = "";
    if(avgDiff > 2) trendDesc = "强势上升趋势，回调压力增大";
    else if(avgDiff < -2) trendDesc = "深度下跌趋势，反弹概率增加";
    else if(volatility > 8) trendDesc = "剧烈震荡，混沌相变临近";
    else trendDesc = "箱体整理，能量蓄积";
    return `<strong>混沌形态：</strong>${shape}<br>📊 <strong>特码序列：</strong>${specials.slice(-5).join(' → ')}<br>📈 <strong>波动率：</strong>${volatility.toFixed(2)} &nbsp; <strong>平均变动：</strong>${avgDiff.toFixed(2)}<br>🔮 <strong>斐波那契预测区间：</strong>${uniqueNext.slice(0,3).join('、')}<br>🌀 <strong>趋势研判：</strong>${trendDesc}<br>⚛️ 量子纠缠模型指向下期能量中心靠近 <strong style="color:var(--gold-l);">${prediction}</strong>，建议关注波色轮动。`;
}
function enhanceFourD(last10) {
    if(last10.length < 3) return "累积数据中，四维共振即将显现...";
    const sp = last10.map(r=>r.specialNum);
    const l3 = sp.slice(-3);
    const parity = l3.map(v=>v%2===0?'偶':'奇').join('-');
    const size = l3.map(v=>v>=25?'大':'小').join('-');
    const mean = (l3.reduce((a,b)=>a+b,0)/3).toFixed(1);
    const goldenMean = (l3[0]*0.618 + l3[1]*0.382).toFixed(1);
    const symmetry = Math.abs(l3[2] - l3[0]) <= 5 ? "对称性高，关注镜像号码" : "不对称态，关注补涨补跌";
    let predict = Math.round(parseFloat(mean)) + (Math.random() > 0.5 ? 1 : -1);
    if(predict<1) predict=1; if(predict>49) predict=49;
    return `✨ 近三期特码 [<strong>${l3.join(', ')}</strong>]<br>奇偶形态：<strong style="color:var(--cyan);">${parity}</strong> &nbsp;|&nbsp; 大小形态：<strong style="color:var(--purple);">${size}</strong><br>均值中枢：<strong style="color:var(--gold-l);">${mean}</strong> &nbsp; 黄金分割中枢：<strong>${goldenMean}</strong><br>🔍 形态特征：${symmetry}<br>🌌 四维共振推测下期能量交变点位于 <strong style="color:var(--green);">${predict}</strong> 附近，与马、蛇、龙呈量子纠缠态。`;
}
function updateThreeInThreePrediction(last10, all) {
    const firstDiv = document.getElementById("szsFirst");
    const middleDiv = document.getElementById("szsMiddle");
    const lastDiv = document.getElementById("szsLast");
    const reasonDiv = document.getElementById("szsReason");
    if (!firstDiv || !last10.length) return;
    const specials = last10.map(r => r.specialNum);
    const freq = new Array(50).fill(0);
    all.forEach(r => { if(r.specialNum) freq[r.specialNum]++; });
    const hotNums = freq.map((c,n)=>({n,c})).filter(x=>x.n>0).sort((a,b)=>b.c-a.c).slice(0,5).map(h=>h.n);
    const coldNums = freq.map((c,n)=>({n,c})).filter(x=>x.n>0).sort((a,b)=>a.c-b.c).slice(0,5).map(c=>c.n);
    const horseNums = zodiacMapping["马"];
    const firstSet = new Set();
    hotNums.slice(0,2).forEach(n => firstSet.add(n));
    horseNums.slice(0,2).forEach(n => firstSet.add(n));
    while(firstSet.size < 3) firstSet.add(Math.floor(Math.random()*49)+1);
    const first = [...firstSet].slice(0,3);
    const midSet = new Set();
    coldNums.slice(0,2).forEach(n => midSet.add(n));
    specials.slice(-3).forEach(n => midSet.add(n));
    while(midSet.size < 3) midSet.add(Math.floor(Math.random()*49)+1);
    const middle = [...midSet].slice(0,3);
    const lastSet = new Set();
    const waveCount = {'红波':0,'蓝波':0,'绿波':0};
    last10.forEach(r => waveCount[r.wave]++);
    const leastWave = Object.entries(waveCount).sort((a,b)=>+a[1]-+b[1])[0][0];
    for(let i=1;i<=49;i++) if(getWave(i)===leastWave && lastSet.size<3) lastSet.add(i);
    while(lastSet.size < 3) lastSet.add(Math.floor(Math.random()*49)+1);
    const last = [...lastSet].slice(0,3);
    firstDiv.innerHTML = first.map(n => `<span class="szs-number" style="background:${getWave(n)==='红波'?'rgba(248,113,113,0.3)':getWave(n)==='蓝波'?'rgba(96,165,250,0.3)':'rgba(74,222,128,0.3)'}">${n}</span>`).join('');
    middleDiv.innerHTML = middle.map(n => `<span class="szs-number" style="background:${getWave(n)==='红波'?'rgba(248,113,113,0.3)':getWave(n)==='蓝波'?'rgba(96,165,250,0.3)':'rgba(74,222,128,0.3)'}">${n}</span>`).join('');
    lastDiv.innerHTML = last.map(n => `<span class="szs-number" style="background:${getWave(n)==='红波'?'rgba(248,113,113,0.3)':getWave(n)==='蓝波'?'rgba(96,165,250,0.3)':'rgba(74,222,128,0.3)'}">${n}</span>`).join('');
    const szsFirstCopyBtn=document.getElementById("szsFirstCopyBtn"), szsMiddleCopyBtn=document.getElementById("szsMiddleCopyBtn"), szsLastCopyBtn=document.getElementById("szsLastCopyBtn");
    if(szsFirstCopyBtn) szsFirstCopyBtn.dataset.nums = first.join(', ');
    if(szsMiddleCopyBtn) szsMiddleCopyBtn.dataset.nums = middle.join(', ');
    if(szsLastCopyBtn) szsLastCopyBtn.dataset.nums = last.join(', ');
    reasonDiv.innerHTML = `🎲 三中三预测基于最近10期特码序列 [${specials.slice(-5).join(', ')}] 的走势规律生成。<br>🔥 组合一（热号主导）：融合热号（${hotNums.slice(0,2).join(', ')}）与马年本命生肖（${horseNums.slice(0,2).join(', ')}），代表趋势惯性。<br>❄️ 组合二（冷号反抽）：融合冷号（${coldNums.slice(0,2).join(', ')}）与近期出现号码（${specials.slice(-3).join(', ')}），代表统计回补概率。<br>🌊 组合三（波色轮动）：当前最低占比波色为 <strong>${leastWave}</strong>，优先筛选该波色号码，反补波色均衡。`;
    // 计算三中三分析统计
    updateSzsAnalysis(last10, all, freq, hotNums, coldNums, leastWave, first, middle, last);
}
function updateSzsAnalysis(last10, all, freq, hotNums, coldNums, leastWave, first, middle, last) {
    // 近50期命中率（三组任意一组与实际特码相符）
    const recent50 = all.slice(-50);
    let hitCount = 0;
    for(const r of recent50) {
        const sp = r.specialNum;
        if(first.includes(sp) || middle.includes(sp) || last.includes(sp)) hitCount++;
    }
    const hitRate = recent50.length ? (hitCount/recent50.length*100).toFixed(1)+'%' : '--';
    // 平均遗漏期数
    let missTotal = 0; let missCount = 0;
    for(let n=1;n<=49;n++) { if(freq[n]>0) { const lastIdx = all.findLastIndex(r=>r.specialNum===n); const miss = all.length - lastIdx - 1; missTotal+=miss; missCount++; } }
    const avgMiss = missCount ? (missTotal/missCount).toFixed(1) : '--';
    // 最长连续未中
    let maxConsec = 0; let curConsec = 0;
    for(const r of all.slice(-100)) {
        const sp = r.specialNum;
        if(!first.includes(sp) && !middle.includes(sp) && !last.includes(sp)) curConsec++;
        else { if(curConsec>maxConsec) maxConsec=curConsec; curConsec=0; }
    }
    if(curConsec>maxConsec) maxConsec=curConsec;
    // 最优区间
    const zHits = [0,0,0,0,0,0];
    for(const r of recent50) { for(let i=0;i<6;i++) { const tier = zoneRules[i](r.specialNum); if(tier===1) zHits[i]++; } }
    const bestZone = zHits.indexOf(Math.max(...zHits))+1;
    const el1=document.getElementById("szsHitRate"), el2=document.getElementById("szsAvgMiss");
    const el3=document.getElementById("szsMaxConsec"), el4=document.getElementById("szsBestZone");
    if(el1) el1.textContent=hitRate; if(el2) el2.textContent=avgMiss;
    if(el3) el3.textContent=maxConsec+'期'; if(el4) el4.textContent='区间'+bestZone;
    // 三种方法结果显示
    const r1 = document.getElementById("szsMethodResult1");
    const r2 = document.getElementById("szsMethodResult2");
    const r3 = document.getElementById("szsMethodResult3");
    if(r1) r1.textContent = `推荐号码：${hotNums.slice(0,2).join('、')} + ${coldNums.slice(0,1).join('、')} → 组合：${first.join('-')}`;
    if(r2) {
        const zodCount2={}; last10.forEach(r=>{zodCount2[r.zodiac]=(zodCount2[r.zodiac]||0)+1;});
        const coldZod2=Object.entries(zodCount2).sort((a,b)=>a[1]-b[1]).slice(0,2).map(([z])=>z);
        r2.textContent = `冷门生肖：${coldZod2.join('、')} + 波色：${leastWave} → 组合：${middle.join('-')}`;
    }
    if(r3) {
        const zoneTier = [];
        for(let i=0;i<4;i++) { const {nextTier}=computeZoneQuantumNumsEnhanced(i,last10,all); zoneTier.push(nextTier); }
        r3.textContent = `区间预测档位：${zoneTier.map((t,i)=>`区间${i+1}→${t===1?'低区':t===2?'中区':'高区'}`).join(' | ')} → 组合：${last.join('-')}`;
    }
    // 交集号码分析
    const allPredNums = new Set([...first,...middle,...last]);
    const intersection = [...allPredNums].filter(n=>first.includes(n)&&(middle.includes(n)||last.includes(n))||middle.includes(n)&&last.includes(n));
    const summaryEl = document.getElementById("szsAnalysisSummary");
    if(summaryEl) {
        const intersectionText = intersection.length ? `三方法交集号码（最高参考价值）：<strong style="color:var(--gold-l);">${intersection.join('、')}</strong>。` : '三组合无直接交集，各有侧重。';
        summaryEl.innerHTML = `📊 近50期综合命中率 <strong style="color:var(--cyan);">${hitRate}</strong>（三组任意一组含中）。${intersectionText}<br>⚡ 建议将三组交集号码作为优先参考，辅以各组独立号码灵活搭配。`;
    }
}
function analyzeWaveform(arr) { if(arr.length<5) return "数据积累中"; const diffs=[]; for(let i=1;i<arr.length;i++) diffs.push(arr[i]-arr[i-1]); const up=diffs.filter(d=>d>0).length, dn=diffs.filter(d=>d<0).length; if(up>dn+2) return "上升金字塔形态"; if(dn>up+2) return "阶梯坠落形态"; if(arr.slice(-3).every((v,i,a)=>i>0&&Math.abs(v-a[i-1])>8)) return "剧烈锯齿震荡"; return "混沌波浪态"; }
function updateAnalysis(last10, all) {
    if(!last10.length) return;
    const specials = last10.map(r=>r.specialNum);
    const shape = analyzeWaveform(specials);
    const el = document.getElementById("numAnalysis");
    if(el) el.innerHTML = enhanceQuantumAnalysis(last10, all);
    for(let i=1;i<=6;i++) {
        const vals = last10.map(r=>zoneRules[i-1](r.specialNum));
        const l3 = vals.slice(-3);
        const p1=(l3.filter(v=>v===1).length/3*100).toFixed(0);
        const p2=(l3.filter(v=>v===2).length/3*100).toFixed(0);
        const p3=(l3.filter(v=>v===3).length/3*100).toFixed(0);
        const tend = +p2>40?'中区共振':(+p3>40?'高区引力':'低区筑底');
        // 档位转换分析
        const trans = {1:0,2:0,3:0};
        for(let j=1;j<vals.length;j++) trans[vals[j]]++;
        const totalTrans = Math.max(1, vals.length-1);
        const dominant = Object.entries(trans).sort((a,b)=>b[1]-a[1])[0];
        const domTier = dominant[0], domPct = (dominant[1]/totalTrans*100).toFixed(0);
        // 波色在区间内的分布
        const zoneNums = []; for(let n=1;n<=49;n++) if(zoneRules[i-1](n)===parseInt(domTier)) zoneNums.push(n);
        const zoneWaves = zoneNums.map(n=>getWave(n));
        const zr=zoneWaves.filter(w=>w==='红波').length, zb=zoneWaves.filter(w=>w==='蓝波').length, zg=zoneWaves.filter(w=>w==='绿波').length;
        // 连续趋势
        const consec = vals.slice(-5);
        let consecSame = 1;
        for(let j=consec.length-2;j>=0;j--) { if(consec[j]===consec[consec.length-1]) consecSame++; else break; }
        // 增强：生肖在区间内的分布
        const zodDist = {};
        zoneNums.forEach(n => { const z=getZodiac(n); zodDist[z]=(zodDist[z]||0)+1; });
        const topZodInZone = Object.entries(zodDist).sort((a,b)=>b[1]-a[1]).slice(0,2).map(([z,c])=>`${z}(${c})`).join('、');
        // 增强：遗漏分析
        const allNums = all || last10;
        const missInZone = zoneNums.map(n => {
            const lastIdx = allNums.findLastIndex(r => r.specialNum === n);
            return { n, miss: allNums.length - lastIdx };
        }).sort((a,b)=>b.miss-a.miss).slice(0,3);
        const e = document.getElementById(`zone${i}Insight`);
        if(e) e.innerHTML = `⚛️ 近3期档位分布：一档 <strong>${p1}%</strong> | 二档 <strong>${p2}%</strong> | 三档 <strong>${p3}%</strong><br>🌀 混沌倾向：<strong style="color:var(--cyan);">${tend}</strong> &nbsp;|&nbsp; 历史主导档位：<strong style="color:var(--gold-l);">${domTier}档(${domPct}%)</strong><br>📊 当前连续${consecSame}期同档 · 区间波色分布：红${zr}·蓝${zb}·绿${zg}<br>🐉 区间生肖分布：${topZodInZone || '--'}<br>❄️ 最大遗漏号码：${missInZone.map(m=>`${m.n}(${m.miss}期)`).join('、')}<br>🔮 量子纠缠模型指向下期能量中心发生档位跃迁概率 <strong style="color:var(--purple);">${consecSame>=3?'高':'中'}</strong>`;
    }
    const hm = document.getElementById("hotMissAnalysis");
    if(hm) hm.innerHTML = `🔥 热号动量持续增强，高频号码进入缠斗区；❄️ 冷号量子反抽周期临近，博冷策略需结合波色矩阵综合判断。`;
    const qEl = document.getElementById("quantumContent");
    if(qEl) qEl.innerHTML = enhanceQuantumAnalysis(last10);
    const zodEl = document.getElementById("zodiacAdvice");
    if(zodEl) {
        const zc={}; last10.forEach(r=>{zc[r.zodiac]=(zc[r.zodiac]||0)+1;});
        const topZ = Object.entries(zc).sort((a,b)=>b[1]-a[1]).slice(0,3).map(([z,c])=>`<strong>${z}</strong>(${c}次)`).join('、');
        zodEl.innerHTML = `🐉 近10期热门生肖：${topZ}<br>马年逢冲生肖为鼠，适当规避。下期高关注：马、蛇、龙三肖纠缠态。`;
    }
}
function updateFourD(last10) { const el = document.getElementById("fourDRes"); if(!el) return; el.innerHTML = enhanceFourD(last10); }
function updateGodView(last10, all) {
    const gEl = document.getElementById("godNums"), bEl = document.getElementById("godBasis");
    if(!gEl || !last10.length) return;
    const { list, reasoning } = computeGodViewEnhanced(last10, all);
    gEl.innerHTML = list.map((n,idx)=>{
        const w=getWave(n), cls=w==='红波'?'gb-r':(w==='蓝波'?'gb-b':'gb-g'), z=getZodiac(n);
        return `<div class="god-ball-wrap"><div class="god-ball ${cls}" style="animation-delay:${idx*.05}s;">${n}</div><div class="ball-zod">${z}</div></div>`;
    }).join("");
    if(bEl) bEl.innerHTML = reasoning;
}
function updateZoneQuantum(last10, all) {
    const tierNames = ['','一档(低区)','二档(中区)','三档(高区)'];
    for(let i=0;i<6;i++) {
        const { nums, nextTier } = computeZoneQuantumNumsEnhanced(i, last10, all);
        const ballsEl = document.getElementById(`zone${i+1}QBalls`);
        const basisEl = document.getElementById(`zone${i+1}QBasis`);
        if(!ballsEl) continue;
        ballsEl.innerHTML = nums.map((n,idx)=>{
            const w=getWave(n), cls=w==='红波'?'gb-r':(w==='蓝波'?'gb-b':'gb-g'), z=getZodiac(n);
            return `<div class="zq-ball-wrap"><div class="zq-ball ${cls}" style="animation-delay:${idx*.06}s;">${n}</div><div class="zq-ball-lbl">${z}</div></div>`;
        }).join('');
        if(basisEl) basisEl.innerHTML = `预测下期档位：<strong style="color:${ZONE_COLORS[i]};">${tierNames[nextTier]}</strong> &nbsp;|&nbsp; 候选池：${nums.join('、')}`;
        const copyBtn = document.getElementById(`zone${i+1}CopyBtn`);
        if(copyBtn) copyBtn.dataset.nums = nums.join(', ');
    }
    updateZoneIntegratePanel(last10, all);
}
function getZoneManualTiers() {
    let manualTiers = {};
    try { const saved = localStorage.getItem("macau_zone_manual_tiers_v1"); if(saved) manualTiers = JSON.parse(saved); }catch(e){}
    return manualTiers;
}
function updateStatCards(last10, all) {
    if(!all.length) return;
    const last = enrich(all[all.length-1]);
    // 近20期波色比
    const last20 = all.slice(-20).map(r=>enrich(r));
    let r20=0,b20=0,g20=0;
    last20.forEach(r=>{ if(r.wave==='红波') r20++; else if(r.wave==='蓝波') b20++; else g20++; });
    const w20El = document.getElementById("stat-wave20");
    if(w20El) w20El.textContent = `${r20} : ${b20} : ${g20}`;
    // 近5期奇偶走势
    const last5spc = all.slice(-5).map(r=>r.specialNum);
    const parityStr = last5spc.map(n=>n%2===0?'偶':'奇').join('-');
    const oddCount = last5spc.filter(n=>n%2!==0).length;
    const parityEl = document.getElementById("stat-parity");
    const paritySub = document.getElementById("stat-parity-sub");
    if(parityEl) parityEl.textContent = parityStr;
    if(paritySub) paritySub.textContent = `奇${oddCount}偶${5-oddCount}（近5期）`;
}
function updateZoneSummary(last10) {
    const el = document.getElementById("zoneSummary");
    if(!el || !last10.length) return;
    const zNames = ['区间①','区间②','区间③','区间④','区间⑤','区间⑥'];
    const zColors = ['var(--gold-l)','var(--cyan)','var(--red)','var(--green)','var(--purple)','#fb923c'];
    el.innerHTML = zNames.map((name,i)=>{
        const vals = last10.map(r=>zoneRules[i](r.specialNum));
        const p1=(vals.filter(v=>v===1).length/vals.length*100).toFixed(0);
        const p2=(vals.filter(v=>v===2).length/vals.length*100).toFixed(0);
        const p3=(vals.filter(v=>v===3).length/vals.length*100).toFixed(0);
        const cur = vals[vals.length-1];
        const curLbl = cur===1?'一档(低区)':cur===2?'二档(中区)':'三档(高区)';
        return `<div class="insight-box" style="margin:0;"><strong style="color:${zColors[i]};">${name}</strong><br>一档 <strong>${p1}%</strong> | 二档 <strong>${p2}%</strong> | 三档 <strong>${p3}%</strong><br>当前档位：<strong style="color:var(--cyan);">${curLbl}</strong></div>`;
    }).join("");
}
function updateZodiacPyramid(last10, all) {
    const container = document.getElementById("zodiacPyramidChart");
    const analysisEl = document.getElementById("zodiacPyramidAnalysis");
    const hotEl = document.getElementById("zodiacHotTrend");
    const coldEl = document.getElementById("zodiacColdTrend");
    const adviceEl = document.getElementById("zodiacPyramidAdvice");
    if(!container || !last10.length) return;
    
    // 统计各生肖出现次数
    const zodCount = {};
    const zodMiss = {};
    ZODIAC_ORDER.forEach(z => { zodCount[z] = 0; zodMiss[z] = 0; });
    
    // 近N期统计
    last10.forEach(r => { zodCount[r.zodiac] = (zodCount[r.zodiac] || 0) + 1; });
    
    // 计算遗漏
    ZODIAC_ORDER.forEach(z => {
        for(let i = all.length - 1; i >= 0; i--) {
            if(all[i].zodiac === z) { zodMiss[z] = all.length - 1 - i; break; }
        }
    });
    
    // 排序得到热门和冷门
    const sortedByCount = ZODIAC_ORDER.map(z => ({z, count: zodCount[z] || 0, miss: zodMiss[z]}))
        .sort((a,b) => b.count - a.count);
    const hotZods = sortedByCount.slice(0, 4);
    const coldZods = sortedByCount.slice(-4).reverse();
    
    // 金字塔形态分析
    const hotTrend = hotZods.map(x => `${x.z}(${x.count}次)`).join('、');
    const coldTrend = coldZods.map(x => `${x.z}(漏${x.miss}期)`).join('、');
    if(hotEl) hotEl.innerHTML = hotTrend;
    if(coldEl) coldEl.innerHTML = coldTrend;
    
    // 形态判断
    const last3Zods = last10.slice(-3).map(r => r.zodiac);
    const shapePattern = analyzeZodiacShape(last3Zods, sortedByCount);
    
    if(analysisEl) {
        analysisEl.innerHTML = `
            <strong style="color:var(--gold-l);">🐉 生肖金字塔形态分析</strong><br>
            近${last10.length}期热门生肖：<strong style="color:var(--red);">${hotTrend}</strong><br>
            近${last10.length}期冷门生肖：<strong style="color:var(--cyan);">${coldTrend}</strong><br>
            <strong>形态特征：</strong>${shapePattern.desc}<br>
            <strong>惯性趋势：</strong>${shapePattern.inertia}<br>
            <strong>规则建议：</strong>${shapePattern.rule}
        `;
    }
    
    if(adviceEl) {
        adviceEl.innerHTML = `
            <strong style="color:var(--gold-l);">📊 生肖金字塔综合建议</strong><br>
            🎯 <strong>形态：</strong>${shapePattern.desc}<br>
            🔄 <strong>惯性：</strong>${shapePattern.inertia}<br>
            📈 <strong>趋势：</strong>${shapePattern.trend}<br>
            ⚖️ <strong>规则：</strong>${shapePattern.rule}<br>
            🔮 <strong>预测：</strong>下期关注 <strong style="color:var(--gold-l);">${shapePattern.predict}</strong> 生肖
        `;
    }
    
    // 绘制金字塔图表
    if(!zodiacPyramidChart || zodiacPyramidChart.isDisposed()) zodiacPyramidChart = echarts.init(container);
    const pyramidData = sortedByCount.map((x, idx) => ({
        name: x.z,
        value: x.count + 1,
        itemStyle: { color: idx < 4 ? '#c8a724' : idx < 8 ? '#22d3ee' : '#60a5fa' }
    }));
    
    darkOpts(zodiacPyramidChart, {
        tooltip: { trigger: 'item', formatter: p => `${p.name}: 出现${p.value-1}次<br>遗漏${zodMiss[p.name]}期` },
        series: [{
            type: 'funnel',
            sort: 'none',
            left: '10%', top: 10, bottom: 10, width: '80%',
            min: 0, max: Math.max(...pyramidData.map(d => d.value)) + 1,
            label: { show: true, position: 'inside', color: '#fff', fontSize: 11, formatter: '{b}' },
            labelLine: { show: false },
            itemStyle: { borderColor: '#0a0c18', borderWidth: 2 },
            emphasis: { label: { fontSize: 13, fontWeight: 'bold' } },
            data: pyramidData
        }]
    });
}

function analyzeZodiacShape(last3Zods, sortedByCount) {
    // 分析最近3期的生肖形态
    const uniqueInLast3 = [...new Set(last3Zods)].length;
    const hotInLast3 = last3Zods.filter(z => sortedByCount.slice(0,4).some(h => h.z === z)).length;
    
    let desc, inertia, trend, rule, predict;
    
    if(uniqueInLast3 === 1) {
        desc = '🔺 单生肖连庄形态（金字塔尖）';
        inertia = '强势惯性，连庄生肖 momentum 极高';
        trend = '延续概率 65%，但需防范反转';
        rule = '连庄3期后，第4期反转概率显著增加';
        predict = sortedByCount[1]?.z || '蛇';
    } else if(uniqueInLast3 === 2) {
        desc = '🔺 双生肖交替形态（金字塔腰）';
        inertia = '交替惯性，双生肖缠斗态';
        trend = '交替延续或引入第三生肖';
        rule = '双生肖交替2-3周期后，通常引入新生肖';
        predict = sortedByCount[0]?.z || '马';
    } else if(uniqueInLast3 === 3) {
        desc = '🔺 三生肖轮动形态（金字塔基）';
        inertia = '分散惯性，无主导生肖';
        trend = '混沌态，下期可能回归热门或继续分散';
        rule = '三生肖轮动后，下期 60% 概率回归前2期之一';
        predict = sortedByCount[0]?.z || '龙';
    } else {
        desc = '🔺 多生肖混沌形态（金字塔底）';
        inertia = '无明确惯性，完全混沌';
        trend = '随机游走，需结合波色和区间分析';
        rule = '混沌态后，下期通常出现热门生肖回补';
        predict = sortedByCount[0]?.z || '马';
    }
    
    // 根据热门生肖修正预测
    if(hotInLast3 >= 2) {
        predict = sortedByCount[sortedByCount.length - 1]?.z || '羊';
        trend += ' · 热门生肖过热，关注冷门反抽';
    }
    
    return { desc, inertia, trend, rule, predict };
}

function updateHotMiss(all) {
    const freq = new Array(50).fill(0);
    all.forEach(r=>{if(r.specialNum) freq[r.specialNum]++;});
    const hot = freq.map((c,n)=>({n,c})).filter(x=>x.n>0).sort((a,b)=>b.c-a.c).slice(0,8);
    const missMap = new Array(50).fill(0);
    for(let i=1;i<=49;i++) missMap[i] = Math.max(0, all.length - (all.findLastIndex(r=>r.specialNum===i)+1));
    const miss = missMap.slice(1).map((m,i)=>({n:i+1,m})).sort((a,b)=>b.m-a.m).slice(0,12);
    const hotContainer = document.getElementById("hotChart"), missContainer = document.getElementById("missChart");
    if(hotContainer) { if(!hotChart||hotChart.isDisposed()) hotChart=echarts.init(hotContainer); darkOpts(hotChart,{ tooltip:{trigger:'axis'}, xAxis:{type:'category',data:hot.map(h=>h.n)}, yAxis:{name:'频次',nameTextStyle:{color:'rgba(221,226,240,.35)',fontSize:9}}, series:[{type:'bar',data:hot.map(h=>h.c),itemStyle:{color:{type:'linear',x:0,y:0,x2:0,y2:1,colorStops:[{offset:0,color:'#f87171'},{offset:1,color:'rgba(248,113,113,.25)'}]},borderRadius:[6,6,0,0]}}] }); }
    if(missContainer) { if(!missChart||missChart.isDisposed()) missChart=echarts.init(missContainer); darkOpts(missChart,{ tooltip:{trigger:'axis'}, xAxis:{type:'category',data:miss.map(m=>m.n),axisLabel:{rotate:45}}, yAxis:{name:'遗漏期',nameTextStyle:{color:'rgba(221,226,240,.35)',fontSize:9}}, series:[{type:'bar',data:miss.map(m=>m.m),itemStyle:{color:{type:'linear',x:0,y:0,x2:0,y2:1,colorStops:[{offset:0,color:'#f97316'},{offset:1,color:'rgba(249,115,22,.22)'}]},borderRadius:[6,6,0,0]}}] }); }
}
// 整合面板：显示所有原始号码 + 底部统一展示预测档位的全部号码
function getZoneDupNums(last10, all, manualTiers) {
    const predSets = [];
    for(let i=0;i<6;i++) {
        let nextTier;
        if(manualTiers && manualTiers[i]) {
            nextTier = manualTiers[i];
        } else {
            const { nextTier: autoTier } = computeZoneQuantumNumsEnhanced(i, last10, all);
            nextTier = autoTier;
        }
        const nums = [];
        for(let n=1;n<=49;n++) { if(zoneRules[i](n) === nextTier) nums.push(n); }
        predSets.push(nums);
    }
    const numCount = {};
    for(const nums of predSets) nums.forEach(n=>{ numCount[n]=(numCount[n]||0)+1; });
    const dupNums = Object.entries(numCount).filter(([n,c])=>c>=2).sort((a,b)=>b[1]-a[1]).map(([n,c])=>({n:+n,c}));
    const uniqueNums = Object.entries(numCount).filter(([n,c])=>c===1).map(([n])=>+n).sort((a,b)=>a-b);
    const totalUnique = Object.keys(numCount).length;
    const allUniqueSorted = Object.keys(numCount).map(Number).sort((a,b)=>a-b);
    return { dupNums, uniqueNums, totalUnique, allUniqueSorted };
}
function updateZoneIntegratePanel(last10, all) {
    const container = document.getElementById("zoneIntegrateBody");
    if(!container) return;
    if(!all || all.length===0) { container.innerHTML = '<div style="text-align:center; padding:20px;">暂无数据，请先在顶部手动录入开奖记录。</div>'; return; }
    const zoneNames = ['区间① (1-16 / 17-33 / 34-49)', '区间② (5-21 / 22-37 / 38-49+1-4)', '区间③ (10-26 / 27-42 / 43-49+1-9)', '区间④ (15-31 / 32-47 / 48-49+1-14)', '区间⑤ (3-18 / 19-35 / 36-49+1-2)', '区间⑥ (8-24 / 25-40 / 41-49+1-7)'];
    const zColors = ['#c8a724','#22d3ee','#f87171','#4ade80','#a78bfa','#fb923c'];
    const zoneRanges = [ [[1,16],[17,33],[34,49]], [[5,21],[22,37],[38,49],[1,4]], [[10,26],[27,42],[43,49],[1,9]], [[15,31],[32,47],[48,49],[1,14]], [[3,18],[19,35],[36,49],[1,2]], [[8,24],[25,40],[41,49],[1,7]] ];
    const tierNames = ['一档(低区)', '二档(中区)', '三档(高区)'];
    // 读取手动选择
    let manualTiers = {};
    try { const saved = localStorage.getItem("macau_zone_manual_tiers_v1"); if(saved) manualTiers = JSON.parse(saved); }catch(e){}
    let cardsHtml = `<div class="zone-int-cards">`;
    for(let i=0;i<6;i++) {
        const ranges = zoneRanges[i];
        let groupsHtml = '';
        for(let g=0;g<ranges.length;g++) {
            let nums = [];
            const [start,end] = ranges[g];
            for(let num=start;num<=end;num++) nums.push(num);
            const uniqueNums = [...new Set(nums)].sort((a,b)=>a-b);
            const groupName = (g===0)?'一档':(g===1)?'二档':'三档';
            groupsHtml += `<div class="zone-number-group"><span class="group-name">${groupName}</span><div class="group-nums">${uniqueNums.map(n=>`<span class="num-mini">${n}</span>`).join('')}</div></div>`;
        }
        const { nextTier } = computeZoneQuantumNumsEnhanced(i, last10, all);
        const autoTierName = tierNames[nextTier-1];
        const manualTier = manualTiers[i];
        cardsHtml += `
            <div class="zone-int-card">
                <div class="zone-int-title" style="color:${zColors[i]};">📌 ${zoneNames[i]}</div>
                <div class="zone-number-list">${groupsHtml}</div>
                <div class="zone-manual-select" style="margin-top:10px;padding-top:8px;border-top:1px dashed var(--border2);">
                    <div style="display:flex;align-items:center;gap:8px;flex-wrap:wrap;">
                        <span style="font-size:.62rem;color:var(--text-muted);">🎚️ 手动选择档位：</span>
                        <select class="zone-tier-select" id="zoneTierSelect${i}" onchange="onZoneTierChange(this,${i})" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.62rem;padding:3px 6px;cursor:pointer;">
                            <option value="" ${!manualTier?'selected':''}>🤖 自动预测 (${autoTierName})</option>
                            <option value="1" ${manualTier===1?'selected':''}>一档 (低区)</option>
                            <option value="2" ${manualTier===2?'selected':''}>二档 (中区)</option>
                            <option value="3" ${manualTier===3?'selected':''}>三档 (高区)</option>
                        </select>
                        <span id="zoneTierBadge${i}" class="${manualTier?'zone-manual-badge':'zone-auto-badge'}" style="font-size:.55rem;padding:1px 6px;border-radius:8px;">${manualTier?'已手动：'+tierNames[manualTier-1]:'当前：'+autoTierName}</span>
                    </div>
                </div>
            </div>
        `;
    }
    cardsHtml += `</div>`;
    container.innerHTML = cardsHtml;
    
    // 底部统一展示每个区间预测档位的全部号码
    renderUnifiedZoneNumbers(last10, all, manualTiers);
    // 重码分析
    renderZoneDupSection(last10, all, manualTiers);
}
function renderUnifiedZoneNumbers(last10, all, manualTiers) {
    const unifiedContainer = document.getElementById("unifiedZoneNumbers");
    if(!unifiedContainer) return;
    const tierNames = ['一档(低区)', '二档(中区)', '三档(高区)'];
    let unifiedHtml = `<div class="unified-title">📊 各区间预测档位全部号码（混沌量子推荐档位）</div><div class="unified-grid">`;
    for(let i=0;i<6;i++) {
        let nextTier;
        let isManual = false;
        if(manualTiers && manualTiers[i]) { nextTier = manualTiers[i]; isManual = true; }
        else { const { nextTier: autoTier } = computeZoneQuantumNumsEnhanced(i, last10, all); nextTier = autoTier; }
        const fullNums = [];
        for(let n=1;n<=49;n++) { if(zoneRules[i](n) === nextTier) fullNums.push(n); }
        fullNums.sort((a,b)=>a-b);
        unifiedHtml += `
            <div class="unified-card">
                <div class="unified-card-title title-with-copy"><span>区间${i+1} ${isManual?'👤手动':'🤖自动'}：${tierNames[nextTier-1]}</span><button class="copy-btn" onclick="copyNumsToClipboard('${fullNums.join(',')}', this)"><i class="fas fa-copy"></i> 复制</button></div>
                <div class="unified-nums">${fullNums.map(n=>`<span class="num-mini">${n}</span>`).join('')}</div>
            </div>
        `;
    }
    unifiedHtml += `</div>`;
    unifiedContainer.innerHTML = unifiedHtml;
}
function renderZoneDupSection(last10, all, manualTiers) {
    const dupContainer = document.getElementById("zoneDupSection");
    if(!dupContainer) return;
    const { dupNums, uniqueNums, totalUnique, allUniqueSorted } = getZoneDupNums(last10, all, manualTiers);
    const hasManual = manualTiers && Object.keys(manualTiers).length > 0;
    dupContainer.innerHTML = `
        <div class="zone-dup-title title-with-copy"><span>🔁 混沌量子推荐档位 · 重码 / 独码整合分析 ${hasManual?'(含手动选择)':''}</span><button class="copy-btn" onclick="copyNumsToClipboard('${allUniqueSorted.join(',')}', this)"><i class="fas fa-copy"></i> 复制</button></div>
        <div style="font-size:.68rem;color:var(--text-muted);margin-bottom:10px;">
            六区间预测档位共包含 <strong style="color:var(--gold-l);">${totalUnique}</strong> 个不同号码，
            其中 <strong style="color:var(--red);">重码（出现≥2个区间）${dupNums.length}</strong> 个，
            <strong style="color:var(--green);">独码（仅1个区间）${uniqueNums.length}</strong> 个。
            重码代表多区间共振，参考价值更高。${hasManual?'<br><span style="color:var(--gold-l);">⚠️ 当前已应用手动选择档位</span>':''}
        </div>
        <div class="zone-dup-grid">
            <div class="zone-dup-card">
                <div class="zone-dup-card-title title-with-copy"><span>🔴 重码号码（多区间共振，${dupNums.length}个）</span><button class="copy-btn" onclick="copyNumsToClipboard('${dupNums.map(({n})=>n).join(',')}', this)"><i class="fas fa-copy"></i> 复制</button></div>
                <div class="zone-dup-nums">${dupNums.map(({n,c})=>`<span class="num-mini num-dup" title="出现${c}个区间">${n}<sup style="font-size:.45rem;">×${c}</sup></span>`).join('')||'<span style="color:var(--text-muted);font-size:.66rem;">无重码</span>'}</div>
            </div>
            <div class="zone-dup-card">
                <div class="zone-dup-card-title title-with-copy"><span>🟢 独码号码（单区间独有，${uniqueNums.length}个）</span><button class="copy-btn" onclick="copyNumsToClipboard('${uniqueNums.join(',')}', this)"><i class="fas fa-copy"></i> 复制</button></div>
                <div class="zone-dup-nums">${uniqueNums.map(n=>`<span class="num-mini num-unique">${n}</span>`).join('')}</div>
            </div>
        </div>
        <div style="margin-top:10px;font-size:.65rem;color:var(--text-muted);line-height:1.6;">
            📌 重码分析：<strong>重码 ${dupNums.length} 次</strong>（出现在2个以上区间），<strong>不重码 ${uniqueNums.length} 次</strong>（仅出现在1个区间）。
            多区间重叠的号码具有更强的统计共振信号，建议优先关注重码号码。
        </div>
    `;
}
function onZoneTierChange(select, zoneIndex) {
    const val = select.value;
    let manualTiers = {};
    try { const saved = localStorage.getItem("macau_zone_manual_tiers_v1"); if(saved) manualTiers = JSON.parse(saved); }catch(e){}
    if(val === '') { delete manualTiers[zoneIndex]; }
    else { manualTiers[zoneIndex] = parseInt(val, 10); }
    try { localStorage.setItem("macau_zone_manual_tiers_v1", JSON.stringify(manualTiers)); }catch(e){}
    // 立即联动更新
    const all = allRecords.map(r=>enrich(r));
    const last10 = all.slice(-getAnalysisWindow());
    renderUnifiedZoneNumbers(last10, all, manualTiers);
    renderZoneDupSection(last10, all, manualTiers);
    // 更新仪表盘重码/独码
    updateDashboardPredictions(last10, all);
    // 更新badge
    const badge = document.getElementById(`zoneTierBadge${zoneIndex}`);
    const tierNames = ['一档(低区)', '二档(中区)', '三档(高区)'];
    if(badge) {
        if(val === '') {
            const autoTier = computeZoneQuantumNumsEnhanced(zoneIndex, last10, all).nextTier;
            badge.className = 'zone-auto-badge';
            badge.style.cssText = 'font-size:.55rem;padding:1px 6px;border-radius:8px;background:rgba(34,211,238,.12);color:var(--cyan);border:1px solid rgba(34,211,238,.2);';
            badge.textContent = `当前：${tierNames[autoTier-1]}`;
        } else {
            badge.className = 'zone-manual-badge';
            badge.style.cssText = 'font-size:.55rem;padding:1px 6px;border-radius:8px;background:rgba(200,167,36,.15);color:var(--gold-l);border:1px solid rgba(200,167,36,.3);';
            badge.textContent = `已手动：${tierNames[parseInt(val,10)-1]}`;
        }
    }
    showToast(val ? `✅ 区间${zoneIndex+1}已手动设为${tierNames[parseInt(val,10)-1]}，已联动全局` : `✅ 区间${zoneIndex+1}已恢复自动预测，已联动全局`);
}
function renderWaveTables() {
    const el = document.getElementById("waveTableContainer");
    if(!el) return;
    const reds=[], blues=[], greens=[];
    for(let i=1;i<=49;i++) { const w=getWave(i); if(w==='红波') reds.push(i); else if(w==='蓝波') blues.push(i); else greens.push(i); }
    el.innerHTML = `<div class="wave-cols"><div class="wave-col"><div class="wave-col-ttl" style="color:var(--red);">🔴 红波 (${reds.length})</div><div class="wave-nms">${reds.map(n=>`<span class="num-ball nb-r">${n}</span>`).join("")}</div></div><div class="wave-col"><div class="wave-col-ttl" style="color:var(--blue);">🔵 蓝波 (${blues.length})</div><div class="wave-nms">${blues.map(n=>`<span class="num-ball nb-b">${n}</span>`).join("")}</div></div><div class="wave-col"><div class="wave-col-ttl" style="color:var(--green);">🟢 绿波 (${greens.length})</div><div class="wave-nms">${greens.map(n=>`<span class="num-ball nb-g">${n}</span>`).join("")}</div></div></div>`;
}
function renderZodiacGrid() {
    const el = document.getElementById("zodiacFullTable");
    if(!el) return;
    el.innerHTML = `<div class="zod-grid">${Object.keys(zodiacMapping).map(z=>`<div class="zod-item"><div class="zod-name">${z}</div><div class="zod-nms">${zodiacMapping[z].map(n=>{const w=getWave(n);const cls=w==='红波'?'nb-r':(w==='蓝波'?'nb-b':'nb-g');return `<span class="num-ball ${cls}" style="width:24px;height:24px;font-size:.58rem;">${n}</span>`;}).join("")}</div></div>`).join("")}</div>`;
}
async function refreshUI() {
    allRecords = await getAllRecords();
    if(allRecords.length) {
        const last = enrich(allRecords[allRecords.length-1]);
        document.getElementById("liveExp").textContent = last.expect;
        document.getElementById("latestDrawSpecial").textContent = last.specialNum;
        document.getElementById("latestDrawNums").textContent = getDisplayNums(last.openCode) || last.openCode;
    }
    const tbody = document.getElementById("historyTbody");
    const badge = document.getElementById("recCount");
    if(badge) badge.textContent = `(${allRecords.length}期)`;
    if(tbody) {
        const latest = [...allRecords].reverse().slice(0,50).map(r=>enrich(r));
        tbody.innerHTML = latest.map(r=>{ const dn=getDisplayNums(r.openCode); const wCls=r.wave==='红波'?'nb-r':(r.wave==='蓝波'?'nb-b':'nb-g'); const wpCls=r.wave==='红波'?'wp-r':(r.wave==='蓝波'?'wp-b':'wp-g'); return `<tr><td style="color:var(--text-muted);">${r.expect}</td><td style="color:var(--text-dim);font-size:.6rem;">${dn||'—'}</td><td><span class="num-ball ${wCls}">${r.specialNum}</span></td><td><span class="zod-pill">${r.zodiac}</span></td><td><span class="wave-pill ${wpCls}">${r.wave}</span></td></tr>`; }).join("");
    }
    renderWaveTables(); renderZodiacGrid();
    const all = allRecords.map(r=>enrich(r));
    initPiEnergy(all);
    renderProbHeatmap(all);
    if(!allRecords.length) return;
    const last10 = all.slice(-getAnalysisWindow());
    updateStatCards(last10, all);
    updateDashboardPredictions(last10, all);
    updateTrendCharts(last10);
    updateZoneCharts(last10);
    updateZoneQuantum(last10, all);
    updateHotMiss(all);
    updateAnalysis(last10, all);
    updateFourD(last10);
    updateGodView(last10, all);
    updateZoneSummary(last10);
    updateThreeInThreePrediction(last10, all);
    updateDashboardAIHighLow(all);
    updateZodiacPyramid(last10, all);
    setTimeout(()=>allCharts().forEach(c=>{try{c?.resize();}catch(e){}}),100);
}
// π能量系统
const PI_DIGITS = "14159265358979323846264338327950288419716939937510582097494459230781640628620899862803482534211706798214808651328230664709384460955058223172535940812848111745028410270193852110555964462294895493038196444590575168";
let piFreqChart, piWaveChart;
function initPiEnergy(all) { const today=new Date(); const y=today.getFullYear(), m=today.getMonth()+1, d=today.getDate(); document.getElementById("piDateInfo").textContent = `今日：${y}年${m}月${d}日 · 宇宙时间线 ${y} · π恒态矩阵激活`; const seed = ((y%100)*31 + m*7 + d*3 + all.length) % (PI_DIGITS.length-20); document.getElementById("piSeedVal").textContent = PI_DIGITS.substring(seed,seed+1)+PI_DIGITS.substring(seed+1,seed+3); document.getElementById("piSeedSub").textContent = `π[${seed}~${seed+9}]`; renderPiDigitGrid(seed); const piWindow = PI_DIGITS.substring(seed,seed+20); computePiEnergyNums(piWindow,seed,y,m,d,all); renderPiFreqChart(); renderPiWaveChart(all,seed); computePiHistResonance(all,seed); computePiEnhancedAnalysis(all,seed); }
function renderPiDigitGrid(activeSeed) { const el=document.getElementById("piDigitGrid"); if(!el) return; const digitWave={0:'g',1:'r',2:'r',3:'b',4:'b',5:'g',6:'g',7:'b',8:'r',9:'r'}; const html = PI_DIGITS.substring(0,50).split('').map((d,idx)=>{ const wClass=`pi-d-${digitWave[+d]}`; const isActive = idx>=activeSeed%50 && idx<(activeSeed%50)+5; return `<span class="pi-digit ${wClass}${isActive?' pi-d-active':''}" title="π第${idx+1}位: ${d}">${d}</span>`; }).join(''); el.innerHTML=html; }
function getPiEnergyFive(piWindow,seed,y,m,d,all) { 
    const piNums=[], usedNums=new Set(); 
    const dateEnergy = (y*3 + m*7 + d*13 + seed*2)%49; 
    // 历史共振能量：分析历史开奖与π数字的共振频率
    let histResonance = 0;
    if(all && all.length >= 5) {
        const piSet = new Set();
        for(let i=0;i<20;i++){ const d1=parseInt(piWindow[i]||'3'), d2=parseInt(piWindow[i+1]||'1'); piSet.add(((d1*5+d2*3+i)%49)+1); }
        const recent = all.slice(-20);
        let hits = 0;
        recent.forEach(r => { if(piSet.has(r.specialNum)) hits++; });
        histResonance = hits / recent.length;
    }
    // 波色能量分析
    const waveEnergy = {'红波':0,'蓝波':0,'绿波':0};
    if(all && all.length) { all.slice(-10).forEach(r => waveEnergy[r.wave]++); }
    const minWave = Object.entries(waveEnergy).sort((a,b)=>a[1]-b[1])[0][0];
    // 生肖能量
    const zodEnergy = {}; 
    if(all && all.length) { all.slice(-10).forEach(r => zodEnergy[r.zodiac]=(zodEnergy[r.zodiac]||0)+1); }
    const hotZod = Object.entries(zodEnergy).sort((a,b)=>b[1]-a[1]).slice(0,2).map(([z])=>z);
    for(let i=0;i<15 && piNums.length<5;i++){ 
        const d1=parseInt(piWindow[i]||'3'), d2=parseInt(piWindow[i+1]||'1'), d3=parseInt(piWindow[(i+2)%piWindow.length]||'4'); 
        let num=((d1*7+d2*5+d3*3+dateEnergy+i*11+seed*3)%49)+1; 
        if(!usedNums.has(num)){ piNums.push(num); usedNums.add(num); } 
        let num2=((d1*11+d2*7+i*13+seed*5+dateEnergy)%49)+1; 
        if(!usedNums.has(num2) && piNums.length<5){ piNums.push(num2); usedNums.add(num2); } 
    } 
    // 波色回补补充
    for(let n=1;n<=49 && piNums.length<5;n++) { if(getWave(n)===minWave && !usedNums.has(n)) { piNums.push(n); usedNums.add(n); } }
    // 生肖热度补充
    for(let n=1;n<=49 && piNums.length<5;n++) { if(hotZod.includes(getZodiac(n)) && !usedNums.has(n)) { piNums.push(n); usedNums.add(n); } }
    while(piNums.length<5){ const extra=((seed+piNums.length*17+dateEnergy)%49)+1; if(!usedNums.has(extra)){ piNums.push(extra); usedNums.add(extra); } else { piNums.push(((extra+3)%49)+1); break; } } 
    return { final5: piNums.slice(0,5), dateEnergy, histResonance, minWave, hotZod }; 
}
function computePiEnergyNums(piWindow,seed,y,m,d,all) { const el=document.getElementById("piEnergyNums"), calcEl=document.getElementById("piCalcSteps"); if(!el) return; const { final5, dateEnergy, histResonance, minWave, hotZod } = getPiEnergyFive(piWindow,seed,y,m,d,all); el.innerHTML=final5.map((n,idx)=>{ const w=getWave(n), cls=w==='红波'?'gb-r':(w==='蓝波'?'gb-b':'gb-g'), z=getZodiac(n); return `<div class="pi-e-ball-wrap"><div class="pi-e-ball ${cls}" style="animation-delay:${idx*.07}s;">${n}</div><div class="pi-e-ball-lbl">${z}</div></div>`; }).join(''); const piCopyBtn=document.getElementById("piEnergyCopyBtn"); if(piCopyBtn) piCopyBtn.dataset.nums=final5.join(', '); if(calcEl){ const piSlice=piWindow.substring(0,10).split('').join(' · '); const resonanceTxt = all && all.length>=5 ? `历史共振率：<strong style="color:var(--gold-l);">${(histResonance*100).toFixed(0)}%</strong> · 波色回补：<strong style="color:var(--cyan);">${minWave}</strong> · 热门生肖：<strong style="color:var(--purple);">${hotZod.join('、')||'--'}</strong><br>` : ''; calcEl.innerHTML=`<strong style="color:var(--purple);">π量子种子计算（增强版）：</strong><br>π[${seed}~${seed+9}] = ${piSlice}<br>日期能量值 = (${y}×3 + ${m}×7 + ${d}×13 + 种子×2) mod 49 = <strong style="color:var(--gold-l);">${dateEnergy}</strong><br>${resonanceTxt}七维映射公式：N = (π[i]×7 + π[i+1]×5 + π[i+2]×3 + 日期能量 + i×11 + 种子×3) mod 49 + 1<br>推荐号码：<strong style="color:var(--cyan);">${final5.join(' · ')}</strong>`; } }
function renderPiFreqChart() { const freq=new Array(10).fill(0); PI_DIGITS.substring(0,100).split('').forEach(d=>{if(!isNaN(d)) freq[+d]++;}); const container=document.getElementById("piFreqChart"); if(!container) return; if(!piFreqChart||piFreqChart.isDisposed()) piFreqChart=echarts.init(container); const colors=['#4ade80','#f87171','#f87171','#60a5fa','#60a5fa','#4ade80','#4ade80','#60a5fa','#f87171','#f87171']; darkOpts(piFreqChart,{ tooltip:{trigger:'axis',formatter:p=>`数字 ${p[0].axisValue}：出现 ${p[0].value} 次`}, xAxis:{type:'category',data:['0','1','2','3','4','5','6','7','8','9']}, yAxis:{name:'出现次数',nameTextStyle:{color:'rgba(221,226,240,.35)',fontSize:9}}, series:[{type:'bar',data:freq,itemStyle:{color:params=>colors[params.dataIndex],borderRadius:[5,5,0,0]}}] }); }
function renderPiWaveChart(all,seed) { let piWaveCount={'红波':0,'蓝波':0,'绿波':0}; for(let i=0;i<30;i++){ const d1=parseInt(PI_DIGITS[i]||'1'), d2=parseInt(PI_DIGITS[i+1]||'4'); const n=((d1*5+d2*3+i)%49)+1; piWaveCount[getWave(n)]++; } const container=document.getElementById("piWaveChart"); if(!container) return; if(!piWaveChart||piWaveChart.isDisposed()) piWaveChart=echarts.init(container); darkOpts(piWaveChart,{ tooltip:{trigger:'item',formatter:'{b}: {c} ({d}%)'}, legend:{bottom:0,textStyle:{color:'rgba(221,226,240,.6)',fontSize:10}}, series:[{ type:'pie', radius:['40%','70%'], data:[{value:piWaveCount['红波'],name:'红波能量',itemStyle:{color:'rgba(248,113,113,.7)'}},{value:piWaveCount['蓝波'],name:'蓝波能量',itemStyle:{color:'rgba(96,165,250,.7)'}},{value:piWaveCount['绿波'],name:'绿波能量',itemStyle:{color:'rgba(74,222,128,.7)'}}], label:{color:'rgba(221,226,240,.7)',fontSize:10} }] }); const maxWave=Object.entries(piWaveCount).sort((a,b)=>b[1]-a[1])[0][0]; const el=document.getElementById("piWaveAnalysis"); if(el) el.innerHTML=`🌊 π数字能量场中，<strong style="color:var(--gold-l);">${maxWave}</strong>能量最强（${piWaveCount[maxWave]}次）。今日π量子场与彩票波色场发生<strong>${maxWave}</strong>共振，${maxWave}号码群具有较高π能量激活度。`; }
function computePiHistResonance(all,seed) { const el=document.getElementById("piHistResonance"); if(!el) return; if(!all.length){ el.innerHTML = "📡 暂无开奖历史数据，请先在顶部「手动入录」添加开奖记录，π共振验证将自动生成。"; return; } const piNums=new Set(); for(let i=0;i<30;i++){ const d1=parseInt(PI_DIGITS[i%PI_DIGITS.length]||'1'), d2=parseInt(PI_DIGITS[(i+1)%PI_DIGITS.length]||'4'); const n=((d1*5+d2*3+i)%49)+1; piNums.add(n); } const recent20=all.slice(-20); const hits=recent20.filter(r=>piNums.has(r.specialNum)).length; const rate=(hits/recent20.length*100).toFixed(0); el.innerHTML=`📡 π共振验证（近20期）：π能量号码池覆盖历史特码 <strong style="color:var(--gold-l);">${hits}/20期</strong>，共振率 <strong style="color:var(--cyan);">${rate}%</strong>。<br>最近5期特码与π能量场：${recent20.slice(-5).map(r=>{const inPi=piNums.has(r.specialNum);return `<span style="color:${inPi?'var(--green)':'var(--text-muted)'}">${r.specialNum}${inPi?'✓':''}</span>`;}).join(' → ')}`; }
function computePiEnhancedAnalysis(all,seed) {
    // 增强π能量分析：多维度能量场评估
    const el = document.getElementById("piWaveAnalysis");
    if(!el || !all.length) return;
    const piNums=new Set(); 
    for(let i=0;i<50;i++){ const d1=parseInt(PI_DIGITS[i%PI_DIGITS.length]||'1'), d2=parseInt(PI_DIGITS[(i+1)%PI_DIGITS.length]||'4'), d3=parseInt(PI_DIGITS[(i+2)%PI_DIGITS.length]||'1'); const n=((d1*7+d2*5+d3*3+i*11+seed)%49)+1; piNums.add(n); }
    // 分析π能量场与历史数据的深度共振
    const recent30 = all.slice(-30);
    const waveHits = {'红波':0,'蓝波':0,'绿波':0};
    const zodHits = {};
    let totalHits = 0;
    recent30.forEach(r => {
        if(piNums.has(r.specialNum)) {
            totalHits++;
            waveHits[r.wave]++;
            zodHits[r.zodiac] = (zodHits[r.zodiac]||0)+1;
        }
    });
    const topZod = Object.entries(zodHits).sort((a,b)=>b[1]-a[1]).slice(0,3).map(([z,c])=>`${z}(${c})`).join('、');
    const maxWave = Object.entries(waveHits).sort((a,b)=>b[1]-a[1])[0][0];
    const piEnergyScore = (totalHits / recent30.length * 100).toFixed(0);
    el.innerHTML = `🌊 π恒态矩阵能量场分析：<strong style="color:var(--gold-l);">${maxWave}</strong>能量最强（π共振${waveHits[maxWave]}次）。<br>🌀 π能量场与彩票波色场发生<strong style="color:var(--cyan);">${maxWave}</strong>深度共振，${maxWave}号码群具有最高π能量激活度。<br>📊 近30期π能量共振率：<strong style="color:var(--purple);">${piEnergyScore}%</strong> · 高共振生肖：<strong style="color:var(--gold-l);">${topZod||'--'}</strong><br>⚛️ π恒态矩阵推演：下期能量交变点位于π能量场与历史遗漏的叠加区域，建议关注π能量高共振号码。`;
}
window.saveNote=function(key){ const inp=document.getElementById(`input_${key}`), ok=document.getElementById(`note_${key}`); if(inp?.value) localStorage.setItem(`ln_${key}`,inp.value); if(ok){ ok.textContent="✓ 已保存"; setTimeout(()=>ok.textContent="",1500); } };
function loadNotes(){ ['numNote'].forEach(key=>{ const saved=localStorage.getItem(`ln_${key}`); const inp=document.getElementById(`input_${key}`); if(saved && inp) inp.value=saved; }); }
const allCharts=()=>[numChart,zodiacChart,...zoneCharts,hotChart,missChart,piFreqChart,piWaveChart,zodiacPyramidChart].filter(c=>c&&!c.isDisposed());
document.querySelectorAll('.tab-btn').forEach(btn=>{ btn.addEventListener('click',()=>{ document.querySelectorAll('.tab-btn').forEach(b=>b.classList.remove('active')); document.querySelectorAll('.tab-panel').forEach(p=>p.classList.remove('active')); btn.classList.add('active'); const panel=document.getElementById(`tab-${btn.dataset.tab}`); if(panel) panel.classList.add('active'); setTimeout(()=>allCharts().forEach(c=>{try{c.resize();}catch(e){}}),80); }); });
window.addEventListener('resize',()=>{ clearTimeout(window._resizeTimer); window._resizeTimer=setTimeout(()=>{ allCharts().forEach(c=>{try{c.resize();}catch(e){}}); },200); });
window.toggleCard=function(el){ el.closest('.card, .robot-card').classList.toggle('collapsed'); setTimeout(()=>allCharts().forEach(c=>{try{c.resize();}catch(e){}}),220); };
window.toggleSegment=function(el){ el.closest('.segment').classList.toggle('collapsed'); };
// ============================================================
// 通用 UI：模态框 / 轻提示
// ============================================================
function showModal(innerHtml){ const overlay=document.getElementById("modalOverlay"), box=document.getElementById("modalBox"); if(!overlay||!box) return; box.innerHTML=innerHtml; overlay.classList.add("active"); }
function closeModal(){ const overlay=document.getElementById("modalOverlay"); if(overlay) overlay.classList.remove("active"); }
window.closeModal = closeModal;
function showToast(msg){ const t=document.getElementById("toast"); if(!t) return; t.textContent=msg; t.classList.add("show"); clearTimeout(window._toastTimer); window._toastTimer=setTimeout(()=>t.classList.remove("show"),2800); }

// ============================================================
// 清空数据（自定义确认框，替代原生 prompt/alert，修复无法弹出问题）
// ============================================================
function confirmClearAll(){
    const cnt = allRecords.length;
    showModal(`
        <div class="modal-title"><span>⚠️ 确认清空全部数据</span><span class="modal-close" onclick="closeModal()"><i class="fas fa-times"></i></span></div>
        <div class="modal-desc" style="font-size:.75rem;color:var(--text);">
            此操作将永久删除本机保存的全部 <strong style="color:var(--red);">${cnt}</strong> 期开奖记录、AI自学习权重与统计数据，且<strong style="color:var(--red);">无法恢复</strong>。
            <br><br>建议先在「设置 → 导出备份」保存一份 JSON 文件。
            <br><br>确定要继续清空吗？
        </div>
        <div class="modal-actions">
            <button class="btn" onclick="closeModal()">取消</button>
            <button class="btn btn-danger" onclick="doClearAll()">确认清空</button>
        </div>
    `);
}
async function doClearAll(){
    await deleteAllRecords();
    try{ localStorage.removeItem(PRED_SNAPSHOT_KEY); localStorage.removeItem(PRED_STATS_KEY); }catch(e){}
    await refreshUI();
    closeModal();
    showToast("✅ 已清空全部本地数据");
}

// ============================================================
// 本地数据备份 · 导入 / 导出（纯本地，无外部接口）
// ============================================================
function exportBackup(){
    const data = { app:"澳门智慧数据台", version:1, exportedAt:new Date().toISOString(), records:allRecords, weights:getWeights(), stats:getPredStats(), autoLearn:isAutoLearnEnabled() };
    const blob = new Blob([JSON.stringify(data,null,2)], {type:'application/json'});
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url; a.download = `macau_lottery_backup_${new Date().toISOString().slice(0,10)}.json`;
    document.body.appendChild(a); a.click(); document.body.removeChild(a);
    setTimeout(()=>URL.revokeObjectURL(url), 1000);
    showToast("✅ 备份文件已导出");
}
async function importBackup(file){
    if(!file) return;
    try{
        const text = await file.text();
        const data = JSON.parse(text);
        const records = Array.isArray(data) ? data : data.records;
        if(!Array.isArray(records)) throw new Error("文件格式不正确");
        let count = 0;
        for(const r of records){
            const sp = Number(r && r.specialNum);
            if(r && r.expect!=null && sp>=1 && sp<=49){
                await saveRecord({ expect:String(r.expect), openCode:r.openCode||String(sp), specialNum:sp, timestamp:r.timestamp||Date.now() });
                count++;
            }
        }
        if(data && data.weights) saveWeights(data.weights);
        if(data && data.stats) savePredStats(data.stats);
        if(data && typeof data.autoLearn==='boolean') setAutoLearnEnabled(data.autoLearn);
        await refreshUI();
        showToast(`✅ 已导入 ${count} 期记录`);
        closeModal();
    }catch(e){
        showToast("❌ 导入失败：" + e.message);
    }
}

// ============================================================
// 设置面板
// ============================================================
const FACTOR_LABELS = { freq:'热号频率', miss:'遗漏值', zodiac:'生肖共振', wave:'波色均衡', zone:'区间共振', pi:'π能量', fib:'斐波那契', trend:'走势学习' };
function openSettings(){
    const weights = getWeights();
    const stats = getPredStats();
    const dashStats = getDashStats();
    const autoLearn = isAutoLearnEnabled();
    const cfg = getSyncConfig();
    const curWindow = getAnalysisWindow();
    const all = allRecords.map(r=>enrich(r));
    const trend = analyzeHistoricalTrends(all);
    const accTxt = stats.total>0 ? `${stats.total} 期 · 命中率 ${(stats.hit15/stats.total*100).toFixed(0)}%` : '暂无样本（数据积累中）';
    const piAccTxt = dashStats.pi.total>0 ? `${dashStats.pi.total} 期 · 命中率 ${(dashStats.pi.hit/dashStats.pi.total*100).toFixed(0)}%` : '暂无样本';
    const zoneAccTxt = dashStats.zone.total>0 ? `${dashStats.zone.total} 期 · 命中率 ${(dashStats.zone.hit/dashStats.zone.total*100).toFixed(0)}%` : '暂无样本';
    showModal(`
        <div class="modal-title"><span>⚙ 系统设置</span><span class="modal-close" onclick="closeModal()"><i class="fas fa-times"></i></span></div>
        <div class="modal-section">
            <div class="modal-section-title">📦 数据与本地存储</div>
            <div class="modal-row"><span>当前已存储期数</span><strong style="color:var(--gold-l);">${allRecords.length} 期</strong></div>
            <div class="modal-row"><span>存储方式</span><span style="color:var(--green);text-align:right;">IndexedDB（自动回退 localStorage）</span></div>
            <div class="modal-row" style="gap:8px;">
                <button class="btn" onclick="exportBackup()"><i class="fas fa-download"></i> 导出备份(JSON)</button>
                <label class="btn" style="cursor:pointer;margin:0;">
                    <i class="fas fa-upload"></i> 导入备份
                    <input type="file" accept="application/json" style="display:none;" onchange="importBackup(this.files[0])">
                </label>
                <button class="btn btn-danger" onclick="confirmClearAll()"><i class="fas fa-trash"></i> 清空全部数据</button>
            </div>
            <div class="modal-desc">所有开奖数据完整保存于本机浏览器（IndexedDB / localStorage）。导出/导入用于跨设备迁移或备份；清空操作不可恢复。</div>
        </div>
        <div class="modal-section">
            <div class="modal-section-title">🔗 官方开奖接口同步</div>
            <div class="modal-row" style="flex-direction:column;align-items:stretch;gap:6px;">
                <span>接口地址（GET，返回JSON）</span>
                <input type="text" id="syncUrlInput" value="${cfg.url.replace(/"/g,'&quot;')}" placeholder="https://..." style="width:100%;background:var(--surface);border:1px solid var(--border2);border-radius:6px;padding:7px 9px;color:var(--text);font-size:.66rem;font-family:'JetBrains Mono',monospace;box-sizing:border-box;">
            </div>
            <div class="modal-row">
                <span>开启自动同步</span>
                <label class="switch"><input type="checkbox" id="autoSyncToggle" ${cfg.autoSync?'checked':''}><span class="slider"></span></label>
            </div>
            <div class="modal-row">
                <span>同步间隔</span>
                <select id="syncIntervalSelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    ${[5,10,15,30,60].map(v=>`<option value="${v}" ${cfg.intervalMin===v?'selected':''}>每 ${v} 分钟</option>`).join('')}
                </select>
            </div>
            <div class="modal-row"><span>上次同步</span><span style="color:var(--text-muted);text-align:right;">${cfg.lastSyncAt||'尚未同步'}${cfg.lastSyncMsg?`<br>${cfg.lastSyncMsg}`:''}</span></div>
            <div class="modal-actions">
                <button class="btn" onclick="saveSyncSettingsFromUI()">保存设置</button>
                <button class="btn" onclick="syncFromAPI(true)"><i class="fas fa-sync"></i> 立即同步</button>
            </div>
            <div class="modal-desc">同步到的开奖记录会写入本地数据库，并与手动入录一样立即联动应用到全部走势分析、区间预测、π能量预测与AI概率分级。若浏览器因跨域限制（CORS）同步失败，请确认接口允许跨域访问。</div>
        </div>
        <div class="modal-section">
            <div class="modal-section-title">🎛️ 全局分析参数</div>
            <div class="modal-row">
                <span>分析窗口（近N期）</span>
                <select id="analysisWindowSelect" onchange="updateAnalysisWindow(this.value)" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    ${[5,8,10,12,15,20,30].map(v=>`<option value="${v}" ${curWindow===v?'selected':''}>近${v}期</option>`).join('')}
                </select>
            </div>
            <div class="modal-desc">此参数将全局应用于走势分析、区间量子预测、生肖/波色统计及AI七维因子等所有"近N期"相关计算，修改后立即在全站生效，可用于提升预测分析的作业效率与精细度。</div>
        </div>
        <div class="modal-section">
            <div class="modal-section-title">🔮 π 数能量预测 · 计算等级与能力设置</div>
            <div class="modal-row">
                <span>π能量计算等级</span>
                <select id="piLevelSelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="1">初级预测</option>
                    <option value="2">中级预测</option>
                    <option value="3">高级预测</option>
                    <option value="4">专家预测</option>
                    <option value="5">大师预测</option>
                    <option value="6" selected>神级预测</option>
                </select>
            </div>
            <div class="modal-row">
                <span>π能量学习能力</span>
                <select id="piLearnAbilitySelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="low">低阶学习</option>
                    <option value="medium">中阶学习</option>
                    <option value="high">高阶学习</option>
                    <option value="super" selected>超阶学习</option>
                </select>
            </div>
            <div class="modal-row">
                <span>π能量分析能力</span>
                <select id="piAnalysisAbilitySelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="basic">基础分析</option>
                    <option value="advanced">进阶分析</option>
                    <option value="expert">专家分析</option>
                    <option value="god" selected>神级分析</option>
                </select>
            </div>
            <div class="modal-row">
                <span>π能量预测能力</span>
                <select id="piPredAbilitySelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="basic">基础预测</option>
                    <option value="advanced">进阶预测</option>
                    <option value="expert">专家预测</option>
                    <option value="god" selected>神级预测</option>
                </select>
            </div>
            <div class="modal-row">
                <span>π能量分析预测能力</span>
                <select id="piAnalysisPredSelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="basic">基础分析预测</option>
                    <option value="advanced">进阶分析预测</option>
                    <option value="expert">专家分析预测</option>
                    <option value="god" selected>神级分析预测</option>
                </select>
            </div>
            <div class="modal-desc">π数能量预测的计算等级与能力设置将直接影响π量子场分析、能量映射公式及预测精度。等级越高，计算复杂度与预测精准度同步提升。最高等级为「神级预测」。所有设置保存后联动全局。</div>
        </div>
        <div class="modal-section">
            <div class="modal-section-title">🧠 超级AI预测引擎 · 自学习能力</div>
            <div class="modal-row">
                <span>开启超级AI自学习权重调整</span>
                <label class="switch"><input type="checkbox" id="autoLearnToggle" ${autoLearn?'checked':''} onchange="setAutoLearnEnabled(this.checked)"><span class="slider"></span></label>
            </div>
            <div class="modal-desc">超级AI引擎每新增 / 修改一期开奖记录（手动入录或接口同步）后，系统会用该真实结果覆盖上一轮的预测分析，并自动微调下方七维因子权重，使预测逐步贴合本地历史走势。此设置应用到全局所有预测模块。所有设置保存后联动全局。</div>
            <div class="modal-row" style="margin-top:8px;">
                <span>AI自学习强度</span>
                <select id="aiLearnStrengthSelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="low">低强度（保守学习）</option>
                    <option value="medium">中强度（均衡学习）</option>
                    <option value="high" selected>高强度（激进学习）</option>
                </select>
            </div>
            <div class="modal-row">
                <span>AI预测模式</span>
                <select id="aiPredModeSelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="balanced">均衡模式</option>
                    <option value="trend">趋势优先</option>
                    <option value="reverse" selected>反转优先</option>
                </select>
            </div>
            <div class="modal-row">
                <span>学习预测能力</span>
                <select id="learnPredAbilitySelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="basic">基础预测</option>
                    <option value="advanced">进阶预测</option>
                    <option value="expert">专家预测</option>
                    <option value="master" selected>大师预测</option>
                </select>
            </div>
            <div class="modal-row">
                <span>AI学习能力</span>
                <select id="aiLearnAbilitySelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="basic">基础学习</option>
                    <option value="advanced">进阶学习</option>
                    <option value="expert">专家学习</option>
                    <option value="master">大师学习</option>
                    <option value="god" selected>神级学习</option>
                </select>
            </div>
            <div class="modal-row">
                <span>AI分析预测能力</span>
                <select id="aiAnalysisPredSelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="basic">基础分析预测</option>
                    <option value="advanced">进阶分析预测</option>
                    <option value="expert">专家分析预测</option>
                    <option value="master">大师分析预测</option>
                    <option value="god" selected>神级分析预测</option>
                </select>
            </div>
            <div class="modal-row">
                <span>顶级学习进度</span>
                <select id="topLearnProgressSelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="stage1">第一阶段 · 数据积累</option>
                    <option value="stage2">第二阶段 · 模式识别</option>
                    <option value="stage3">第三阶段 · 深度优化</option>
                    <option value="stage4">第四阶段 · 顶级推演</option>
                    <option value="stage5" selected>第五阶段 · 神级顿悟</option>
                </select>
            </div>
            <div class="modal-row">
                <span>开奖惯性学习</span>
                <label class="switch"><input type="checkbox" id="inertiaLearnToggle" checked><span class="slider"></span></label>
            </div>
            <div class="modal-row">
                <span>趋势形态学习</span>
                <label class="switch"><input type="checkbox" id="trendShapeLearnToggle" checked><span class="slider"></span></label>
            </div>
            <div class="modal-row">
                <span>概率分布学习</span>
                <label class="switch"><input type="checkbox" id="probDistLearnToggle" checked><span class="slider"></span></label>
            </div>
            <div class="modal-row">
                <span>波色形态学习</span>
                <label class="switch"><input type="checkbox" id="waveShapeLearnToggle" checked><span class="slider"></span></label>
            </div>
            <div class="modal-row">
                <span>圆周率实时变化学习</span>
                <label class="switch"><input type="checkbox" id="piChangeLearnToggle" checked><span class="slider"></span></label>
            </div>
            <div class="modal-row">
                <span>规则引擎学习</span>
                <label class="switch"><input type="checkbox" id="ruleEngineLearnToggle" checked><span class="slider"></span></label>
            </div>
            <div class="modal-row">
                <span>增强稳定性和流畅性</span>
                <label class="switch"><input type="checkbox" id="stabilityToggle" checked><span class="slider"></span></label>
            </div>
            <div class="modal-row">
                <span>全局深度学习引擎</span>
                <label class="switch"><input type="checkbox" id="globalDeepLearnToggle" checked><span class="slider"></span></label>
            </div>
            <div class="modal-row">
                <span>全局预测增强模式</span>
                <select id="globalPredEnhanceSelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="basic">基础预测</option>
                    <option value="advanced">进阶预测</option>
                    <option value="expert">专家预测</option>
                    <option value="master" selected>大师预测</option>
                    <option value="god">神级预测</option>
                </select>
            </div>
            <div class="modal-row">
                <span>全局分析增强模式</span>
                <select id="globalAnalysisEnhanceSelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="basic">基础分析</option>
                    <option value="advanced">进阶分析</option>
                    <option value="expert">专家分析</option>
                    <option value="master" selected>大师分析</option>
                    <option value="god">神级分析</option>
                </select>
            </div>
            <div class="modal-row">
                <span>全局学习增强模式</span>
                <select id="globalLearnEnhanceSelect" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    <option value="basic">基础学习</option>
                    <option value="advanced">进阶学习</option>
                    <option value="expert">专家学习</option>
                    <option value="master" selected>大师学习</option>
                    <option value="god">神级学习</option>
                </select>
            </div>
            <div class="modal-row">
                <span>多维度共振分析</span>
                <label class="switch"><input type="checkbox" id="multiResonanceToggle" checked><span class="slider"></span></label>
            </div>
            <div class="modal-row">
                <span>量子纠缠预测模型</span>
                <label class="switch"><input type="checkbox" id="quantumEntangleToggle" checked><span class="slider"></span></label>
            </div>
            <div style="margin-top:10px;">
                ${FACTOR_KEYS.map(k=>`<div class="weight-bar-row"><span class="wlabel">${FACTOR_LABELS[k]}</span><div class="weight-bar-track"><div class="weight-bar-fill" style="width:${(weights[k]*100).toFixed(1)}%;"></div></div><span class="wval">${(weights[k]*100).toFixed(1)}%</span></div>`).join('')}
            </div>
            <div class="modal-row" style="margin-top:8px;"><span>1-49概率分级 · 前15强命中率</span><strong style="color:var(--cyan);">${accTxt}</strong></div>
            <div class="modal-row"><span>π能量预测特码命中率</span><strong style="color:var(--gold-l);">${piAccTxt}</strong></div>
            <div class="modal-row"><span>区间重码预测命中率</span><strong style="color:var(--cyan);">${zoneAccTxt}</strong></div>
            <div class="modal-actions"><button class="btn" onclick="resetWeights()">重置学习权重</button></div>
        </div>
        <div class="modal-section">
            <div class="modal-section-title">📊 历史走势学习报告</div>
            ${trend ? `
            <div class="modal-row"><span>动量延续率 / 反转率</span><strong>${(trend.contRate*100).toFixed(0)}% / ${(trend.revRate*100).toFixed(0)}%</strong></div>
            <div class="modal-row"><span>波色切换频率</span><strong>${(trend.waveSwitchRate*100).toFixed(0)}%</strong></div>
            <div class="modal-row"><span>奇偶切换频率</span><strong>${(trend.parSwitchRate*100).toFixed(0)}%</strong></div>
            <div class="modal-row"><span>大小切换频率（25为界）</span><strong>${(trend.sizeSwitchRate*100).toFixed(0)}%</strong></div>
            <div class="modal-row"><span>生肖平均重复间隔</span><strong>${trend.avgZodiacGap.toFixed(1)} 期</strong></div>
            <div class="modal-row"><span>近20期平均波动步长</span><strong>${trend.avgStep.toFixed(1)}</strong></div>
            <div class="modal-desc">系统基于 ${trend.sampleSize} 期本地历史数据自动研究号码变化规律：当前历史整体呈<strong style="color:var(--gold-l);">${trend.contRate>=0.5?'"延续型"走势（趋势倾向于沿用相同方向）':'"反转型"走势（趋势倾向于反向修正）'}</strong>。该规律已作为"走势学习"因子纳入AI七维评分与下期预测，每新增一期数据将自动重新研究并更新。</div>
            ` : `<div class="modal-desc">数据量不足（建议至少5期），积累更多开奖记录后将自动生成走势学习报告。</div>`}
        </div>
        <div class="modal-section">
            <div class="modal-section-title">ℹ️ 关于本系统</div>
            <div class="modal-desc">澳门智慧数据台 · 旗舰版<br>所有走势分析、AI预测、π数能量预测及1-49号码概率分级均为基于本地历史数据的统计娱乐功能，不构成任何投注建议，请理性对待。</div>
        </div>
        <div class="modal-section" style="border:2px solid var(--gold);border-radius:10px;padding:16px;background:linear-gradient(145deg, rgba(12,18,38,.98), rgba(18,12,4,.96));">
            <div class="modal-section-title" style="color:var(--gold-l);font-size:1rem;">💾 确认保存所有设置</div>
            <div class="modal-desc">点击下方「确认保存」按钮后，所有设置将立刻永久性生效，并应用到全局所有预测模块、走势分析和AI计算中。</div>
            <div class="modal-actions" style="margin-top:12px;">
                <button class="btn" style="background:linear-gradient(90deg, var(--gold), var(--gold-l));color:#0a0e1a;font-weight:700;padding:10px 28px;font-size:.8rem;" onclick="confirmSaveAllSettings()"><i class="fas fa-save"></i> 确认保存</button>
            </div>
        </div>
    `);
}
function saveSyncSettingsFromUI(){
    const cfg=getSyncConfig();
    const urlInp=document.getElementById("syncUrlInput");
    const autoInp=document.getElementById("autoSyncToggle");
    const intervalInp=document.getElementById("syncIntervalSelect");
    if(urlInp) cfg.url=urlInp.value.trim();
    if(autoInp) cfg.autoSync=autoInp.checked;
    if(intervalInp) cfg.intervalMin=parseInt(intervalInp.value)||10;
    saveSyncConfig(cfg);
    setupAutoSync();
    showToast("✅ 同步设置已保存");
}
function updateAnalysisWindow(v){
    setAnalysisWindow(parseInt(v));
    refreshUI();
    showToast(`✅ 全局分析窗口已设为近${v}期，已应用到全站分析与预测`);
}
function resetWeights(){
    saveWeights({...DEFAULT_WEIGHTS});
    try{ localStorage.removeItem(PRED_SNAPSHOT_KEY); localStorage.removeItem(PRED_STATS_KEY); }catch(e){}
    showToast("✅ 已重置AI学习权重");
    openSettings();
}

// ============================================================
// AI 概率分级预测 · 自学习引擎（七维因子，纯本地计算）
// ============================================================
const PRED_WEIGHTS_KEY = "macau_pred_weights_v1";
const PRED_SNAPSHOT_KEY = "macau_pred_snapshot_v1";
const PRED_STATS_KEY = "macau_pred_stats_v1";
const AUTOLEARN_KEY = "macau_autolearn_v1";
const FACTOR_KEYS = ["freq","miss","zodiac","wave","zone","pi","fib","trend"];
const DEFAULT_WEIGHTS = { freq:1/8, miss:1/8, zodiac:1/8, wave:1/8, zone:1/8, pi:1/8, fib:1/8, trend:1/8 };
function getWeights(){ try{ const s=localStorage.getItem(PRED_WEIGHTS_KEY); if(s){ const w=JSON.parse(s); FACTOR_KEYS.forEach(k=>{ if(typeof w[k]!=='number'||isNaN(w[k])) w[k]=DEFAULT_WEIGHTS[k]; }); return w; } }catch(e){} return {...DEFAULT_WEIGHTS}; }
function saveWeights(w){ try{ localStorage.setItem(PRED_WEIGHTS_KEY, JSON.stringify(w)); }catch(e){} }
function getPredStats(){ try{ const s=localStorage.getItem(PRED_STATS_KEY); if(s) return JSON.parse(s); }catch(e){} return { total:0, hit15:0 }; }
function savePredStats(s){ try{ localStorage.setItem(PRED_STATS_KEY, JSON.stringify(s)); }catch(e){} }
function isAutoLearnEnabled(){ try{ return localStorage.getItem(AUTOLEARN_KEY) !== "0"; }catch(e){ return true; } }
function setAutoLearnEnabled(v){ try{ localStorage.setItem(AUTOLEARN_KEY, v?"1":"0"); }catch(e){} }

// ============================================================
// 历史走势 · 自学习分析研究
// ============================================================
function analyzeHistoricalTrends(all){
    if(!all || all.length<5) return null;
    const specials = all.map(r=>r.specialNum);
    // 1. 连续动量：相邻两次"涨跌方向"延续 or 反转
    let cont=0, rev=0;
    for(let i=2;i<specials.length;i++){
        const d1=specials[i-1]-specials[i-2], d2=specials[i]-specials[i-1];
        if(d1===0||d2===0) continue;
        if(Math.sign(d1)===Math.sign(d2)) cont++; else rev++;
    }
    const totalDir = cont+rev;
    const contRate = totalDir>0 ? cont/totalDir : 0.5;
    // 2. 波色切换频率
    let waveSwitch=0;
    for(let i=1;i<all.length;i++){ if(all[i].wave!==all[i-1].wave) waveSwitch++; }
    const waveSwitchRate = all.length>1 ? waveSwitch/(all.length-1) : 0;
    // 3. 生肖重复平均间隔（期）
    const zodiacGaps=[]; const lastSeenZ={};
    all.forEach((r,i)=>{ if(lastSeenZ[r.zodiac]!=null) zodiacGaps.push(i-lastSeenZ[r.zodiac]); lastSeenZ[r.zodiac]=i; });
    const avgZodiacGap = zodiacGaps.length ? (zodiacGaps.reduce((a,b)=>a+b,0)/zodiacGaps.length) : 0;
    // 4. 奇偶切换频率
    let parSwitch=0;
    for(let i=1;i<specials.length;i++){ if((specials[i]%2)!==(specials[i-1]%2)) parSwitch++; }
    const parSwitchRate = specials.length>1 ? parSwitch/(specials.length-1) : 0;
    // 5. 大小切换频率（>=25为大）
    let sizeSwitch=0;
    for(let i=1;i<specials.length;i++){ if((specials[i]>=25)!==(specials[i-1]>=25)) sizeSwitch++; }
    const sizeSwitchRate = specials.length>1 ? sizeSwitch/(specials.length-1) : 0;
    // 6. 平均步长（相邻特码差值绝对值，近20期）
    const recentDiffs=[];
    for(let i=Math.max(1,all.length-20);i<all.length;i++) recentDiffs.push(Math.abs(specials[i]-specials[i-1]));
    const avgStep = recentDiffs.length ? recentDiffs.reduce((a,b)=>a+b,0)/recentDiffs.length : 12;
    return { contRate, revRate:1-contRate, waveSwitchRate, avgZodiacGap, parSwitchRate, sizeSwitchRate, avgStep, sampleSize: all.length };
}
// 计算七维因子原始分（0~1）
function computeFactorScores(all){
    const factors={}; FACTOR_KEYS.forEach(k=>factors[k]={});
    const last10 = all.slice(-getAnalysisWindow());
    // 1. 热号频率（近50期出现次数）
    const freqCount=new Array(50).fill(0);
    all.slice(-50).forEach(r=>{ if(r.specialNum>=1&&r.specialNum<=49) freqCount[r.specialNum]++; });
    const maxFreq=Math.max(1,...freqCount.slice(1));
    // 2. 遗漏值（距上次出现的期数）
    const missCount=new Array(50).fill(all.length);
    for(let n=1;n<=49;n++){ for(let i=all.length-1;i>=0;i--){ if(all[i].specialNum===n){ missCount[n]=all.length-1-i; break; } } }
    const maxMiss=Math.max(1,...missCount.slice(1));
    // 3. 生肖共振（近10期生肖热度）
    const zodCount={}; last10.forEach(r=>zodCount[r.zodiac]=(zodCount[r.zodiac]||0)+1);
    // 4. 波色均衡（近10期最少波色优先回补）
    const waveCount={'红波':0,'蓝波':0,'绿波':0}; last10.forEach(r=>waveCount[r.wave]++);
    const minWaveCount=Math.min(...Object.values(waveCount));
    const maxWaveCount=Math.max(1,...Object.values(waveCount));
    // 5. 区间共振（六个区间下一档预测池命中次数）
    const zoneFreq={};
    if(last10.length>=1){
        for(let i=0;i<6;i++){ try{ const {nums}=computeZoneQuantumNumsEnhanced(i,last10,all); nums.forEach(n=>{ zoneFreq[n]=(zoneFreq[n]||0)+1; }); }catch(e){} }
    }
    // 6. π能量号码池
    const piNums=new Set();
    for(let i=0;i<30;i++){ const d1=parseInt(PI_DIGITS[i%PI_DIGITS.length]||'1'), d2=parseInt(PI_DIGITS[(i+1)%PI_DIGITS.length]||'4'); const n=((d1*5+d2*3+i)%49)+1; piNums.add(n); }
    // 7. 斐波那契投影
    const fibSet=new Set();
    if(last10.length>=3){
        const specials=last10.map(r=>r.specialNum);
        const range=Math.max(...specials)-Math.min(...specials);
        [0.236,0.382,0.5,0.618,0.786].forEach(f=>{ const v=Math.round(Math.min(...specials)+range*f); if(v>=1&&v<=49) fibSet.add(v); });
    }
    for(let n=1;n<=49;n++){
        factors.freq[n] = freqCount[n]/maxFreq;
        factors.miss[n] = missCount[n]/maxMiss;
        const z=getZodiac(n); factors.zodiac[n] = Math.min((zodCount[z]||0)/3, 1);
        const w=getWave(n); factors.wave[n] = maxWaveCount>minWaveCount ? (maxWaveCount-waveCount[w])/(maxWaveCount-minWaveCount) : 0.5;
        factors.zone[n] = Math.min((zoneFreq[n]||0)/4, 1);
        factors.pi[n] = piNums.has(n) ? 1 : 0;
        let fibScore=0; fibSet.forEach(fv=>{ const dist=Math.abs(n-fv); if(dist===0) fibScore=Math.max(fibScore,1); else if(dist<=2) fibScore=Math.max(fibScore,0.5); });
        factors.fib[n] = fibScore;
    }
    // 8. 走势学习因子：依据历史"延续/反转"规律推算下期号码的预期落点
    const trendInfo = analyzeHistoricalTrends(all);
    let expectedNext = 25;
    if(trendInfo && all.length>=2){
        const lastNum = all[all.length-1].specialNum;
        const lastDiff = all[all.length-1].specialNum - all[all.length-2].specialNum;
        let dir = 0;
        if(lastDiff!==0) dir = (trendInfo.contRate>=0.5) ? Math.sign(lastDiff) : -Math.sign(lastDiff);
        const step = Math.max(1, Math.round(trendInfo.avgStep));
        expectedNext = ((lastNum-1 + dir*step) % 49 + 49) % 49 + 1;
    } else if(all.length>=1){
        expectedNext = all[all.length-1].specialNum;
    }
    for(let n=1;n<=49;n++){
        let dist = Math.abs(n-expectedNext); dist = Math.min(dist, 49-dist);
        factors.trend[n] = Math.max(0, 1 - dist/24);
    }
    return factors;
}
function computeNumberScores(all, weights){
    const factors=computeFactorScores(all);
    const scores={};
    for(let n=1;n<=49;n++){ let s=0; FACTOR_KEYS.forEach(k=> s += (weights[k]||0)*(factors[k][n]||0)); scores[n]=s; }
    return { scores, factors };
}
function scoresToPercent(scores){
    const vals=Object.values(scores); const min=Math.min(...vals), max=Math.max(...vals);
    const pct={};
    for(let n=1;n<=49;n++) pct[n] = (max>min) ? Math.round((scores[n]-min)/(max-min)*100) : 50;
    return pct;
}
// 自学习 + 计算最新预测；返回 {pct, ranking}
function runLearningAndPredict(all){
    if(isAutoLearnEnabled()){
        try{
            const snapRaw=localStorage.getItem(PRED_SNAPSHOT_KEY);
            if(snapRaw && all.length>=1){
                const snap=JSON.parse(snapRaw);
                if(snap && snap.basedOnCount===all.length-1 && Array.isArray(snap.ranking)){
                    const actual=all[all.length-1].specialNum;
                    const rank=snap.ranking.indexOf(actual)+1;
                    const stats=getPredStats();
                    stats.total=(stats.total||0)+1;
                    const hit = rank>0 && rank<=15;
                    if(hit) stats.hit15=(stats.hit15||0)+1;
                    savePredStats(stats);
                    const w=getWeights();
                    const delta=0.012;
                    FACTOR_KEYS.forEach(k=>{
                        const fScore = (snap.factors && snap.factors[k] && typeof snap.factors[k][actual]==='number') ? snap.factors[k][actual] : 0.5;
                        const adj = (fScore-0.5)*delta*(hit?1:-1);
                        w[k] = Math.max(0.03, Math.min(0.45, w[k]+adj));
                    });
                    const sum=FACTOR_KEYS.reduce((a,k)=>a+w[k],0);
                    FACTOR_KEYS.forEach(k=> w[k]=w[k]/sum);
                    saveWeights(w);
                }
            }
        }catch(e){ console.warn("自学习引擎异常：",e); }
    }
    const weights=getWeights();
    const {scores, factors}=computeNumberScores(all, weights);
    const pct=scoresToPercent(scores);
    const ranking=Object.entries(scores).sort((a,b)=>b[1]-a[1]).map(([n])=>+n);
    try{ localStorage.setItem(PRED_SNAPSHOT_KEY, JSON.stringify({ basedOnCount: all.length, forExpect: nextExpect(), ranking, factors })); }catch(e){}
    return { pct, ranking, weights };
}
function renderProbHeatmap(all){
    const grid=document.getElementById("probHeatmapGrid");
    const summary=document.getElementById("probSummary");
    if(!grid||!summary) return;
    if(all.length<3){
        let html=''; for(let n=1;n<=49;n++) html+=`<div class="prob-cell prob-tier-4"><div class="pc-num">${n}</div><div class="pc-pct">--</div></div>`;
        grid.innerHTML=html;
        summary.innerHTML='📊 数据量不足（建议至少积累3期开奖记录），AI概率分级预测将在数据积累后自动启用并持续自学习。';
        return;
    }
    const {pct, ranking}=runLearningAndPredict(all);
    const tier=p=>p>=85?1:p>=65?2:p>=40?3:p>=15?4:5;
    let html='';
    for(let n=1;n<=49;n++) html+=`<div class="prob-cell prob-tier-${tier(pct[n])}" title="第${n}号 · 综合概率评分 ${pct[n]}%"><div class="pc-num">${n}</div><div class="pc-pct">${pct[n]}%</div></div>`;
    grid.innerHTML=html;
    const top=ranking.slice(0,6), bottom=ranking.slice(-6).reverse();
    const stats=getPredStats();
    const accTxt = stats.total>0 ? `近${stats.total}期学习样本 · 前15强命中率 ${(stats.hit15/stats.total*100).toFixed(0)}%` : 'AI正在积累学习样本';
    summary.innerHTML = `🎯 下期高能量号码：${top.map(n=>`<strong style="color:var(--gold-l);">${n}</strong>(${pct[n]}%)`).join('、')}<br>🧊 下期低能量号码：${bottom.map(n=>`${n}(${pct[n]}%)`).join('、')}<br>🧠 ${accTxt} · 自学习权重${isAutoLearnEnabled()?'已开启':'已关闭'}（可在「设置」中调整）`;
}

// ============================================================
// π 数能量预测增强 · AI优选下期特码
// ============================================================
function computePiPrediction(all){
    const today=new Date(); const y=today.getFullYear(), m=today.getMonth()+1, d=today.getDate();
    const seed = ((y%100)*31 + m*7 + d*3 + (all?all.length:0)) % (PI_DIGITS.length-20);
    const piWindow = PI_DIGITS.substring(seed,seed+20);
    const { final5, histResonance, minWave, hotZod } = getPiEnergyFive(piWindow, seed, y, m, d, all);
    if(!all || all.length<3) return { pick: final5[0], final5, pct:null, histResonance, minWave, hotZod };
    const weights = getWeights();
    const { scores } = computeNumberScores(all, weights);
    const pct = scoresToPercent(scores);
    let best=final5[0], bestScore=-Infinity;
    final5.forEach(n=>{ 
        let s = scores[n];
        if(getWave(n)===minWave) s += 0.15;
        if(hotZod.includes(getZodiac(n))) s += 0.1;
        if(s>bestScore){ bestScore=s; best=n; } 
    });
    return { pick: best, final5, pct, histResonance, minWave, hotZod };
}

// ============================================================
// 全局分析窗口设置（应用于全站"近N期"分析参数）
// ============================================================
const ANALYSIS_WINDOW_KEY = "macau_analysis_window_v1";
function getAnalysisWindow(){ try{ const v=parseInt(localStorage.getItem(ANALYSIS_WINDOW_KEY)); if(v>=5 && v<=30) return v; }catch(e){} return 10; }
function setAnalysisWindow(v){ try{ localStorage.setItem(ANALYSIS_WINDOW_KEY, String(v)); }catch(e){} }

// ============================================================
// 仪表盘双卡预测 + 上期验证（自学习联动）
// ============================================================
const DASH_PRED_KEY = "macau_dash_pred_v1";
const DASH_STATS_KEY = "macau_dash_stats_v1";
function getDashStats(){ try{ const s=localStorage.getItem(DASH_STATS_KEY); if(s) return JSON.parse(s); }catch(e){} return { pi:{total:0,hit:0}, zone:{total:0,hit:0} }; }
function saveDashStats(s){ try{ localStorage.setItem(DASH_STATS_KEY, JSON.stringify(s)); }catch(e){} }
function updateDashboardPredictions(last10, all){
    const zoneEl=document.getElementById("stat-zone-pred"), zoneSubEl=document.getElementById("stat-zone-sub"), zoneFbEl=document.getElementById("stat-zone-feedback");
    if(!zoneEl) return;
    if(!all.length || !last10.length){
        zoneEl.textContent='--'; zoneSubEl.textContent='区间重码预测 · 待数据';
        if(zoneFbEl) zoneFbEl.innerHTML = `<span class="fb-pending">📡 暂无可验证的上期预测</span>`;
        return;
    }
    const stats=getDashStats();
    // ---- 验证上一轮预测（使用DASH_PRED_KEY快照） ----
    let snap=null;
    try{ const raw=localStorage.getItem(DASH_PRED_KEY); if(raw) snap=JSON.parse(raw); }catch(e){}
    if(snap && snap.basedOnCount===all.length-1 && Array.isArray(snap.zoneDup)){
        const actual=all[all.length-1].specialNum;
        stats.zone.total=(stats.zone.total||0)+1;
        const zoneHit = snap.zoneDup.includes(actual);
        if(zoneHit) stats.zone.hit=(stats.zone.hit||0)+1;
        if(zoneFbEl){
            zoneFbEl.className='stat-feedback ' + (zoneHit?'fb-hit':'fb-miss');
            zoneFbEl.innerHTML = zoneHit ? `✅ 上期(${snap.forExpect||''})预测正确：${actual} 命中重码` : `❌ 上期(${snap.forExpect||''})预测错误：实际${actual} 不在重码内`;
        }
        saveDashStats(stats);
    } else {
        if(zoneFbEl) zoneFbEl.innerHTML = `<span class="fb-pending">📡 暂无可验证的上期预测</span>`;
    }
    // ---- 生成下一期预测：从getZoneDupNums获取重码和独码号码 ----
    const manualTiers = getZoneManualTiers();
    const { dupNums, uniqueNums } = getZoneDupNums(last10, all, manualTiers);
    const zoneDupList = dupNums.map(d=>d.n);
    const zoneUniqList = uniqueNums;
    const dupEl = document.getElementById("stat-zone-dup");
    const uniqEl = document.getElementById("stat-zone-uniq");
    if(dupEl) {
        const dupNumsHtml = zoneDupList.length ? zoneDupList.map(n=>`<span class="num-mini num-dup" style="margin:1px;">${n}</span>`).join('') : '<span style="color:var(--text-muted);font-size:.6rem;">无重码</span>';
        dupEl.innerHTML = `<span class="zone-dup-label" style="color:var(--gold-l);">🔁重码(${zoneDupList.length}个):</span><span class="zone-dup-nums">${dupNumsHtml}</span>`;
    }
    if(uniqEl) {
        const uniqNumsHtml = zoneUniqList.length ? zoneUniqList.map(n=>`<span class="num-mini num-unique" style="margin:1px;">${n}</span>`).join('') : '<span style="color:var(--text-muted);font-size:.6rem;">无独码</span>';
        uniqEl.innerHTML = `<span class="zone-dup-label" style="color:var(--cyan);">❄️独码(${zoneUniqList.length}个):</span><span class="zone-dup-nums">${uniqNumsHtml}</span>`;
    }
    const hasManual = manualTiers && Object.keys(manualTiers).length > 0;
    const zoneAcc = stats.zone.total>0 ? `命中率 ${(stats.zone.hit/stats.zone.total*100).toFixed(0)}%（${stats.zone.total}期）` : '深度学习中';
    zoneSubEl.textContent = `六区间混沌量子推荐档位 · 重码/独码整合分析${hasManual?' [手动]':''} · ${zoneAcc}`;
    // ---- 保存本轮预测快照，供下期验证 ----
    try{
        const existingSnap = JSON.parse(localStorage.getItem(DASH_PRED_KEY)||'{}');
        localStorage.setItem(DASH_PRED_KEY, JSON.stringify({ ...existingSnap, basedOnCount: all.length, forExpect: nextExpect(), zoneDup: zoneDupList }));
    }catch(e){}
}

// ============================================================
// 官方开奖接口同步（纯前端 fetch，本地数据为最终来源）
// ============================================================
const SYNC_CONFIG_KEY = "macau_sync_config_v1";
const DEFAULT_SYNC_CONFIG = { url: "https://macaumarksix.com/api/live2", autoSync: false, intervalMin: 10, lastSyncAt: "", lastSyncMsg: "" };
function getSyncConfig(){ try{ const s=localStorage.getItem(SYNC_CONFIG_KEY); if(s){ const c=JSON.parse(s); return {...DEFAULT_SYNC_CONFIG, ...c}; } }catch(e){} return {...DEFAULT_SYNC_CONFIG}; }
function saveSyncConfig(c){ try{ localStorage.setItem(SYNC_CONFIG_KEY, JSON.stringify(c)); }catch(e){} }
// 将各种可能的字段名规整为 {expect, openCode, specialNum}
function parseSyncItem(item){
    if(!item || typeof item!=='object') return null;
    const expect = item.expect ?? item.expect_no ?? item.issue ?? item.period ?? item.no ?? item.qihao ?? item.term;
    let openCodeStr = item.openCode ?? item.open_code ?? item.opencode ?? item.code ?? item.numbers ?? item.number;
    let special = item.specialNum ?? item.special ?? item.tema ?? item.sm ?? item.zodiacNum;
    if(Array.isArray(openCodeStr)) openCodeStr = openCodeStr.join(',');
    if(openCodeStr==null && special==null) return null;
    let arr = [];
    if(typeof openCodeStr==='string') arr = openCodeStr.split(/[,，\s+]+/).map(s=>s.trim()).filter(Boolean).map(Number);
    else if(typeof openCodeStr==='number') arr = [openCodeStr];
    let specialNum = (special!=null) ? Number(special) : (arr.length ? arr[arr.length-1] : NaN);
    if(!arr.length && !isNaN(specialNum)) arr=[specialNum];
    if(isNaN(specialNum) || specialNum<1 || specialNum>49) return null;
    return { expect: expect!=null ? String(expect) : null, openCode: arr.join(','), specialNum };
}
function extractSyncArray(data){
    if(Array.isArray(data)) return data;
    if(!data || typeof data!=='object') return [];
    for(const key of ['data','result','list','records','rows','draws','items']){
        if(Array.isArray(data[key])) return data[key];
        if(data[key] && typeof data[key]==='object'){
            for(const k2 of ['data','result','list','records','rows']){
                if(Array.isArray(data[key][k2])) return data[key][k2];
            }
        }
    }
    // 单条记录对象（非数组）
    const single = parseSyncItem(data);
    return single ? [data] : [];
}
async function syncFromAPI(showFeedback=true){
    const cfg=getSyncConfig();
    const statusEl=document.getElementById("syncStatus");
    if(!cfg.url){ if(showFeedback) showToast("⚠️ 请先在「设置」中填写官方开奖接口地址"); return; }
    if(statusEl) statusEl.textContent='🔄 同步中...';
    try{
        const resp = await fetch(cfg.url, { method:'GET', cache:'no-store' });
        if(!resp.ok) throw new Error(`HTTP ${resp.status}`);
        const data = await resp.json();
        const arr = extractSyncArray(data);
        if(!arr.length) throw new Error('接口返回数据为空或格式不支持');
        let added=0, skipped=0, fallbackExpect=null;
        for(const raw of arr){
            const rec = parseSyncItem(raw);
            if(!rec){ skipped++; continue; }
            if(!rec.expect){
                if(fallbackExpect===null){ fallbackExpect=parseInt(nextExpect(),10); if(isNaN(fallbackExpect)) fallbackExpect=null; }
                rec.expect = (fallbackExpect!==null) ? String(fallbackExpect++) : `sync_${Date.now()}_${added}`;
            }
            await saveRecord({ expect:rec.expect, openCode:rec.openCode, specialNum:rec.specialNum, timestamp:Date.now(), source:'sync' });
            added++;
        }
        allRecords = await getAllRecords();
        await refreshUI();
        cfg.lastSyncAt = new Date().toLocaleString('zh-CN');
        cfg.lastSyncMsg = `成功同步 ${added} 条${skipped?`（忽略${skipped}条无法识别）`:''}`;
        saveSyncConfig(cfg);
        if(statusEl) statusEl.textContent = `✅ ${cfg.lastSyncAt} 同步${added}条`;
        if(showFeedback) showToast(`✅ 同步完成：新增/更新 ${added} 期`);
    }catch(e){
        cfg.lastSyncAt = new Date().toLocaleString('zh-CN');
        cfg.lastSyncMsg = `失败：${e.message}`;
        saveSyncConfig(cfg);
        if(statusEl) statusEl.textContent = `❌ 同步失败：${e.message}`;
        if(showFeedback) showToast(`❌ 同步失败：${e.message}（可能为跨域限制，请检查接口或在设置中确认地址）`);
    }
}
function setupAutoSync(){
    clearInterval(window._autoSyncTimer);
    const cfg=getSyncConfig();
    if(cfg.autoSync && cfg.url){
        window._autoSyncTimer = setInterval(()=>syncFromAPI(false), Math.max(1,cfg.intervalMin)*60*1000);
    }
}

// ============================================================
// 初始化
// ============================================================
// ============================================================
// 历史开奖接口
// ============================================================
async function openHistoryAPI(){
    const year = new Date().getFullYear();
    const url = `https://history.macaumarksix.com/history/macaujc2/y/${year}`;
    showModal(`
        <div class="modal-title"><span>📜 历史开奖接口</span><span class="modal-close" onclick="closeModal()"><i class="fas fa-times"></i></span></div>
        <div class="modal-section">
            <div class="modal-section-title">🔗 历史开奖数据接口</div>
            <div class="modal-row" style="flex-direction:column;align-items:stretch;gap:6px;">
                <span>API地址（当前年份）</span>
                <input type="text" value="${url}" readonly style="width:100%;background:var(--surface);border:1px solid var(--border2);border-radius:6px;padding:7px 9px;color:var(--text);font-size:.66rem;font-family:'JetBrains Mono',monospace;box-sizing:border-box;">
            </div>
            <div class="modal-row" style="flex-direction:column;align-items:stretch;gap:6px;">
                <span>选择年份</span>
                <select id="historyYearSelect" onchange="updateHistoryUrl(this.value)" style="background:var(--surface);border:1px solid var(--border2);border-radius:6px;color:var(--text);font-size:.66rem;padding:4px 6px;">
                    ${[2020,2021,2022,2023,2024,2025,2026].map(y=>`<option value="${y}" ${y===year?'selected':''}>${y}年</option>`).join('')}
                </select>
            </div>
            <div class="modal-row" style="flex-direction:column;align-items:stretch;gap:6px;">
                <span>完整API地址</span>
                <input type="text" id="historyFullUrl" value="${url}" readonly style="width:100%;background:var(--surface);border:1px solid var(--border2);border-radius:6px;padding:7px 9px;color:var(--gold-l);font-size:.66rem;font-family:'JetBrains Mono',monospace;box-sizing:border-box;">
            </div>
            <div class="modal-actions">
                <button class="btn" onclick="fetchHistoryAPI()"><i class="fas fa-download"></i> 获取历史数据</button>
                <button class="btn" onclick="copyHistoryUrl()"><i class="fas fa-copy"></i> 复制地址</button>
            </div>
            <div class="modal-desc">此接口用于获取指定年份的历史开奖数据。点击「获取历史数据」将自动拉取并导入到本地数据库中。</div>
        </div>
        <div id="historyResult" style="max-height:300px;overflow-y:auto;"></div>
    `);
}
function updateHistoryUrl(year){
    const url = `https://history.macaumarksix.com/history/macaujc2/y/${year}`;
    const el = document.getElementById("historyFullUrl");
    if(el) el.value = url;
}
function copyHistoryUrl(){
    const el = document.getElementById("historyFullUrl");
    if(el){ navigator.clipboard.writeText(el.value).then(()=>showToast("✅ 地址已复制")); }
}
async function fetchHistoryAPI(){
    const year = document.getElementById("historyYearSelect")?.value || new Date().getFullYear();
    const url = `https://history.macaumarksix.com/history/macaujc2/y/${year}`;
    const resultEl = document.getElementById("historyResult");
    if(resultEl) resultEl.innerHTML = '<div style="padding:10px;color:var(--cyan);">🔄 正在获取数据...</div>';
    try{
        const resp = await fetch(url, { method:'GET', cache:'no-store' });
        if(!resp.ok) throw new Error(`HTTP ${resp.status}`);
        const data = await resp.json();
        const arr = extractSyncArray(data);
        if(!arr.length) throw new Error('接口返回数据为空或格式不支持');
        let added=0, skipped=0;
        for(const raw of arr){
            const rec = parseSyncItem(raw);
            if(!rec){ skipped++; continue; }
            await saveRecord({ expect:rec.expect, openCode:rec.openCode, specialNum:rec.specialNum, timestamp:Date.now(), source:'history_api' });
            added++;
        }
        allRecords = await getAllRecords();
        await refreshUI();
        if(resultEl) resultEl.innerHTML = `<div style="padding:10px;color:var(--green);">✅ 成功导入 ${added} 期历史数据${skipped?`（跳过${skipped}条）`:''}</div>`;
        showToast(`✅ 历史数据导入完成：${added} 期`);
    }catch(e){
        if(resultEl) resultEl.innerHTML = `<div style="padding:10px;color:var(--red);">❌ 获取失败：${e.message}</div>`;
        showToast(`❌ 历史数据获取失败：${e.message}`);
    }
}

// ============================================================
// 确认保存所有设置
// ============================================================
function confirmSaveAllSettings(){
    // Save π energy settings
    const piLevel = document.getElementById("piLevelSelect")?.value || '6';
    const piLearn = document.getElementById("piLearnAbilitySelect")?.value || 'super';
    const piAnalysis = document.getElementById("piAnalysisAbilitySelect")?.value || 'god';
    const piPred = document.getElementById("piPredAbilitySelect")?.value || 'god';
    const piAnalysisPred = document.getElementById("piAnalysisPredSelect")?.value || 'god';
    try{
        localStorage.setItem("macau_pi_level_v1", piLevel);
        localStorage.setItem("macau_pi_learn_v1", piLearn);
        localStorage.setItem("macau_pi_analysis_v1", piAnalysis);
        localStorage.setItem("macau_pi_pred_v1", piPred);
        localStorage.setItem("macau_pi_analysis_pred_v1", piAnalysisPred);
    }catch(e){}
    
    // Save AI settings
    const aiStrength = document.getElementById("aiLearnStrengthSelect")?.value || 'high';
    const aiMode = document.getElementById("aiPredModeSelect")?.value || 'reverse';
    const learnPred = document.getElementById("learnPredAbilitySelect")?.value || 'master';
    const aiLearnAbility = document.getElementById("aiLearnAbilitySelect")?.value || 'master';
    const aiAnalysisPred = document.getElementById("aiAnalysisPredSelect")?.value || 'master';
    const topLearn = document.getElementById("topLearnProgressSelect")?.value || 'stage4';
    const stability = document.getElementById("stabilityToggle")?.checked ?? true;
    const globalDeepLearn = document.getElementById("globalDeepLearnToggle")?.checked ?? true;
    const globalPredEnhance = document.getElementById("globalPredEnhanceSelect")?.value || 'master';
    const globalAnalysisEnhance = document.getElementById("globalAnalysisEnhanceSelect")?.value || 'master';
    const globalLearnEnhance = document.getElementById("globalLearnEnhanceSelect")?.value || 'master';
    const multiResonance = document.getElementById("multiResonanceToggle")?.checked ?? true;
    const quantumEntangle = document.getElementById("quantumEntangleToggle")?.checked ?? true;
    const inertiaLearn = document.getElementById("inertiaLearnToggle")?.checked ?? true;
    const trendShapeLearn = document.getElementById("trendShapeLearnToggle")?.checked ?? true;
    const probDistLearn = document.getElementById("probDistLearnToggle")?.checked ?? true;
    const waveShapeLearn = document.getElementById("waveShapeLearnToggle")?.checked ?? true;
    const piChangeLearn = document.getElementById("piChangeLearnToggle")?.checked ?? true;
    const ruleEngineLearn = document.getElementById("ruleEngineLearnToggle")?.checked ?? true;
    try{
        localStorage.setItem("macau_ai_strength_v1", aiStrength);
        localStorage.setItem("macau_ai_mode_v1", aiMode);
        localStorage.setItem("macau_learn_pred_v1", learnPred);
        localStorage.setItem("macau_ai_learn_ability_v1", aiLearnAbility);
        localStorage.setItem("macau_ai_analysis_pred_v1", aiAnalysisPred);
        localStorage.setItem("macau_top_learn_v1", topLearn);
        localStorage.setItem("macau_stability_v1", stability ? "1" : "0");
        localStorage.setItem("macau_global_deep_learn_v1", globalDeepLearn ? "1" : "0");
        localStorage.setItem("macau_global_pred_enhance_v1", globalPredEnhance);
        localStorage.setItem("macau_global_analysis_enhance_v1", globalAnalysisEnhance);
        localStorage.setItem("macau_global_learn_enhance_v1", globalLearnEnhance);
        localStorage.setItem("macau_multi_resonance_v1", multiResonance ? "1" : "0");
        localStorage.setItem("macau_quantum_entangle_v1", quantumEntangle ? "1" : "0");
        localStorage.setItem("macau_inertia_learn_v1", inertiaLearn ? "1" : "0");
        localStorage.setItem("macau_trend_shape_learn_v1", trendShapeLearn ? "1" : "0");
        localStorage.setItem("macau_prob_dist_learn_v1", probDistLearn ? "1" : "0");
        localStorage.setItem("macau_wave_shape_learn_v1", waveShapeLearn ? "1" : "0");
        localStorage.setItem("macau_pi_change_learn_v1", piChangeLearn ? "1" : "0");
        localStorage.setItem("macau_rule_engine_learn_v1", ruleEngineLearn ? "1" : "0");
    }catch(e){}

    // Save sync settings
    saveSyncSettingsFromUI();
    
    // Save analysis window
    const windowVal = document.getElementById("analysisWindowSelect")?.value;
    if(windowVal) setAnalysisWindow(parseInt(windowVal));
    
    // Refresh UI to apply all settings globally
    refreshUI();
    
    showToast("✅ 所有设置已永久保存并联动全局");
    setTimeout(()=>closeModal(), 800);
}

// ============================================================
// 更新仪表盘AI高/低概率号码显示
// ============================================================
function updateDashboardAIHighLow(all){
    const el = document.getElementById("stat-ai-high-low");
    const subEl = document.getElementById("stat-ai-sub");
    const fbEl = document.getElementById("stat-ai-feedback");
    if(!el) return;
    if(!all || all.length < 3){
        el.textContent = '--';
        if(subEl) subEl.textContent = 'π恒态矩阵 · 1-49 能量分布场 · 待数据';
        if(fbEl) fbEl.innerHTML = `<span class="fb-pending">📡 暂无可验证的上期预测</span>`;
        return;
    }
    const {pct, ranking} = runLearningAndPredict(all);
    const top = ranking.slice(0, 6);
    const bottom = ranking.slice(-6).reverse();
    const stats = getPredStats();
    const accTxt = stats.total > 0 ? `近${stats.total}期学习样本 · 前15强命中率 ${(stats.hit15/stats.total*100).toFixed(0)}%` : 'π恒态矩阵正在积累能量学习样本';

    el.innerHTML = `<div style="width:100%;"><div style="margin-bottom:6px;"><span style="color:var(--gold-l);">🎯高能量:</span> ${top.map(n=>`<strong style="color:var(--gold-l);">${n}</strong>(${pct[n]}%)`).join('、')}</div><div><span style="color:var(--cyan);">🧊低能量:</span> ${bottom.map(n=>`${n}(${pct[n]}%)`).join('、')}</div></div>`;
    if(subEl) subEl.textContent = `π恒态矩阵 · 能量分布场 · ${accTxt}`;

    // Verify feedback: always show result if we have at least 2 records
    if(fbEl){
        try{
            const snapRaw = localStorage.getItem(PRED_SNAPSHOT_KEY);
            if(snapRaw && all.length >= 2){
                const snap = JSON.parse(snapRaw);
                if(snap && Array.isArray(snap.ranking)){
                    const actual = all[all.length-1].specialNum;
                    const rank = snap.ranking.indexOf(actual) + 1;
                    const hit = rank > 0 && rank <= 15;
                    fbEl.className = 'stat-feedback ' + (hit ? 'fb-hit' : 'fb-miss');
                    fbEl.innerHTML = hit ? `✅ 上期预测正确：${actual} 排第${rank}位` : `❌ 上期预测错误：${actual} 排第${rank > 0 ? rank : '50+'}位`;
                } else {
                    fbEl.innerHTML = `<span class="fb-pending">📡 暂无可验证的上期预测</span>`;
                }
            } else {
                fbEl.innerHTML = `<span class="fb-pending">📡 暂无可验证的上期预测</span>`;
            }
        }catch(e){ fbEl.innerHTML = `<span class="fb-pending">📡 暂无可验证的上期预测</span>`; }
    }
}

window.onload=async()=>{
    try{
        await openDB();
        loadNotes();
        allRecords = await getAllRecords();
        await refreshUI();
    }catch(e){
        console.error("初始化数据加载异常：", e);
    }
    const clearBtn=document.getElementById("clearBtn"); if(clearBtn) clearBtn.onclick=confirmClearAll;
    const settingsBtn=document.getElementById("settingsBtn"); if(settingsBtn) settingsBtn.onclick=openSettings;
    const syncBtn=document.getElementById("syncBtn"); if(syncBtn) syncBtn.onclick=()=>syncFromAPI(true);
    setupAutoSync();
    try{
        const cfg=getSyncConfig();
        const statusEl=document.getElementById("syncStatus");
        if(statusEl && cfg.lastSyncAt) statusEl.textContent = `上次同步：${cfg.lastSyncAt}`;
    }catch(e){}
    const addBtn=document.getElementById("manualAddBtn"); if(addBtn) addBtn.onclick=manualAddRecord;
    const numsInp=document.getElementById("manualNums"); if(numsInp) numsInp.addEventListener('keydown', e=>{ if(e.key==='Enter') manualAddRecord(); });
    const expectInp=document.getElementById("manualExpect"); if(expectInp) expectInp.addEventListener('keydown', e=>{ if(e.key==='Enter') manualAddRecord(); });
};
</script>
</body>
</html>