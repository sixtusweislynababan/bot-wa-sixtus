<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sixtus Terminal v40.0</title>
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    :root {
      --bg-deep: #05080c;
      --bg-surface: #0c1117;
      --bg-elevated: #141b24;
      --accent: #00e5a0;
      --accent-dim: #00b37d;
      --warning: #ffb020;
      --danger: #ff4757;
      --info: #3b82f6;
      --text-main: #e8eaed;
      --text-muted: #6b7a8f;
      --border: #1e2a38;
      --glow: rgba(0, 229, 160, 0.15);
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }
    
    body {
      font-family: 'Space Grotesk', sans-serif;
      background: var(--bg-deep);
      color: var(--text-main);
      min-height: 100vh;
      overflow-x: hidden;
    }

    /* Animated Grid Background */
    .grid-bg {
      position: fixed;
      inset: 0;
      background-image: 
        linear-gradient(rgba(0, 229, 160, 0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0, 229, 160, 0.03) 1px, transparent 1px);
      background-size: 60px 60px;
      z-index: 0;
    }

    .grid-bg::after {
      content: '';
      position: absolute;
      inset: 0;
      background: radial-gradient(ellipse at 50% 0%, rgba(0, 229, 160, 0.08) 0%, transparent 60%);
    }

    /* Floating Orbs */
    .orb {
      position: fixed;
      border-radius: 50%;
      filter: blur(100px);
      opacity: 0.4;
      animation: orbFloat 20s ease-in-out infinite;
      pointer-events: none;
    }

    .orb-1 {
      width: 500px;
      height: 500px;
      background: radial-gradient(circle, rgba(0, 229, 160, 0.3), transparent 70%);
      top: -150px;
      left: -100px;
    }

    .orb-2 {
      width: 400px;
      height: 400px;
      background: radial-gradient(circle, rgba(59, 130, 246, 0.25), transparent 70%);
      bottom: -100px;
      right: -50px;
      animation-delay: -10s;
    }

    @keyframes orbFloat {
      0%, 100% { transform: translate(0, 0) scale(1); }
      33% { transform: translate(30px, -40px) scale(1.05); }
      66% { transform: translate(-20px, 20px) scale(0.95); }
    }

    /* Scanline Effect */
    .scanlines {
      position: fixed;
      inset: 0;
      background: repeating-linear-gradient(
        0deg,
        transparent,
        transparent 2px,
        rgba(0, 0, 0, 0.03) 2px,
        rgba(0, 0, 0, 0.03) 4px
      );
      pointer-events: none;
      z-index: 1000;
    }

    /* Top Accent Bar */
    .accent-bar {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      height: 2px;
      background: linear-gradient(90deg, transparent, var(--accent), transparent);
      z-index: 100;
    }

    /* Navigation */
    .nav {
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      z-index: 50;
      background: rgba(5, 8, 12, 0.85);
      backdrop-filter: blur(20px);
      border-bottom: 1px solid var(--border);
    }

    .nav-inner {
      max-width: 1400px;
      margin: 0 auto;
      padding: 0 20px;
      height: 64px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 14px;
    }

    .logo-icon {
      width: 42px;
      height: 42px;
      background: linear-gradient(135deg, var(--accent), var(--accent-dim));
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: 'JetBrains Mono', monospace;
      font-weight: 700;
      font-size: 18px;
      color: var(--bg-deep);
      position: relative;
    }

    .logo-icon::after {
      content: '';
      position: absolute;
      inset: -2px;
      border-radius: 12px;
      background: linear-gradient(135deg, var(--accent), transparent);
      z-index: -1;
      opacity: 0.5;
    }

    .logo-text h1 {
      font-size: 18px;
      font-weight: 700;
      letter-spacing: -0.5px;
    }

    .logo-text span {
      font-size: 11px;
      color: var(--text-muted);
      font-family: 'JetBrains Mono', monospace;
    }

    .nav-tabs {
      display: flex;
      gap: 4px;
      background: var(--bg-surface);
      padding: 4px;
      border-radius: 10px;
      border: 1px solid var(--border);
    }

    .nav-tab {
      padding: 8px 16px;
      font-size: 13px;
      font-weight: 500;
      color: var(--text-muted);
      background: transparent;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      transition: all 0.2s;
      white-space: nowrap;
    }

    .nav-tab:hover {
      color: var(--text-main);
      background: rgba(255, 255, 255, 0.03);
    }

    .nav-tab.active {
      color: var(--bg-deep);
      background: var(--accent);
      font-weight: 600;
    }

    .nav-status {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 6px 14px;
      background: var(--bg-surface);
      border: 1px solid var(--border);
      border-radius: 20px;
      font-size: 12px;
      font-family: 'JetBrains Mono', monospace;
    }

    .status-dot {
      width: 8px;
      height: 8px;
      border-radius: 50%;
      background: var(--danger);
    }

    .status-dot.online {
      background: var(--accent);
      box-shadow: 0 0 10px var(--accent);
      animation: pulse 2s infinite;
    }

    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.5; }
    }

    /* Main Content */
    .main {
      position: relative;
      z-index: 10;
      padding: 84px 20px 40px;
      max-width: 1400px;
      margin: 0 auto;
    }

    /* Tab Content */
    .tab-panel {
      display: none;
      animation: fadeIn 0.3s ease;
    }

    .tab-panel.active {
      display: block;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

    /* Hero Section */
    .hero {
      text-align: center;
      padding: 40px 0 50px;
    }

    .hero-badge {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 8px 16px;
      background: rgba(0, 229, 160, 0.1);
      border: 1px solid rgba(0, 229, 160, 0.2);
      border-radius: 50px;
      font-size: 12px;
      font-weight: 500;
      color: var(--accent);
      margin-bottom: 20px;
      font-family: 'JetBrains Mono', monospace;
    }

    .hero-title {
      font-size: clamp(32px, 6vw, 52px);
      font-weight: 700;
      letter-spacing: -1px;
      margin-bottom: 12px;
      line-height: 1.1;
    }

    .hero-title span {
      background: linear-gradient(135deg, var(--accent), var(--info));
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
    }

    .hero-desc {
      font-size: 16px;
      color: var(--text-muted);
      max-width: 500px;
      margin: 0 auto 24px;
      line-height: 1.6;
    }

    .hero-stats {
      display: flex;
      justify-content: center;
      gap: 40px;
      flex-wrap: wrap;
    }

    .hero-stat {
      text-align: center;
    }

    .hero-stat-value {
      font-size: 28px;
      font-weight: 700;
      font-family: 'JetBrains Mono', monospace;
      color: var(--accent);
    }

    .hero-stat-label {
      font-size: 12px;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 0.5px;
    }

    /* Connection Card */
    .connect-wrapper {
      max-width: 520px;
      margin: 0 auto;
    }

    .connect-card {
      background: var(--bg-surface);
      border: 1px solid var(--border);
      border-radius: 16px;
      overflow: hidden;
    }

    .connect-header {
      padding: 20px 24px;
      background: var(--bg-elevated);
      border-bottom: 1px solid var(--border);
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .connect-title {
      font-size: 16px;
      font-weight: 600;
    }

    .connect-status {
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 12px;
      font-family: 'JetBrains Mono', monospace;
      padding: 4px 12px;
      background: rgba(255, 71, 87, 0.1);
      border-radius: 20px;
      color: var(--danger);
    }

    .connect-status.connected {
      background: rgba(0, 229, 160, 0.1);
      color: var(--accent);
    }

    .connect-status.connecting {
      background: rgba(255, 176, 32, 0.1);
      color: var(--warning);
    }

    .connect-body {
      padding: 24px;
    }

    /* Method Selector */
    .method-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 12px;
      margin-bottom: 20px;
    }

    .method-card {
      padding: 16px;
      background: var(--bg-elevated);
      border: 1px solid var(--border);
      border-radius: 12px;
      cursor: pointer;
      transition: all 0.2s;
      text-align: center;
    }

    .method-card:hover {
      border-color: rgba(0, 229, 160, 0.3);
    }

    .method-card.active {
      border-color: var(--accent);
      background: rgba(0, 229, 160, 0.05);
    }

    .method-icon {
      font-size: 28px;
      margin-bottom: 8px;
    }

    .method-name {
      font-weight: 600;
      font-size: 14px;
      margin-bottom: 4px;
    }

    .method-desc {
      font-size: 11px;
      color: var(--text-muted);
    }

    /* Input */
    .input-group {
      margin-bottom: 16px;
    }

    .input-label {
      display: block;
      font-size: 12px;
      font-weight: 500;
      color: var(--text-muted);
      margin-bottom: 8px;
    }

    .input-field {
      width: 100%;
      padding: 14px 16px;
      background: var(--bg-elevated);
      border: 1px solid var(--border);
      border-radius: 10px;
      font-size: 15px;
      color: var(--text-main);
      font-family: 'JetBrains Mono', monospace;
      transition: all 0.2s;
    }

    .input-field:focus {
      outline: none;
      border-color: var(--accent);
      box-shadow: 0 0 0 3px var(--glow);
    }

    .input-field::placeholder {
      color: var(--text-muted);
    }

    /* Buttons */
    .btn {
      width: 100%;
      padding: 14px 24px;
      font-size: 14px;
      font-weight: 600;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: all 0.2s;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
    }

    .btn-primary {
      background: var(--accent);
      color: var(--bg-deep);
    }

    .btn-primary:hover {
      background: var(--accent-dim);
      transform: translateY(-2px);
      box-shadow: 0 8px 20px rgba(0, 229, 160, 0.3);
    }

    .btn-secondary {
      background: var(--bg-elevated);
      color: var(--text-main);
      border: 1px solid var(--border);
    }

    .btn-secondary:hover {
      background: var(--bg-surface);
    }

    .btn-danger {
      background: rgba(255, 71, 87, 0.1);
      color: var(--danger);
      border: 1px solid rgba(255, 71, 87, 0.2);
    }

    .btn-danger:hover {
      background: rgba(255, 71, 87, 0.2);
    }

    /* QR Display */
    .qr-container {
      text-align: center;
      padding: 20px 0;
    }

    .qr-frame {
      position: relative;
      display: inline-block;
      padding: 16px;
      background: var(--bg-elevated);
      border-radius: 16px;
      border: 1px solid var(--border);
    }

    .qr-corners {
      position: absolute;
      width: 20px;
      height: 20px;
      border: 2px solid var(--accent);
    }

    .qr-corners.tl { top: -1px; left: -1px; border-right: none; border-bottom: none; border-radius: 8px 0 0 0; }
    .qr-corners.tr { top: -1px; right: -1px; border-left: none; border-bottom: none; border-radius: 0 8px 0 0; }
    .qr-corners.bl { bottom: -1px; left: -1px; border-right: none; border-top: none; border-radius: 0 0 0 8px; }
    .qr-corners.br { bottom: -1px; right: -1px; border-left: none; border-top: none; border-radius: 0 0 8px 0; }

    .qr-image {
      width: 200px;
      height: 200px;
      border-radius: 8px;
    }

    .qr-instruction {
      margin-top: 16px;
      font-size: 12px;
      color: var(--text-muted);
    }

    /* Pairing Code */
    .pairing-display {
      text-align: center;
      padding: 20px 0;
    }

    .pairing-digits {
      display: flex;
      justify-content: center;
      gap: 8px;
      margin: 16px 0;
    }

    .pairing-digit {
      width: 44px;
      height: 56px;
      background: var(--bg-elevated);
      border: 1px solid var(--border);
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 24px;
      font-weight: 700;
      font-family: 'JetBrains Mono', monospace;
      color: var(--accent);
    }

    /* Terminal */
    .terminal {
      background: var(--bg-surface);
      border: 1px solid var(--border);
      border-radius: 12px;
      overflow: hidden;
      margin-top: 20px;
    }

    .terminal-header {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 12px 16px;
      background: var(--bg-elevated);
      border-bottom: 1px solid var(--border);
    }

    .terminal-dot {
      width: 12px;
      height: 12px;
      border-radius: 50%;
    }

    .terminal-dot.red { background: #ff5f56; }
    .terminal-dot.yellow { background: #ffbd2e; }
    .terminal-dot.green { background: #27ca40; }

    .terminal-title {
      flex: 1;
      text-align: center;
      font-size: 12px;
      color: var(--text-muted);
      font-family: 'JetBrains Mono', monospace;
    }

    .terminal-body {
      padding: 16px;
      font-family: 'JetBrains Mono', monospace;
      font-size: 12px;
      max-height: 180px;
      overflow-y: auto;
      line-height: 1.8;
    }

    .log-line {
      margin-bottom: 4px;
    }

    .log-time {
      color: var(--text-muted);
    }

    .log-info { color: var(--info); }
    .log-success { color: var(--accent); }
    .log-warn { color: var(--warning); }
    .log-error { color: var(--danger); }

    /* Content Grid */
    .content-grid {
      display: grid;
      gap: 16px;
    }

    @media (min-width: 768px) {
      .content-grid {
        grid-template-columns: repeat(2, 1fr);
      }
    }

    @media (min-width: 1024px) {
      .content-grid {
        grid-template-columns: repeat(3, 1fr);
      }
    }

    /* Feature Cards */
    .feature-card {
      background: var(--bg-surface);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 20px;
      transition: all 0.3s;
    }

    .feature-card:hover {
      border-color: rgba(0, 229, 160, 0.3);
      transform: translateY(-4px);
      box-shadow: 0 12px 30px rgba(0, 0, 0, 0.3);
    }

    .feature-icon {
      width: 48px;
      height: 48px;
      border-radius: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 22px;
      margin-bottom: 16px;
    }

    .feature-title {
      font-size: 16px;
      font-weight: 600;
      margin-bottom: 8px;
    }

    .feature-desc {
      font-size: 13px;
      color: var(--text-muted);
      margin-bottom: 16px;
      line-height: 1.5;
    }

    .feature-cmds {
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
    }

    .cmd-tag {
      padding: 5px 10px;
      background: var(--bg-elevated);
      border: 1px solid var(--border);
      border-radius: 6px;
      font-size: 11px;
      font-family: 'JetBrains Mono', monospace;
      color: var(--accent);
      cursor: pointer;
      transition: all 0.2s;
    }

    .cmd-tag:hover {
      background: rgba(0, 229, 160, 0.1);
      border-color: var(--accent);
    }

    /* Bot Panel */
    .bot-layout {
      display: grid;
      gap: 20px;
    }

    @media (min-width: 1024px) {
      .bot-layout {
        grid-template-columns: 260px 1fr;
      }
    }

    .sidebar {
      background: var(--bg-surface);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 16px;
      height: fit-content;
    }

    .sidebar-section {
      margin-bottom: 20px;
    }

    .sidebar-title {
      font-size: 10px;
      font-weight: 600;
      color: var(--text-muted);
      text-transform: uppercase;
      letter-spacing: 1px;
      margin-bottom: 12px;
    }

    .sidebar-item {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 10px 12px;
      border-radius: 8px;
      font-size: 13px;
      color: var(--text-muted);
      cursor: pointer;
      transition: all 0.2s;
    }

    .sidebar-item:hover {
      background: var(--bg-elevated);
      color: var(--text-main);
    }

    .sidebar-item.active {
      background: rgba(0, 229, 160, 0.1);
      color: var(--accent);
    }

    .sidebar-item-count {
      margin-left: auto;
      font-size: 10px;
      padding: 2px 8px;
      background: var(--bg-elevated);
      border-radius: 20px;
      font-family: 'JetBrains Mono', monospace;
    }

    .sidebar-status {
      padding: 16px;
      background: var(--bg-elevated);
      border-radius: 10px;
    }

    .status-row {
      display: flex;
      justify-content: space-between;
      font-size: 12px;
      margin-bottom: 10px;
    }

    .status-row:last-child {
      margin-bottom: 0;
    }

    .status-row span:first-child {
      color: var(--text-muted);
    }

    .main-panel {
      background: var(--bg-surface);
      border: 1px solid var(--border);
      border-radius: 14px;
      padding: 20px;
    }

    .panel-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
      flex-wrap: wrap;
      gap: 12px;
    }

    .panel-title {
      font-size: 16px;
      font-weight: 600;
    }

    .search-input {
      padding: 10px 14px;
      background: var(--bg-elevated);
      border: 1px solid var(--border);
      border-radius: 8px;
      color: var(--text-main);
      font-size: 13px;
      outline: none;
      transition: all 0.2s;
      width: 200px;
    }

    .search-input:focus {
      border-color: var(--accent);
    }

    .cmd-grid {
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
      max-height: 500px;
      overflow-y: auto;
    }

    /* Downloader Grid */
    .dl-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 12px;
    }

    @media (min-width: 640px) {
      .dl-grid {
        grid-template-columns: repeat(3, 1fr);
      }
    }

    @media (min-width: 1024px) {
      .dl-grid {
        grid-template-columns: repeat(4, 1fr);
      }
    }

    .dl-card {
      padding: 20px;
      border-radius: 12px;
      cursor: pointer;
      transition: all 0.3s;
      text-align: center;
    }

    .dl-card:hover {
      transform: scale(1.05);
    }

    .dl-icon {
      font-size: 28px;
      margin-bottom: 10px;
    }

    .dl-name {
      font-weight: 600;
      font-size: 14px;
      margin-bottom: 4px;
    }

    .dl-cmd {
      font-size: 11px;
      opacity: 0.7;
      font-family: 'JetBrains Mono', monospace;
    }

    /* Music Player */
    .music-search-wrapper {
      max-width: 500px;
      margin: 0 auto 24px;
      position: relative;
    }

    .music-search {
      width: 100%;
      padding: 14px 16px 14px 48px;
      background: var(--bg-surface);
      border: 1px solid var(--border);
      border-radius: 12px;
      color: var(--text-main);
      font-size: 15px;
      outline: none;
      transition: all 0.2s;
    }

    .music-search:focus {
      border-color: var(--accent);
    }

    .search-icon {
      position: absolute;
      left: 16px;
      top: 50%;
      transform: translateY(-50%);
      color: var(--text-muted);
    }

    .music-container {
      background: var(--bg-surface);
      border: 1px solid var(--border);
      border-radius: 14px;
      overflow: hidden;
    }

    .music-header {
      padding: 14px 20px;
      background: var(--bg-elevated);
      border-bottom: 1px solid var(--border);
      display: flex;
      align-items: center;
      gap: 12px;
      font-size: 13px;
    }

    .music-header code {
      color: var(--accent);
      font-family: 'JetBrains Mono', monospace;
    }

    .music-header span {
      color: var(--text-muted);
    }

    .music-list {
      max-height: 400px;
      overflow-y: auto;
    }

    .music-item {
      display: flex;
      align-items: center;
      gap: 14px;
      padding: 12px 20px;
      border-bottom: 1px solid var(--border);
      cursor: pointer;
      transition: background 0.2s;
    }

    .music-item:hover {
      background: var(--bg-elevated);
    }

    .music-num {
      width: 24px;
      font-size: 12px;
      color: var(--text-muted);
      font-family: 'JetBrains Mono', monospace;
    }

    .music-info {
      flex: 1;
      min-width: 0;
    }

    .music-title {
      font-size: 14px;
      font-weight: 500;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .music-artist {
      font-size: 12px;
      color: var(--text-muted);
    }

    /* Footer */
    .footer {
      border-top: 1px solid var(--border);
      background: var(--bg-surface);
      padding: 30px 20px;
      margin-top: 50px;
    }

    .footer-content {
      max-width: 1400px;
      margin: 0 auto;
      display: flex;
      flex-wrap: wrap;
      justify-content: space-between;
      align-items: center;
      gap: 20px;
    }

    .footer-brand {
      display: flex;
      align-items: center;
      gap: 14px;
    }

    .footer-logo {
      width: 40px;
      height: 40px;
      background: linear-gradient(135deg, var(--accent), var(--accent-dim));
      border-radius: 10px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-weight: 700;
      font-family: 'JetBrains Mono', monospace;
      color: var(--bg-deep);
    }

    .footer-name {
      font-weight: 600;
    }

    .footer-owner {
      font-size: 12px;
      color: var(--text-muted);
    }

    .footer-contact {
      display: flex;
      align-items: center;
      gap: 8px;
      padding: 10px 20px;
      background: rgba(0, 229, 160, 0.1);
      border: 1px solid rgba(0, 229, 160, 0.2);
      border-radius: 10px;
      color: var(--accent);
      text-decoration: none;
      font-size: 14px;
      transition: all 0.2s;
    }

    .footer-contact:hover {
      background: rgba(0, 229, 160, 0.2);
    }

    /* Toast */
    .toast {
      position: fixed;
      bottom: 24px;
      left: 50%;
      transform: translateX(-50%) translateY(100px);
      background: var(--accent);
      color: var(--bg-deep);
      padding: 12px 24px;
      border-radius: 10px;
      font-size: 14px;
      font-weight: 600;
      opacity: 0;
      transition: all 0.3s;
      z-index: 1000;
    }

    .toast.show {
      opacity: 1;
      transform: translateX(-50%) translateY(0);
    }

    /* Scrollbar */
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }

    ::-webkit-scrollbar-track {
      background: var(--bg-surface);
    }

    ::-webkit-scrollbar-thumb {
      background: var(--accent);
      border-radius: 3px;
    }

    /* Mobile Nav */
    .mobile-nav {
      display: block;
    }

    @media (min-width: 900px) {
      .mobile-nav {
        display: none;
      }
    }

    .desktop-nav {
      display: none;
    }

    @media (min-width: 900px) {
      .desktop-nav {
        display: flex;
      }
    }

    .mobile-select {
      width: 100%;
      padding: 10px 14px;
      background: var(--bg-surface);
      border: 1px solid var(--border);
      border-radius: 8px;
      color: var(--text-main);
      font-size: 14px;
      outline: none;
    }

    /* Utility */
    .hidden { display: none !important; }
    .text-center { text-align: center; }
    .flex-center { display: flex; align-items: center; justify-content: center; }
    .gap-2 { gap: 8px; }
    .mt-4 { margin-top: 16px; }
    .mb-4 { margin-bottom: 16px; }
  </style>
</head>
<body>
  <!-- Background Effects -->
  <div class="grid-bg"></div>
  <div class="orb orb-1"></div>
  <div class="orb orb-2"></div>
  <div class="scanlines"></div>
  <div class="accent-bar"></div>

  <!-- Navigation -->
  <nav class="nav">
    <div class="nav-inner">
      <div class="logo">
        <div class="logo-icon">S</div>
        <div class="logo-text">
          <h1>Sixtus Terminal</h1>
          <span>v40.0 // ULTIMATE</span>
        </div>
      </div>

      <div class="nav-tabs desktop-nav">
        <button class="nav-tab active" data-tab="connect">Connect</button>
        <button class="nav-tab" data-tab="home">Home</button>
        <button class="nav-tab" data-tab="bot">Bot Panel</button>
        <button class="nav-tab" data-tab="game">Game</button>
        <button class="nav-tab" data-tab="tools">Tools</button>
        <button class="nav-tab" data-tab="music">Music</button>
        <button class="nav-tab" data-tab="download">Download</button>
      </div>

      <div class="nav-status">
        <div class="status-dot" id="globalStatus"></div>
        <span id="globalStatusText">Offline</span>
      </div>
    </div>
  </nav>

  <!-- Mobile Navigation -->
  <div class="main">
    <div class="mobile-nav mb-4">
      <select class="mobile-select" id="mobileNav">
        <option value="connect">Connect</option>
        <option value="home">Home</option>
        <option value="bot">Bot Panel</option>
        <option value="game">Game</option>
        <option value="tools">Tools</option>
        <option value="music">Music</option>
        <option value="download">Download</option>
      </select>
    </div>

    <!-- CONNECT TAB -->
    <div class="tab-panel active" id="tab-connect">
      <div class="connect-wrapper">
        <div class="connect-card">
          <div class="connect-header">
            <span class="connect-title">Connection Manager</span>
            <div class="connect-status" id="connectStatus">
              <span id="connectStatusText">Disconnected</span>
            </div>
          </div>

          <div class="connect-body">
            <!-- Initial Form -->
            <div id="initForm">
              <p class="input-label">Select Connection Method</p>
              <div class="method-grid">
                <div class="method-card active" data-method="qr" onclick="selectMethod('qr')">
                  <div class="method-icon">QR</div>
                  <div class="method-name">Scan Code</div>
                  <div class="method-desc">Use camera to connect</div>
                </div>
                <div class="method-card" data-method="pairing" onclick="selectMethod('pairing')">
                  <div class="method-icon">8-Digit</div>
                  <div class="method-name">Pairing Code</div>
                  <div class="method-desc">Enter code manually</div>
                </div>
              </div>

              <div id="phoneInput" class="hidden">
                <p class="input-label">WhatsApp Number</p>
                <input type="text" class="input-field" id="phoneNumber" placeholder="628xxxxxxxxxx">
                <p style="font-size: 11px; color: var(--text-muted); margin-top: 6px;">Format: 628123456789 (no +, spaces, or dashes)</p>
              </div>

              <button class="btn btn-primary" onclick="initConnect()">Initialize Connection</button>
            </div>

            <!-- QR Display -->
            <div id="qrPanel" class="hidden">
              <div class="qr-container">
                <div class="qr-frame">
                  <div class="qr-corners tl"></div>
                  <div class="qr-corners tr"></div>
                  <div class="qr-corners bl"></div>
                  <div class="qr-corners br"></div>
                  <img class="qr-image" id="qrImage" src="" alt="QR">
                </div>
                <p class="qr-instruction">Scan with WhatsApp → Linked Devices → Link Device</p>
              </div>
              <button class="btn btn-danger mt-4" onclick="cancelConnect()">Cancel Connection</button>
            </div>

            <!-- Pairing Display -->
            <div id="pairingPanel" class="hidden">
              <div class="pairing-display">
                <p style="color: var(--text-muted); margin-bottom: 8px;">Enter this code in WhatsApp:</p>
                <div class="pairing-digits" id="pairingDigits"></div>
                <div class="flex-center gap-2 mt-4">
                  <button class="btn btn-secondary" style="width: auto; flex: 1;" onclick="copyPairing()">Copy Code</button>
                  <button class="btn btn-danger" style="width: auto;" onclick="cancelConnect()">Cancel</button>
                </div>
              </div>
            </div>

            <!-- Connecting -->
            <div id="connectingPanel" class="hidden">
              <div class="text-center" style="padding: 40px 0;">
                <div style="width: 50px; height: 50px; border: 3px solid var(--border); border-top-color: var(--accent); border-radius: 50%; animation: spin 1s linear infinite; margin: 0 auto 20px;"></div>
                <p>Establishing secure connection...</p>
              </div>
            </div>

            <!-- Connected -->
            <div id="connectedPanel" class="hidden">
              <div class="text-center" style="padding: 20px 0;">
                <div style="width: 70px; height: 70px; background: var(--accent); border-radius: 50%; display: flex; align-items: center; justify-content: center; margin: 0 auto 16px; font-size: 28px; color: var(--bg-deep);">OK</div>
                <h3 style="font-size: 20px; margin-bottom: 8px; color: var(--accent);">Connected Successfully</h3>
                <p id="connectedNumber" style="font-family: 'JetBrains Mono', monospace; color: var(--text-muted); margin-bottom: 20px;"></p>
                <div class="flex-center gap-2">
                  <button class="btn btn-primary" style="width: auto; flex: 1;" onclick="showTab('bot')">Open Bot Panel</button>
                  <button class="btn btn-danger" style="width: auto;" onclick="disconnect()">Disconnect</button>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Terminal -->
        <div class="terminal">
          <div class="terminal-header">
            <div class="terminal-dot red"></div>
            <div class="terminal-dot yellow"></div>
            <div class="terminal-dot green"></div>
            <span class="terminal-title">sixtus-terminal</span>
          </div>
          <div class="terminal-body" id="terminalOutput"></div>
        </div>
      </div>
    </div>

    <!-- HOME TAB -->
    <div class="tab-panel" id="tab-home">
      <div class="hero">
        <div class="hero-badge">
          <span>v40.0</span>
          <span>//</span>
          <span>ULTIMATE TOOLS EXPANSION</span>
        </div>
        <h1 class="hero-title">Sixtus <span>Terminal</span></h1>
        <p class="hero-desc">Advanced WhatsApp automation system with 3000+ commands, AI-powered features, and enterprise-grade reliability.</p>
        <div class="hero-stats">
          <div class="hero-stat">
            <div class="hero-stat-value" data-count="3000">0</div>
            <div class="hero-stat-label">Commands</div>
          </div>
          <div class="hero-stat">
            <div class="hero-stat-value" data-count="1000">0</div>
            <div class="hero-stat-label">Songs</div>
          </div>
          <div class="hero-stat">
            <div class="hero-stat-value" data-count="500">0</div>
            <div class="hero-stat-label">Games</div>
          </div>
          <div class="hero-stat">
            <div class="hero-stat-value" data-count="50">0</div>
            <div class="hero-stat-label">Downloaders</div>
          </div>
        </div>
      </div>

      <div class="content-grid" id="featureGrid"></div>
    </div>

    <!-- BOT TAB -->
    <div class="tab-panel" id="tab-bot">
      <div class="bot-layout">
        <div class="sidebar">
          <div class="sidebar-section">
            <div class="sidebar-title">Command Categories</div>
            <div class="sidebar-item active" onclick="loadCommands('all')">
              <span>All Commands</span>
              <span class="sidebar-item-count">3000+</span>
            </div>
            <div class="sidebar-item" onclick="loadCommands('game')">
              <span>Game</span>
              <span class="sidebar-item-count">500+</span>
            </div>
            <div class="sidebar-item" onclick="loadCommands('group')">
              <span>Group</span>
              <span class="sidebar-item-count">100+</span>
            </div>
            <div class="sidebar-item" onclick="loadCommands('tools')">
              <span>Tools</span>
              <span class="sidebar-item-count">500+</span>
            </div>
            <div class="sidebar-item" onclick="loadCommands('downloader')">
              <span>Downloader</span>
              <span class="sidebar-item-count">50+</span>
            </div>
            <div class="sidebar-item" onclick="loadCommands('music')">
              <span>Music</span>
              <span class="sidebar-item-count">20+</span>
            </div>
          </div>

          <div class="sidebar-section">
            <div class="sidebar-title">Bot Status</div>
            <div class="sidebar-status">
              <div class="status-row">
                <span>Status</span>
                <span id="sidebarStatus" style="color: var(--accent);">Online</span>
              </div>
              <div class="status-row">
                <span>Uptime</span>
                <span id="sidebarUptime">00:00:00</span>
              </div>
              <div class="status-row">
                <span>Messages</span>
                <span id="sidebarMessages">0</span>
              </div>
            </div>
          </div>
        </div>

        <div class="main-panel">
          <div class="panel-header">
            <h3 class="panel-title" id="panelTitle">All Commands</h3>
            <input type="text" class="search-input" placeholder="Search commands..." id="cmdSearch" oninput="filterCmds()">
          </div>
          <div class="cmd-grid" id="cmdGrid"></div>
        </div>
      </div>
    </div>

    <!-- GAME TAB -->
    <div class="tab-panel" id="tab-game">
      <h2 class="hero-title text-center" style="font-size: 28px; margin-bottom: 8px;">Game <span>Center</span></h2>
      <p class="hero-desc text-center" style="margin-bottom: 30px;">500+ interactive games and fun commands</p>
      <div class="content-grid" id="gameGrid"></div>
    </div>

    <!-- TOOLS TAB -->
    <div class="tab-panel" id="tab-tools">
      <h2 class="hero-title text-center" style="font-size: 28px; margin-bottom: 8px;">Utility <span>Tools</span></h2>
      <p class="hero-desc text-center" style="margin-bottom: 30px;">Converters, generators, and productivity tools</p>
      <div class="content-grid" id="toolsGrid"></div>
    </div>

    <!-- MUSIC TAB -->
    <div class="tab-panel" id="tab-music">
      <h2 class="hero-title text-center" style="font-size: 28px; margin-bottom: 8px;">Music <span>Library</span></h2>
      <p class="hero-desc text-center" style="margin-bottom: 30px;">Stream and download 1000+ songs</p>

      <div class="music-search-wrapper">
        <span class="search-icon">
          <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/>
          </svg>
        </span>
        <input type="text" class="music-search" id="musicSearch" placeholder="Search songs...">
      </div>

      <div class="music-container">
        <div class="music-header">
          <code>.play [song name]</code>
          <span>to play a song</span>
        </div>
        <div class="music-list" id="musicList"></div>
      </div>
    </div>

    <!-- DOWNLOAD TAB -->
    <div class="tab-panel" id="tab-download">
      <h2 class="hero-title text-center" style="font-size: 28px; margin-bottom: 8px;">Media <span>Downloader</span></h2>
      <p class="hero-desc text-center" style="margin-bottom: 30px;">Download from 15+ platforms</p>
      <div class="dl-grid" id="dlGrid"></div>
    </div>
  </div>

  <!-- Footer -->
  <footer class="footer">
    <div class="footer-content">
      <div class="footer-brand">
        <div class="footer-logo">S</div>
        <div>
          <div class="footer-name">Sixtus Terminal v40.0</div>
          <div class="footer-owner">Developed by Sixtus Weisly Nababan</div>
        </div>
      </div>
      <a href="https://wa.me/6283833526728" target="_blank" class="footer-contact">
        <span>Contact Developer</span>
      </a>
    </div>
  </footer>

  <!-- Toast -->
  <div class="toast" id="toast"></div>

  <style>
    @keyframes spin {
      to { transform: rotate(360deg); }
    }
  </style>

  <script>
    // =====================================================
    // SIXTUS TERMINAL v40.0 - DATA & LOGIC
    // =====================================================

    // Configuration
    const CONFIG = {
      owner: '6283833526728',
      name: 'Sixtus Weisly Nababan',
      bot: 'Sixtus Terminal v40.0',
      prefix: '.',
      version: '40.0'
    };

    // State
    const state = {
      connectionMethod: 'qr',
      connectionStatus: 'disconnected',
      pairingCode: '',
      startTime: Date.now(),
      messageCount: 0
    };

    // Game Data
    const gameCategories = [
      { name: 'Truth or Dare', icon: '🎯', color: '#ff6b6b', cmds: ['truth', 'dare', 'truth18', 'dare18', 'neverhaveiever', 'wouldyourather'] },
      { name: 'Casino', icon: '🎰', color: '#ffd43b', cmds: ['slot', 'casino', 'roulette', 'blackjack', 'poker', 'dice', 'coinflip', 'lottery'] },
      { name: 'Interactive', icon: '🎲', color: '#69db7c', cmds: ['tictactoe', 'tebakangka', 'math', 'quiz', 'rps', '8ball', 'wordle', 'hangman', 'trivia'] },
      { name: 'Economy', icon: '💰', color: '#4dabf7', cmds: ['rob', 'work', 'balance', 'bank', 'shop', 'buy', 'sell', 'daily', 'leaderboard', 'gamble'] },
      { name: 'Love Meter', icon: '💕', color: '#f783ac', cmds: ['lovecalc', 'ship', 'divorce', 'marry', 'couple', 'friendship', 'soulmate', 'match'] },
      { name: 'Rate', icon: '📊', color: '#b197fc', cmds: ['rate', 'keberuntungan', 'sange', 'gay', 'lesbi', 'pintar', 'handsome', 'beautiful', 'cool'] },
      { name: 'Fortune', icon: '🔮', color: '#63e6be', cmds: ['zodiac', 'horoscope', 'tarot', 'lucky', 'fortune', 'future', 'destiny', 'aura', 'numerology'] },
      { name: 'Fun Actions', icon: '🎉', color: '#ffa94d', cmds: ['slap', 'hug', 'kiss', 'pat', 'bite', 'poke', 'highfive', 'cuddle', 'tickle', 'bully', 'simp'] }
    ];

    // Tools Data
    const toolsCategories = [
      { name: 'Media Converter', icon: '🎬', color: '#a855f7', cmds: ['sticker', 'toimg', 'tomp3', 'tovideo', 'toaudio', 'togif', 'webm', 'flac', 'aac'] },
      { name: 'Document Tools', icon: '📄', color: '#3b82f6', cmds: ['topdf', 'todoc', 'docx', 'xlsx', 'pptx', 'txt', 'csv', 'pdf', 'compress'] },
      { name: 'Encode/Decode', icon: '🔐', color: '#10b981', cmds: ['base64', 'binary', 'hex', 'morse', 'rot13', 'atbash', 'urlencode', 'ascii', 'utf8'] },
      { name: 'Hash Generator', icon: '#️⃣', color: '#8b5cf6', cmds: ['hashmd5', 'hashsha1', 'hashsha256', 'hashsha512', 'bcrypt', 'crc32', 'hashverify'] },
      { name: 'Password Tools', icon: '🔑', color: '#84cc16', cmds: ['generatepassword', 'passwordstrength', 'uuid', 'passphrase', 'pincode', 'otp', 'token'] },
      { name: 'Math Calculator', icon: '🧮', color: '#06b6d4', cmds: ['calc', 'add', 'subtract', 'multiply', 'divide', 'sqrt', 'power', 'factorial', 'percentage'] },
      { name: 'Search Tools', icon: '🔍', color: '#f97316', cmds: ['google', 'wikipedia', 'wikihow', 'github', 'reddit', 'ytsearch', 'imagesearch', 'news'] },
      { name: 'QR & Barcode', icon: '📱', color: '#d946ef', cmds: ['qrcode', 'barcode', 'scanqr', 'readbarcode', 'qrcodewithlogo', 'qrcodewifi'] }
    ];

    // Downloader Data
    const downloaders = [
      { name: 'TikTok', cmd: '.tiktok', icon: 'TT', bg: '#000000' },
      { name: 'YouTube MP4', cmd: '.ytmp4', icon: 'YT', bg: '#dc2626' },
      { name: 'YouTube MP3', cmd: '.ytmp3', icon: 'YT', bg: '#dc2626' },
      { name: 'Instagram', cmd: '.ig', icon: 'IG', bg: 'linear-gradient(135deg, #8338ec, #e1306c, #fd1d1d)' },
      { name: 'Facebook', cmd: '.fb', icon: 'FB', bg: '#2563eb' },
      { name: 'Twitter', cmd: '.twitter', icon: 'X', bg: '#000000' },
      { name: 'Pinterest', cmd: '.pin', icon: 'PN', bg: '#dc2626' },
      { name: 'Spotify', cmd: '.spotify', icon: 'SP', bg: '#22c55e' },
      { name: 'SoundCloud', cmd: '.sc', icon: 'SC', bg: '#f97316' },
      { name: 'MediaFire', cmd: '.mf', icon: 'MF', bg: '#3b82f6' },
      { name: 'Google Drive', cmd: '.gdrive', icon: 'GD', bg: '#eab308' },
      { name: 'CapCut', cmd: '.capcut', icon: 'CC', bg: '#000000' }
    ];

    // Music Data
    const musicLibrary = [
      { title: 'Demons', artist: 'Imagine Dragons' },
      { title: 'Believer', artist: 'Imagine Dragons' },
      { title: 'Thunder', artist: 'Imagine Dragons' },
      { title: 'Radioactive', artist: 'Imagine Dragons' },
      { title: 'Enemy', artist: 'Imagine Dragons' },
      { title: 'Bones', artist: 'Imagine Dragons' },
      { title: 'Shape of You', artist: 'Ed Sheeran' },
      { title: 'Perfect', artist: 'Ed Sheeran' },
      { title: 'Blinding Lights', artist: 'The Weeknd' },
      { title: 'Starboy', artist: 'The Weeknd' },
      { title: 'Die For You', artist: 'The Weeknd' },
      { title: 'Bohemian Rhapsody', artist: 'Queen' },
      { title: 'Dont Stop Me Now', artist: 'Queen' },
      { title: 'Lose Yourself', artist: 'Eminem' },
      { title: 'Without Me', artist: 'Eminem' },
      { title: 'Rap God', artist: 'Eminem' },
      { title: 'Uptown Funk', artist: 'Bruno Mars' },
      { title: '24K Magic', artist: 'Bruno Mars' },
      { title: 'Faded', artist: 'Alan Walker' },
      { title: 'On My Way', artist: 'Alan Walker' },
      { title: 'Alone', artist: 'Alan Walker' },
      { title: 'Fix You', artist: 'Coldplay' },
      { title: 'Yellow', artist: 'Coldplay' },
      { title: 'Viva La Vida', artist: 'Coldplay' },
      { title: 'Someone Like You', artist: 'Adele' },
      { title: 'Hello', artist: 'Adele' },
      { title: 'Let It Be', artist: 'The Beatles' },
      { title: 'Yesterday', artist: 'The Beatles' }
    ];

    // Features Data
    const features = [
      { title: 'AI Upscaler', icon: 'AI', desc: 'Upscale images to 4K Ultra HD', color: '#a855f7', cmds: ['.hd', '.upscale'], tab: null },
      { title: 'Music Player', icon: 'MP', desc: 'Stream and download 1000+ songs', color: '#22c55e', cmds: ['.play', '.listmusic'], tab: 'music' },
      { title: 'Media Downloader', icon: 'DL', desc: 'Download from 15+ platforms', color: '#3b82f6', cmds: ['.tiktok', '.ytmp4', '.ig'], tab: 'download' },
      { title: 'Game Center', icon: 'GC', desc: '500+ interactive games', color: '#fb7185', cmds: ['.menugame'], tab: 'game' },
      { title: 'Group Manager', icon: 'GM', desc: 'Complete group administration', color: '#fbbf24', cmds: ['.menugroup'], tab: null },
      { title: 'Utility Tools', icon: 'UT', desc: '500+ converter tools', color: '#818cf8', cmds: ['.menutools'], tab: 'tools' }
    ];

    // Group Commands
    const groupCmds = ['kick', 'add', 'promote', 'demote', 'kickall', 'ban', 'unban', 'mute', 'unmute', 'warn', 'tagall', 'hidetag', 'setname', 'setdesc', 'linkgroup', 'revoke', 'antilink', 'antispam', 'welcome', 'goodbye', 'admins', 'members', 'groupinfo'];

    // =====================================================
    // UTILITY FUNCTIONS
    // =====================================================

    function $(id) { return document.getElementById(id); }

    function showTab(tabId) {
      document.querySelectorAll('.tab-panel').forEach(p => p.classList.remove('active'));
      document.querySelectorAll('.nav-tab').forEach(t => t.classList.remove('active'));
      $('tab-' + tabId).classList.add('active');
      document.querySelector(`.nav-tab[data-tab="${tabId}"]`)?.classList.add('active');
      $('mobileNav').value = tabId;
      
      if (tabId === 'home') animateCounters();
    }

    function showToast(msg) {
      const toast = $('toast');
      toast.textContent = msg;
      toast.classList.add('show');
      setTimeout(() => toast.classList.remove('show'), 2000);
    }

    function copyCmd(cmd) {
      navigator.clipboard.writeText(cmd);
      showToast('Copied: ' + cmd);
    }

    function log(msg, type = 'info') {
      const time = new Date().toLocaleTimeString();
      const output = $('terminalOutput');
      if (output) {
        const line = document.createElement('div');
        line.className = `log-line log-${type}`;
        line.innerHTML = `<span class="log-time">[${time}]</span> ${msg}`;
        output.appendChild(line);
        output.scrollTop = output.scrollHeight;
      }
    }

    // =====================================================
    // CONNECTION LOGIC
    // =====================================================

    function selectMethod(method) {
      state.connectionMethod = method;
      document.querySelectorAll('.method-card').forEach(c => c.classList.remove('active'));
      document.querySelector(`.method-card[data-method="${method}"]`).classList.add('active');
      $('phoneInput').classList.toggle('hidden', method !== 'pairing');
    }

    function initConnect() {
      if (state.connectionMethod === 'pairing') {
        const phone = $('phoneNumber').value.trim();
        if (!phone || phone.length < 10) {
          showToast('Enter a valid phone number');
          return;
        }
      }

      state.connectionStatus = 'connecting';
      updateUI();
      log('Initializing connection...', 'info');

      setTimeout(() => {
        if (state.connectionMethod === 'qr') {
          state.connectionStatus = 'qr_ready';
          log('QR Code generated', 'success');
        } else {
          state.connectionStatus = 'pairing_ready';
          state.pairingCode = Math.random().toString(36).substring(2, 10).toUpperCase();
          log(`Pairing code: ${state.pairingCode}`, 'success');
        }
        updateUI();
      }, 2000);
    }

    function cancelConnect() {
      state.connectionStatus = 'disconnected';
      log('Connection cancelled', 'warn');
      updateUI();
    }

    function disconnect() {
      state.connectionStatus = 'disconnected';
      state.pairingCode = '';
      log('Disconnected from WhatsApp', 'error');
      updateUI();
    }

    function copyPairing() {
      navigator.clipboard.writeText(state.pairingCode);
      showToast('Code copied: ' + state.pairingCode);
    }

    function updateUI() {
      const status = $('connectStatus');
      const statusText = $('connectStatusText');
      const globalStatus = $('globalStatus');
      const globalText = $('globalStatusText');

      // Panels
      ['initForm', 'qrPanel', 'pairingPanel', 'connectingPanel', 'connectedPanel'].forEach(p => $(p).classList.add('hidden'));

      status.classList.remove('connected', 'connecting');
      globalStatus.classList.remove('online');

      switch(state.connectionStatus) {
        case 'disconnected':
          statusText.textContent = 'Disconnected';
          $('initForm').classList.remove('hidden');
          globalText.textContent = 'Offline';
          break;

        case 'connecting':
          status.classList.add('connecting');
          statusText.textContent = 'Connecting...';
          globalStatus.classList.add('online');
          globalText.textContent = 'Connecting';
          $('connectingPanel').classList.remove('hidden');
          break;

        case 'qr_ready':
          status.classList.add('connecting');
          statusText.textContent = 'Scan QR';
          globalStatus.classList.add('online');
          globalText.textContent = 'QR Ready';
          $('qrPanel').classList.remove('hidden');
          $('qrImage').src = `https://api.qrserver.com/v1/create-qr-code/?size=200x200&bgcolor=0c1117&color=00e5a0&data=Sixtus_${Date.now()}`;
          break;

        case 'pairing_ready':
          status.classList.add('connecting');
          statusText.textContent = 'Enter Code';
          globalStatus.classList.add('online');
          globalText.textContent = 'Pairing';
          $('pairingPanel').classList.remove('hidden');
          $('pairingDigits').innerHTML = state.pairingCode.split('').map(d => `<div class="pairing-digit">${d}</div>`).join('');
          break;

        case 'connected':
          status.classList.add('connected');
          statusText.textContent = 'Connected';
          globalStatus.classList.add('online');
          globalText.textContent = 'Online';
          $('connectedPanel').classList.remove('hidden');
          $('connectedNumber').textContent = '+628xxx connected';
          break;
      }
    }

    // =====================================================
    // RENDER FUNCTIONS
    // =====================================================

    function renderFeatures() {
      const grid = $('featureGrid');
      grid.innerHTML = features.map(f => `
        <div class="feature-card" ${f.tab ? `onclick="showTab('${f.tab}')"` : ''} style="cursor: ${f.tab ? 'pointer' : 'default'}">
          <div class="feature-icon" style="background: ${f.color}20; color: ${f.color}; font-family: 'JetBrains Mono', monospace; font-weight: 700;">${f.icon}</div>
          <h3 class="feature-title">${f.title}</h3>
          <p class="feature-desc">${f.desc}</p>
          <div class="feature-cmds">
            ${f.cmds.map(c => `<span class="cmd-tag" onclick="event.stopPropagation(); copyCmd('${c}')">${c}</span>`).join('')}
          </div>
        </div>
      `).join('');
    }

    function renderGames() {
      const grid = $('gameGrid');
      grid.innerHTML = gameCategories.map(c => `
        <div class="feature-card">
          <div class="feature-icon" style="background: ${c.color}20; color: ${c.color};">${c.icon}</div>
          <h3 class="feature-title">${c.name}</h3>
          <div class="feature-cmds">
            ${c.cmds.map(cmd => `<span class="cmd-tag" onclick="copyCmd('.${cmd}')">.${cmd}</span>`).join('')}
          </div>
        </div>
      `).join('');
    }

    function renderTools() {
      const grid = $('toolsGrid');
      grid.innerHTML = toolsCategories.map(c => `
        <div class="feature-card">
          <div class="feature-icon" style="background: ${c.color}20; color: ${c.color};">${c.icon}</div>
          <h3 class="feature-title">${c.name}</h3>
          <div class="feature-cmds">
            ${c.cmds.map(cmd => `<span class="cmd-tag" onclick="copyCmd('.${cmd}')">.${cmd}</span>`).join('')}
          </div>
        </div>
      `).join('');
    }

    function renderDownloaders() {
      const grid = $('dlGrid');
      grid.innerHTML = downloaders.map(d => `
        <div class="dl-card" style="background: ${d.bg};" onclick="copyCmd('${d.cmd}')">
          <div class="dl-icon" style="font-family: 'JetBrains Mono', monospace; font-weight: 700;">${d.icon}</div>
          <div class="dl-name">${d.name}</div>
          <div class="dl-cmd">${d.cmd}</div>
        </div>
      `).join('');
    }

    function renderMusic() {
      const list = $('musicList');
      list.innerHTML = musicLibrary.map((m, i) => `
        <div class="music-item" onclick="copyCmd('.play ${m.title}')">
          <span class="music-num">${String(i + 1).padStart(2, '0')}</span>
          <div class="music-info">
            <div class="music-title">${m.title}</div>
            <div class="music-artist">${m.artist}</div>
          </div>
        </div>
      `).join('');
    }

    function loadCommands(category) {
      document.querySelectorAll('.sidebar-item').forEach(item => item.classList.remove('active'));
      event.target.closest('.sidebar-item')?.classList.add('active');

      const grid = $('cmdGrid');
      const title = $('panelTitle');
      let cmds = [];

      const allGameCmds = gameCategories.flatMap(c => c.cmds.map(cmd => ({ cmd, cat: c.name })));
      const allToolsCmds = toolsCategories.flatMap(c => c.cmds.map(cmd => ({ cmd, cat: c.name })));
      const allDlCmds = downloaders.map(d => ({ cmd: d.cmd.replace('.', ''), cat: 'Downloader' }));

      switch(category) {
        case 'all':
          title.textContent = 'All Commands';
          cmds = [...allGameCmds, ...allToolsCmds, ...groupCmds.map(c => ({ cmd: c, cat: 'Group' })), ...allDlCmds];
          break;
        case 'game':
          title.textContent = 'Game Commands';
          cmds = allGameCmds;
          break;
        case 'group':
          title.textContent = 'Group Commands';
          cmds = groupCmds.map(c => ({ cmd: c, cat: 'Group' }));
          break;
        case 'tools':
          title.textContent = 'Tools Commands';
          cmds = allToolsCmds;
          break;
        case 'downloader':
          title.textContent = 'Downloader Commands';
          cmds = allDlCmds;
          break;
        case 'music':
          title.textContent = 'Music Commands';
          cmds = ['play', 'listmusic', 'search', 'nowplaying', 'skip', 'pause', 'resume', 'queue', 'volume'].map(c => ({ cmd: c, cat: 'Music' }));
          break;
      }

      grid.innerHTML = cmds.map(c => `
        <span class="cmd-tag" onclick="copyCmd('.${c.cmd}')">.${c.cmd}</span>
      `).join('');
    }

    function filterCmds() {
      const search = $('cmdSearch').value.toLowerCase();
      document.querySelectorAll('#cmdGrid .cmd-tag').forEach(tag => {
        const text = tag.textContent.toLowerCase();
        tag.style.display = text.includes(search) ? 'inline-flex' : 'none';
      });
    }

    // =====================================================
    // ANIMATIONS
    // =====================================================

    function animateCounters() {
      document.querySelectorAll('.hero-stat-value').forEach(el => {
        const target = parseInt(el.dataset.count);
        if (!target || el.dataset.animated) return;
        el.dataset.animated = 'true';

        const duration = 2000;
        const start = performance.now();

        function update(now) {
          const elapsed = now - start;
          const progress = Math.min(elapsed / duration, 1);
          const eased = 1 - Math.pow(1 - progress, 3);
          el.textContent = Math.floor(eased * target).toLocaleString() + '+';
          if (progress < 1) requestAnimationFrame(update);
        }
        requestAnimationFrame(update);
      });
    }

    function updateUptime() {
      const elapsed = Date.now() - state.startTime;
      const h = String(Math.floor(elapsed / 3600000)).padStart(2, '0');
      const m = String(Math.floor((elapsed % 3600000) / 60000)).padStart(2, '0');
      const s = String(Math.floor((elapsed % 60000) / 1000)).padStart(2, '0');
      const el = $('sidebarUptime');
      if (el) el.textContent = `${h}:${m}:${s}`;
    }

    // =====================================================
    // EVENT LISTENERS
    // =====================================================

    document.querySelectorAll('.nav-tab').forEach(tab => {
      tab.addEventListener('click', () => showTab(tab.dataset.tab));
    });

    $('mobileNav').addEventListener('change', e => showTab(e.target.value));

    $('musicSearch').addEventListener('input', e => {
      const search = e.target.value.toLowerCase();
      document.querySelectorAll('.music-item').forEach(item => {
        const title = item.querySelector('.music-title').textContent.toLowerCase();
        const artist = item.querySelector('.music-artist').textContent.toLowerCase();
        item.style.display = (title.includes(search) || artist.includes(search)) ? 'flex' : 'none';
      });
    });

    // =====================================================
    // INITIALIZATION
    // =====================================================

    function init() {
      renderFeatures();
      renderGames();
      renderTools();
      renderDownloaders();
      renderMusic();
      loadCommands('all');

      log('Sixtus Terminal v40.0 initialized', 'success');
      log('Ready for connection', 'info');

      setInterval(updateUptime, 1000);

      // Simulate messages
      setInterval(() => {
        if (state.connectionStatus === 'connected') {
          state.messageCount += Math.floor(Math.random() * 3);
          $('sidebarMessages').textContent = state.messageCount;
        }
      }, 5000);
    }

    init();
  </script>
</body>
</html>
