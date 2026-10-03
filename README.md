<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>mrstoud - منصة الأفلام والمسلسلات الآمنة</title>
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  <style>
    :root {
      --primary-color: #e50914;
      --primary-hover: #b80710;
      --bg-color: #0f0f0f;
      --card-bg: #1c1c1c;
      --text-color: #ffffff;
      --text-secondary: #aaa;
      --sidebar-bg: #141414;
      --border-color: #2a2a2a;
    }

    [data-theme="light"] {
      --primary-color: #e50914;
      --primary-hover: #b80710;
      --bg-color: #f4f4f4;
      --card-bg: #ffffff;
      --text-color: #111111;
      --text-secondary: #666;
      --sidebar-bg: #ffffff;
      --border-color: #ddd;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      -webkit-tap-highlight-color: transparent;
    }

    body {
      background-color: var(--bg-color);
      color: var(--text-color);
      direction: rtl;
      padding-bottom: 30px;
      transition: background-color 0.3s, color 0.3s;
    }

    /* Floating Welcome Banner */
    .welcome-banner-top {
      background: linear-gradient(135deg, var(--primary-color), #ff4757);
      color: #fff;
      padding: 10px 20px;
      text-align: center;
      font-size: 13px;
      font-weight: bold;
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 10px;
      position: relative;
      z-index: 101;
      box-shadow: 0 2px 8px rgba(0,0,0,0.3);
    }
    .welcome-banner-top button {
      background: rgba(255,255,255,0.2);
      border: none;
      color: #fff;
      padding: 3px 8px;
      border-radius: 4px;
      cursor: pointer;
      font-size: 11px;
    }

    /* Blocked Hacker Screen */
    #hackerBlockedScreen {
      display: none;
      position: fixed;
      top: 0; left: 0; width: 100vw; height: 100vh;
      background-color: #0d0000;
      color: #ff3333;
      z-index: 99999;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 20px;
    }

    #hackerBlockedScreen i {
      font-size: 80px;
      margin-bottom: 20px;
      animation: pulse 1.5s infinite;
    }

    @keyframes pulse {
      0% { transform: scale(1); opacity: 0.8; }
      50% { transform: scale(1.1); opacity: 1; }
      100% { transform: scale(1); opacity: 0.8; }
    }

    /* Navbar */
    .navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background-color: var(--sidebar-bg);
      padding: 12px 18px;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
      border-bottom: 1px solid var(--border-color);
    }

    .brand {
      font-size: 24px;
      font-weight: 800;
      color: var(--primary-color);
      text-decoration: none;
      letter-spacing: 1px;
    }

    .nav-actions {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .icon-btn {
      background: none;
      border: none;
      color: var(--text-color);
      font-size: 20px;
      padding: 8px;
      cursor: pointer;
      border-radius: 50%;
      transition: background 0.2s, color 0.2s;
      position: relative;
    }

    .icon-btn:hover, .icon-btn:active {
      background-color: var(--border-color);
      color: var(--primary-color);
    }

    /* Breaking News Ticker Bar */
    .ticker-bar {
      background-color: var(--card-bg);
      border-bottom: 1px solid var(--border-color);
      color: var(--text-color);
      padding: 8px 15px;
      font-size: 13px;
      display: flex;
      align-items: center;
      overflow: hidden;
      white-space: nowrap;
      position: sticky;
      top: 61px;
      z-index: 99;
    }

    .ticker-title {
      background-color: var(--primary-color);
      color: #fff;
      padding: 3px 8px;
      border-radius: 4px;
      font-size: 11px;
      font-weight: bold;
      margin-left: 12px;
      display: flex;
      align-items: center;
      gap: 5px;
    }

    .ticker-content {
      display: inline-block;
      animation: tickerScroll 20s linear infinite;
      color: var(--text-secondary);
    }

    @keyframes tickerScroll {
      0% { transform: translateX(100%); }
      100% { transform: translateX(-100%); }
    }

    /* Sidebar */
    .sidebar {
      position: fixed;
      top: 0;
      right: -320px;
      width: 300px;
      height: 100%;
      background-color: var(--sidebar-bg);
      box-shadow: -4px 0 15px rgba(0, 0, 0, 0.4);
      transition: right 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      z-index: 200;
      padding: 20px 15px;
      display: flex;
      flex-direction: column;
      overflow-y: auto;
    }

    .sidebar.open {
      right: 0;
    }

    .sidebar-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 15px;
      margin-bottom: 15px;
    }

    .sidebar-header h3 {
      font-size: 20px;
      color: var(--primary-color);
    }

    /* Sidebar Search Box */
    .sidebar-search-box {
      margin-bottom: 15px;
      position: relative;
      display: flex;
      gap: 6px;
    }

    .sidebar-search-input {
      width: 100%;
      padding: 10px 12px 10px 35px;
      border-radius: 6px;
      border: 1px solid var(--border-color);
      background-color: var(--card-bg);
      color: var(--text-color);
      font-size: 14px;
      outline: none;
    }

    .sidebar-search-input:focus {
      border-color: var(--primary-color);
    }

    .sidebar-search-icon {
      position: absolute;
      left: 10px;
      top: 50%;
      transform: translateY(-50%);
      color: var(--text-secondary);
      font-size: 14px;
    }

    .sidebar-menu {
      list-style: none;
    }

    .sidebar-menu li {
      margin-bottom: 8px;
    }

    .sidebar-menu a, .sidebar-menu button {
      color: var(--text-color);
      text-decoration: none;
      font-size: 15px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 12px;
      border-radius: 6px;
      background: none;
      border: none;
      cursor: pointer;
      width: 100%;
      text-align: right;
      transition: background 0.2s, color 0.2s;
    }

    .sidebar-menu-left {
      display: flex;
      align-items: center;
      gap: 12px;
    }

    .sidebar-menu a:hover, .sidebar-menu button:hover, .sidebar-menu a.active-link {
      background-color: var(--border-color);
      color: var(--primary-color);
    }

    .badge-count {
      background-color: var(--border-color);
      color: var(--text-secondary);
      font-size: 11px;
      padding: 2px 7px;
      border-radius: 10px;
    }

    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.6);
      backdrop-filter: blur(2px);
      display: none;
      z-index: 150;
    }

    .overlay.active {
      display: block;
    }

    /* Main Header Title */
    .section-title {
      font-size: 20px;
      font-weight: bold;
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      color: var(--text-color);
      border-right: 4px solid var(--primary-color);
      padding-right: 10px;
    }

    /* Main Container & Grid */
    .container {
      max-width: 1200px;
      margin: 15px auto;
      padding: 0 12px;
    }

    .ad-banner {
      background: linear-gradient(135deg, var(--card-bg), var(--sidebar-bg));
      border: 1px dashed var(--primary-color);
      color: var(--text-secondary);
      text-align: center;
      padding: 14px;
      margin-bottom: 20px;
      border-radius: 8px;
      font-size: 13px;
    }

    .shows-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(145px, 1fr));
      gap: 14px;
    }

    @media (min-width: 600px) {
      .shows-grid {
        grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
        gap: 18px;
      }
    }

    .show-card {
      background-color: var(--card-bg);
      border-radius: 8px;
      overflow: hidden;
      position: relative;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      transition: transform 0.2s;
      cursor: pointer;
      border: 1px solid var(--border-color);
    }

    .show-card:hover {
      transform: translateY(-4px);
    }

    .show-badge {
      position: absolute;
      top: 8px;
      right: 8px;
      background-color: var(--primary-color);
      color: #fff;
      padding: 3px 7px;
      font-size: 11px;
      border-radius: 4px;
      font-weight: bold;
      z-index: 2;
    }

    .show-type-tag {
      position: absolute;
      top: 8px;
      left: 8px;
      background-color: rgba(0, 0, 0, 0.75);
      color: #fff;
      padding: 3px 7px;
      font-size: 10px;
      border-radius: 4px;
      z-index: 2;
      border: 1px solid rgba(255,255,255,0.2);
    }

    .show-thumb {
      width: 100%;
      height: 220px;
      object-fit: cover;
      display: block;
    }

    @media (min-width: 600px) {
      .show-thumb {
        height: 260px;
      }
    }

    .show-info {
      padding: 10px;
      text-align: center;
    }

    .show-title {
      font-size: 14px;
      font-weight: 600;
      color: var(--text-color);
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    .meta-sub-info {
      display: flex;
      justify-content: center;
      gap: 10px;
      font-size: 11px;
      color: var(--text-secondary);
      margin-top: 4px;
    }

    /* Modals */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.8);
      z-index: 300;
      justify-content: center;
      align-items: center;
      padding: 15px;
    }

    .modal.active {
      display: flex;
    }

    .modal-content {
      background-color: var(--card-bg);
      color: var(--text-color);
      border-radius: 10px;
      max-width: 650px;
      width: 100%;
      padding: 20px;
      box-shadow: 0 8px 24px rgba(0,0,0,0.5);
      max-height: 90vh;
      overflow-y: auto;
      border: 1px solid var(--border-color);
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 18px;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 10px;
    }

    .close-btn {
      background: none;
      border: none;
      color: var(--text-color);
      font-size: 22px;
      cursor: pointer;
    }

    /* Security Notice Banner */
    .admin-warning-box {
      background-color: rgba(229, 9, 20, 0.15);
      border: 1px solid var(--primary-color);
      color: #ff6b6b;
      padding: 12px;
      border-radius: 6px;
      font-size: 12px;
      margin-bottom: 15px;
      display: flex;
      align-items: center;
      gap: 10px;
      line-height: 1.5;
    }

    .admin-warning-box i {
      font-size: 20px;
      color: var(--primary-color);
    }

    .lockout-msg {
      color: #ff4d4d;
      font-size: 13px;
      margin-top: 10px;
      text-align: center;
      font-weight: bold;
    }

    /* Admin Tabs */
    .admin-tabs {
      display: flex;
      gap: 8px;
      margin-bottom: 20px;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 10px;
      overflow-x: auto;
    }

    .tab-btn {
      background: var(--sidebar-bg);
      border: 1px solid var(--border-color);
      color: var(--text-secondary);
      padding: 8px 14px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
      white-space: nowrap;
      transition: all 0.2s;
    }

    .tab-btn.active {
      background: var(--primary-color);
      color: #fff;
      border-color: var(--primary-color);
    }

    .tab-content {
      display: none;
    }

    .tab-content.active {
      display: block;
    }

    .form-group {
      margin-bottom: 14px;
    }

    .form-group label {
      display: block;
      margin-bottom: 6px;
      font-size: 13px;
      color: var(--text-secondary);
    }

    .form-group input, .form-group select, .form-group textarea {
      width: 100%;
      padding: 10px 12px;
      border-radius: 6px;
      border: 1px solid var(--border-color);
      background-color: var(--sidebar-bg);
      color: var(--text-color);
      font-size: 14px;
      outline: none;
    }

    .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
      border-color: var(--primary-color);
    }

    .btn {
      width: 100%;
      padding: 12px;
      background-color: var(--primary-color);
      color: #fff;
      border: none;
      border-radius: 6px;
      font-size: 15px;
      cursor: pointer;
      font-weight: bold;
      transition: background 0.2s;
    }

    .btn:disabled {
      background-color: #555;
      cursor: not-allowed;
    }

    .btn:hover:not(:disabled) {
      background-color: var(--primary-hover);
    }

    .btn-secondary {
      background-color: #333;
      margin-top: 8px;
    }

    .btn-secondary:hover {
      background-color: #444;
    }

    /* Users & Ban List Styling */
    .user-card {
      background-color: var(--sidebar-bg);
      border: 1px solid var(--border-color);
      padding: 12px;
      border-radius: 6px;
      margin-bottom: 10px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 10px;
    }

    .user-info {
      display: flex;
      flex-direction: column;
      gap: 4px;
    }

    .user-name {
      font-size: 14px;
      font-weight: bold;
      color: var(--text-color);
    }

    .user-email {
      font-size: 12px;
      color: var(--text-secondary);
    }

    .status-badge {
      font-size: 11px;
      padding: 3px 8px;
      border-radius: 4px;
      display: inline-block;
      width: fit-content;
    }

    .status-active { background-color: #27ae60; color: #fff; }
    .status-banned { background-color: #c0392b; color: #fff; }

    /* Video Player Modal Elements */
    .video-container {
      position: relative;
      padding-bottom: 56.25%;
      height: 0;
      overflow: hidden;
      border-radius: 8px;
      background-color: #000;
      margin-bottom: 15px;
    }

    .video-container iframe, .video-container video {
      position: absolute;
      top: 0; left: 0; width: 100%; height: 100%; border: 0;
    }

    .video-details {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .quality-tags {
      display: flex;
      gap: 8px;
      align-items: center;
      flex-wrap: wrap;
    }

    .quality-tag {
      background-color: var(--sidebar-bg);
      color: var(--text-color);
      padding: 4px 8px;
      border-radius: 4px;
      font-size: 12px;
      border: 1px solid var(--border-color);
    }

    .download-btn {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 8px;
      background-color: #27ae60;
      color: white;
      text-decoration: none;
      padding: 12px;
      border-radius: 6px;
      font-weight: bold;
      font-size: 14px;
      text-align: center;
    }

    .download-btn:hover { background-color: #219150; }

    .admin-item {
      display: flex;
      align-items: center;
      justify-content: space-between;
      background-color: var(--sidebar-bg);
      padding: 10px;
      border-radius: 6px;
      margin-bottom: 10px;
      border: 1px solid var(--border-color);
    }

    .admin-item-title {
      font-size: 14px;
      font-weight: 500;
      max-width: 60%;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
      color: var(--text-color);
    }

    .admin-actions { display: flex; gap: 8px; }

    .sm-btn {
      padding: 6px 10px;
      font-size: 12px;
      border-radius: 4px;
      border: none;
      cursor: pointer;
      color: white;
    }

    .btn-edit { background-color: #2980b9; }
    .btn-del { background-color: #c0392b; }
    .btn-ban { background-color: #e67e22; }
    .btn-unban { background-color: #27ae60; }

    /* Multi-Server & Features CSS */
    .server-btn-group {
      display: flex;
      gap: 8px;
      margin-bottom: 12px;
      flex-wrap: wrap;
    }

    .server-btn {
      background: var(--sidebar-bg);
      border: 1px solid var(--border-color);
      color: var(--text-color);
      padding: 8px 14px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
      transition: all 0.2s;
    }

    .server-btn.active, .server-btn:hover {
      background: var(--primary-color);
      border-color: var(--primary-color);
      color: #fff;
    }

    /* Episodes List Style */
    .episodes-section {
      background: var(--sidebar-bg);
      border: 1px solid var(--border-color);
      border-radius: 8px;
      padding: 12px;
      margin-bottom: 15px;
    }
    .episodes-title {
      font-size: 14px;
      font-weight: bold;
      color: var(--primary-color);
      margin-bottom: 10px;
      display: flex;
      align-items: center;
      gap: 6px;
    }
    .episodes-grid {
      display: flex;
      gap: 8px;
      flex-wrap: wrap;
      max-height: 120px;
      overflow-y: auto;
    }
    .episode-chip {
      background: var(--card-bg);
      border: 1px solid var(--border-color);
      color: var(--text-color);
      padding: 6px 12px;
      border-radius: 6px;
      font-size: 12px;
      cursor: pointer;
      transition: 0.2s;
    }
    .episode-chip.active, .episode-chip:hover {
      background: var(--primary-color);
      border-color: var(--primary-color);
      color: #fff;
    }

    /* Player Tools Bar */
    .player-tools-bar {
      background: var(--sidebar-bg);
      border: 1px solid var(--border-color);
      border-radius: 8px;
      padding: 12px;
      margin-bottom: 15px;
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .tool-row {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 10px;
      flex-wrap: wrap;
    }

    .tool-group {
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 13px;
      color: var(--text-secondary);
    }

    .tool-group select, .tool-group input[type="range"] {
      background: var(--card-bg);
      color: var(--text-color);
      border: 1px solid var(--border-color);
      padding: 5px 8px;
      border-radius: 4px;
      font-size: 12px;
      outline: none;
    }

    .slider-container {
      display: flex;
      align-items: center;
      gap: 6px;
      font-size: 12px;
      color: var(--text-secondary);
    }

    .slider-container input {
      width: 90px;
      accent-color: var(--primary-color);
    }

    .comments-section {
      margin-top: 20px;
      border-top: 1px solid var(--border-color);
      padding-top: 15px;
    }

    .comments-title {
      font-size: 16px;
      font-weight: bold;
      margin-bottom: 12px;
      color: var(--primary-color);
    }

    .comment-item {
      background: var(--sidebar-bg);
      border: 1px solid var(--border-color);
      padding: 10px 12px;
      border-radius: 6px;
      margin-bottom: 8px;
      font-size: 13px;
    }

    .comment-header {
      display: flex;
      justify-content: space-between;
      color: var(--text-secondary);
      font-size: 11px;
      margin-bottom: 4px;
    }

    .extra-player-actions {
      display: flex;
      gap: 10px;
      margin-top: 12px;
      align-items: center;
      justify-content: space-between;
      flex-wrap: wrap;
    }

    .action-badge-btn {
      background: var(--sidebar-bg);
      border: 1px solid var(--border-color);
      color: var(--text-color);
      padding: 8px 12px;
      border-radius: 6px;
      cursor: pointer;
      font-size: 13px;
      display: flex;
      align-items: center;
      gap: 6px;
      transition: 0.2s;
    }

    .action-badge-btn:hover {
      border-color: var(--primary-color);
      color: var(--primary-color);
    }

    .star-rating {
      display: flex;
      gap: 4px;
      cursor: pointer;
      font-size: 18px;
      color: #ccc;
    }

    .star-rating .star.rated {
      color: #f1c40f;
    }

    .filters-bar {
      display: flex;
      gap: 10px;
      margin-bottom: 15px;
      overflow-x: auto;
      padding-bottom: 5px;
    }
    .filter-chip {
      background: var(--card-bg);
      border: 1px solid var(--border-color);
      color: var(--text-secondary);
      padding: 6px 14px;
      border-radius: 20px;
      font-size: 13px;
      cursor: pointer;
      white-space: nowrap;
      transition: 0.2s;
    }
    .filter-chip.active, .filter-chip:hover {
      background: var(--primary-color);
      color: #fff;
      border-color: var(--primary-color);
    }
    .cinema-mode body {
      background-color: #000 !important;
    }
    .speed-badge {
      background: var(--sidebar-bg);
      border: 1px solid var(--border-color);
      color: var(--text-color);
      padding: 5px 10px;
      border-radius: 4px;
      font-size: 12px;
      cursor: pointer;
    }
    .download-progress-container {
      margin-top: 10px;
      background: var(--sidebar-bg);
      border: 1px solid var(--border-color);
      border-radius: 6px;
      padding: 8px;
      display: none;
    }
    .progress-bar-track {
      width: 100%;
      height: 6px;
      background: var(--border-color);
      border-radius: 3px;
      overflow: hidden;
      margin-top: 5px;
    }
    .progress-bar-fill {
      width: 0%;
      height: 100%;
      background: #27ae60;
      transition: width 0.3s;
    }

    .toast-notification {
      position: fixed;
      bottom: 25px;
      left: 25px;
      background: #1f1f1f;
      color: #fff;
      border: 1px solid var(--primary-color);
      padding: 12px 20px;
      border-radius: 8px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.5);
      z-index: 9999;
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 14px;
      transform: translateY(100px);
      opacity: 0;
      transition: 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }
    .toast-notification.show {
      transform: translateY(0);
      opacity: 1;
    }
    .accent-picker {
      display: flex;
      gap: 6px;
      align-items: center;
    }
    .color-dot {
      width: 20px;
      height: 20px;
      border-radius: 50%;
      cursor: pointer;
      border: 2px solid transparent;
    }
    .color-dot.active { border-color: #fff; }

    .notif-badge-counter {
      position: absolute;
      top: 3px;
      left: 3px;
      background: var(--primary-color);
      color: #fff;
      font-size: 9px;
      padding: 2px 5px;
      border-radius: 50%;
      font-weight: bold;
    }
    .scroll-to-top {
      position: fixed;
      bottom: 25px;
      right: 25px;
      background: var(--primary-color);
      color: #fff;
      border: none;
      width: 42px;
      height: 42px;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      align-items: center;
      justify-content: center;
      z-index: 90;
      box-shadow: 0 4px 10px rgba(0,0,0,0.3);
      font-size: 16px;
      transition: 0.2s;
    }
    .scroll-to-top:hover { transform: scale(1.1); }
  </style>
</head>
<body>

  <!-- زر العودة للأعلى -->
  <button class="scroll-to-top" id="scrollToTopBtn" onclick="scrollToTop()" title="العودة لأعلى الصفحة"><i class="fas fa-arrow-up"></i></button>

  <!-- رسالة الترحيب العلوية -->
  <div class="welcome-banner-top" id="topWelcomeBanner">
    <span>🎬 أهلاً بك في <strong>mrstoud</strong>! وجهتك الأولى لمشاهدة أحدث الأفلام والمسلسلات بجودة عالية وأمان تام.</span>
    <button onclick="closeTopWelcome()">إخفاء</button>
  </div>

  <!-- Toast Notification System -->
  <div class="toast-notification" id="toastNotification">
    <i class="fas fa-check-circle" style="color: #27ae60; font-size: 18px;"></i>
    <span id="toastMessage">تم بنجاح!</span>
  </div>

  <!-- Hacker Blocked Overlay Screen -->
  <div id="hackerBlockedScreen">
    <i class="fas fa-user-ninja"></i>
    <h1 style="font-size: 28px; margin-bottom: 10px;">تم اكتشاف محاولة اختراق!</h1>
    <p style="color: #ccc; max-width: 500px; font-size: 15px; line-height: 1.6;">
      تم حظر جهازك ومعرفك فوراً بواسطة جدار حماية المنصة (MRSTOUD Firewall WAF). يُمنع منعاً باتاً الوصول إلى أي جزء من الموقع.
    </p>
    <div style="margin-top: 25px; font-size: 12px; color: #777;">
      IP status: <span style="color: red;">PERMANENTLY BANNED</span>
    </div>
  </div>

  <!-- Navigation Bar -->
  <nav class="navbar">
    <a href="#" class="brand" onclick="filterByCategory('all')">mrstoud</a>
    <div class="nav-actions">
      <!-- زر حساب المستخدم الجديد -->
      <button class="icon-btn" onclick="openAuthOrProfileModal()" title="حساب المستخدم وتسجيل الدخول">
        <i class="fas fa-user-circle" id="navUserIcon"></i>
      </button>

      <!-- زر الإشعارات -->
      <button class="icon-btn" onclick="openNotificationsModal()" title="الإشعارات والتنبيهات">
        <i class="fas fa-bell"></i>
        <span class="notif-badge-counter" id="notifBadge">1</span>
      </button>

      <div class="accent-picker" title="اختر لون المنصة">
        <div class="color-dot active" style="background:#e50914;" onclick="changeAccentColor('#e50914')"></div>
        <div class="color-dot" style="background:#3498db;" onclick="changeAccentColor('#3498db')"></div>
        <div class="color-dot" style="background:#27ae60;" onclick="changeAccentColor('#27ae60')"></div>
        <div class="color-dot" style="background:#9b59b6;" onclick="changeAccentColor('#9b59b6')"></div>
      </div>
      <button class="icon-btn" id="cinemaModeBtn" title="وضع السينما المظلم"><i class="fas fa-theater-masks"></i></button>
      <button class="icon-btn" id="themeToggleBtn" title="تبديل المظهر (ليلي/نهاري)"><i class="fas fa-moon" id="themeIcon"></i></button>
      <button class="icon-btn" id="menuToggleBtn" title="القائمة الجانبية"><i class="fas fa-bars"></i></button>
    </div>
  </nav>

  <!-- Breaking News Ticker Bar -->
  <div class="ticker-bar">
    <div class="ticker-title"><i class="fas fa-bullhorn"></i> إعلان عاجل</div>
    <div class="ticker-content">
      مرحباً بكم في منصة mrstoud للأفلام والمسلسلات الحصرية. استمتع بأعلى جودة مشاهدة وأحدث الإصدارات مع حماية أمنية متكاملة WAF!
    </div>
  </div>

  <!-- Sidebar Overlay -->
  <div class="overlay" id="overlay"></div>

  <!-- Sidebar -->
  <aside class="sidebar" id="sidebar">
    <div class="sidebar-header">
      <h3>mrstoud</h3>
      <button class="close-btn" id="closeSidebarBtn">&times;</button>
    </div>

    <!-- Sidebar Search Box -->
    <div class="sidebar-search-box">
      <input type="text" class="sidebar-search-input" id="sidebarSearchInput" placeholder="بحث عن فيلم أو مسلسل...">
      <button class="icon-btn" id="voiceSearchBtn" onclick="startVoiceSearch()" title="بحث صوتي ذكي" style="font-size:16px; padding:6px;"><i class="fas fa-microphone"></i></button>
      <i class="fas fa-search sidebar-search-icon"></i>
    </div>

    <ul class="sidebar-menu">
      <li>
        <a href="#" class="active-link" onclick="filterByCategory('all', event)">
          <div class="sidebar-menu-left"><i class="fas fa-home"></i> الرئيسية</div>
          <span class="badge-count" id="countAll">0</span>
        </a>
      </li>
      <li>
        <a href="#" onclick="filterByCategory('series', event)">
          <div class="sidebar-menu-left"><i class="fas fa-tv"></i> المسلسلات</div>
          <span class="badge-count" id="countSeries">0</span>
        </a>
      </li>
      <li>
        <a href="#" onclick="filterByCategory('movie', event)">
          <div class="sidebar-menu-left"><i class="fas fa-film"></i> الأفلام</div>
          <span class="badge-count" id="countMovies">0</span>
        </a>
      </li>
      <li>
        <a href="#" onclick="filterByCategory('kids', event)">
          <div class="sidebar-menu-left"><i class="fas fa-child" style="color:#f1c40f;"></i> وضع الأطفال الآمن</div>
        </a>
      </li>
      <li>
        <a href="#" onclick="filterByCategory('favorites', event)">
          <div class="sidebar-menu-left"><i class="fas fa-heart" style="color:var(--primary-color);"></i> المفضلة</div>
          <span class="badge-count" id="countFavorites">0</span>
        </a>
      </li>
      <li>
        <a href="#" onclick="filterByCategory('history', event)">
          <div class="sidebar-menu-left"><i class="fas fa-history"></i> سجل المشاهدة</div>
        </a>
      </li>
      <li>
        <a href="#" onclick="filterByCategory('watchlist', event)">
          <div class="sidebar-menu-left"><i class="fas fa-clock"></i> المشاهدة لاحقاً</div>
          <span class="badge-count" id="countWatchlist">0</span>
        </a>
      </li>
      <li>
        <a href="#" onclick="openAnalyticsModal()">
          <div class="sidebar-menu-left"><i class="fas fa-chart-pie" style="color:#f39c12;"></i> إحصائيات المشاهدة</div>
        </a>
      </li>
      <li>
        <a href="#" id="privacyBtn">
          <div class="sidebar-menu-left"><i class="fas fa-user-lock"></i> سياسة الخصوصية</div>
        </a>
      </li>
      <hr style="border-color: var(--border-color); margin: 15px 0;">
      <li><button id="adminBtn"><div class="sidebar-menu-left"><i class="fas fa-user-shield"></i> الإدارة</div></button></li>
    </ul>
  </aside>

  <!-- Main Content -->
  <main class="container">
    <div class="ad-banner">
      <p>📢 مساحة إعلانية - ضع كود الإعلان الخاص بك هنا (AdSense / Native Ads)</p>
    </div>

    <div class="filters-bar" id="genresFilterBar">
      <div class="filter-chip active" onclick="filterByGenre('all', this)">الكل</div>
      <div class="filter-chip" onclick="filterByGenre('action', this)">أكشن ومغامرة</div>
      <div class="filter-chip" onclick="filterByGenre('drama', this)">دراما وتشويق</div>
      <div class="filter-chip" onclick="filterByGenre('comedy', this)">كوميدي</div>
      <div class="filter-chip" onclick="filterByGenre('scifi', this)">خيال علمي</div>
    </div>

    <div class="section-title" id="sectionTitle">
      <span><i class="fas fa-play-circle"></i> جميع الأعمال</span>
      <button onclick="playRandomShow()" class="action-badge-btn" style="padding: 5px 10px; font-size: 12px;"><i class="fas fa-dice"></i> اقتراح عشوائي</button>
    </div>

    <div class="shows-grid" id="showsGrid"></div>
  </main>

  <!-- Welcome Modal -->
  <div class="modal" id="welcomeModal">
    <div class="modal-content" style="text-align: center; max-width: 450px;">
      <i class="fas fa-film" style="font-size: 50px; color: var(--primary-color); margin-bottom: 15px;"></i>
      <h2 style="margin-bottom: 10px; color: var(--text-color);">مرحباً بك في منصة mrstoud!</h2>
      <p style="color: var(--text-secondary); font-size: 14px; line-height: 1.6; margin-bottom: 20px;">
        يسعدنا انضمامك إلينا. يمكنك الآن مشاهدة أحدث الأفلام والمسلسلات عالية الجودة بكل أمان وسهولة. نتمنى لك تجربة ممتعة!
      </p>
      <button class="btn closeModal">ابدأ المشاهدة الآن</button>
    </div>
  </div>

  <!-- ميزة تسجيل الدخول وحساب المستخدمين الجديد (Auth Modal) -->
  <div class="modal" id="authModal">
    <div class="modal-content" style="max-width: 420px;">
      <div class="modal-header">
        <h3><i class="fas fa-user-circle"></i> بوابة حساب المستخدم</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <div class="admin-tabs">
        <button class="tab-btn active" onclick="switchAuthTab('login')">تسجيل الدخول</button>
        <button class="tab-btn" onclick="switchAuthTab('register')">حساب جديد</button>
      </div>

      <!-- تبويب تسجيل الدخول -->
      <div id="authLoginTab" class="tab-content active">
        <form id="userLoginForm">
          <div class="form-group">
            <label>البريد الإلكتروني:</label>
            <input type="email" id="loginEmail" placeholder="name@example.com" required>
          </div>
          <div class="form-group">
            <label>كلمة المرور:</label>
            <input type="password" id="loginPassword" placeholder="كلمة المرور" required>
          </div>
          <button type="submit" class="btn">دخول إلى الحساب</button>
        </form>
      </div>

      <!-- تبويب إنشاء حساب جديد -->
      <div id="authRegisterTab" class="tab-content">
        <form id="userRegisterForm">
          <div class="form-group">
            <label>اسم المستخدم:</label>
            <input type="text" id="regName" placeholder="اسمك الكامل أو المستعار" required>
          </div>
          <div class="form-group">
            <label>البريد الإلكتروني:</label>
            <input type="email" id="regEmail" placeholder="name@example.com" required>
          </div>
          <div class="form-group">
            <label>كلمة المرور:</label>
            <input type="password" id="regPassword" placeholder="كلمة مرور قوية" required>
          </div>
          <button type="submit" class="btn">إنشاء حساب جديد</button>
        </form>
      </div>
    </div>
  </div>

  <!-- ميزة الملف الشخصي ونظام النقاط والمستويات (Profile & Points Modal) -->
  <div class="modal" id="userProfileModal">
    <div class="modal-content" style="max-width: 450px; text-align: center;">
      <div class="modal-header">
        <h3><i class="fas fa-id-badge"></i> ملف المستخدم الشخصي</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>
      <div style="padding: 10px; display: flex; flex-direction: column; gap: 15px;">
        <div style="font-size: 60px; color: var(--primary-color);">
          <i class="fas fa-user-circle"></i>
        </div>
        <div>
          <h3 id="profileUserName" style="color: var(--text-color);">اسم المستخدم</h3>
          <p id="profileUserEmail" style="color: var(--text-secondary); font-size: 13px;">email@example.com</p>
        </div>

        <!-- نظام النقاط والمستويات (Gamification) -->
        <div style="background: var(--sidebar-bg); border: 1px solid var(--border-color); padding: 15px; border-radius: 8px; text-align: right;">
          <div style="display: flex; justify-content: space-between; font-weight: bold; margin-bottom: 8px;">
            <span><i class="fas fa-trophy" style="color: #f1c40f;"></i> مستوى العضوية: <span id="profileUserLevel" style="color: var(--primary-color);">مبتدئ</span></span>
            <span>نقاط XP: <span id="profileUserPoints" style="color: #27ae60;">0</span></span>
          </div>
          <p style="font-size: 11px; color: var(--text-secondary); margin-top: 5px;">شاهد المزيد من الحلقات واكتب التعليقات لترقية مستواك وجمع النقاط!</p>
        </div>

        <button class="btn btn-del" onclick="logoutUser()"><i class="fas fa-sign-out-alt"></i> تسجيل الخروج</button>
      </div>
      <button class="btn closeModal" style="margin-top: 10px;">إغلاق</button>
    </div>
  </div>

  <!-- Notifications Modal -->
  <div class="modal" id="notificationsModal">
    <div class="modal-content" style="max-width: 450px;">
      <div class="modal-header">
        <h3><i class="fas fa-bell"></i> التنبيهات والإشعارات</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>
      <div style="display: flex; flex-direction: column; gap: 10px; font-size: 13px;" id="notificationsListContainer">
        <div style="background:var(--sidebar-bg); padding:10px; border-radius:6px; border-right:3px solid var(--primary-color);">
          <strong>🎉 أهلاً بك في التحديث الجديد</strong>
          <p style="color:var(--text-secondary); margin-top:3px;">تم إضافة نظام اختيار الألام والصور من المعرض وفيسبوك بنجاح!</p>
        </div>
      </div>
      <button class="btn closeModal" style="margin-top: 15px;">حسناً</button>
    </div>
  </div>

  <!-- Privacy Policy Modal -->
  <div class="modal" id="privacyModal">
    <div class="modal-content" style="max-width: 600px;">
      <div class="modal-header">
        <h3><i class="fas fa-user-lock"></i> سياسة الخصوصية</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>
      <div style="font-size: 13px; color: var(--text-secondary); line-height: 1.7; display: flex; flex-direction: column; gap: 12px;">
        <p>مرحباً بك في منصة <strong>mrstoud</strong>. نحن نولي أهمية قصوى لخصوصية مستخدمينا وأمان بياناتهم الشخصية.</p>
        <h4 style="color: var(--primary-color); margin-top: 5px;">1. جمع البيانات</h4>
        <p>قد نقوم بجمع بعض البيانات غير الشخصية مثل نوع المتصفح، عنوان IP، والتعليقات والتقييمات والمفضلة لغرض تحسين الأداء وتجربة المستخدم.</p>
        <h4 style="color: var(--primary-color); margin-top: 5px;">2. حماية البيانات وأمانها</h4>
        <p>نحن نستخدم أنظمة جدار حماية (WAF) متطورة لرصد أي هجمات أو محاولات اختراق وضمان حماية المستخدمين والسيرفرات من أي استغلال خبيث.</p>
        <h4 style="color: var(--primary-color); margin-top: 5px;">3. الإعلانات وملفات الكوكيز (Cookies)</h4>
        <p>قد تستخدم المنصة شبكات إعلانية خارجية تضع ملفات تعريف ارتباط لتقديم إعلانات مخصصة للمستخدم بناءً على زياراته للموقع.</p>
        <h4 style="color: var(--primary-color); margin-top: 5px;">4. التعليقات والاستخدام المقبول</h4>
        <p>يتحمل المستخدم المسؤولية كاملة عن أي تعليق يتم نشره عبر المنصة، ويُمنع استخدام ألفاظ خرسانية أو محاولات إغراق، وتخضع المدخلات لفحص أمني آلي.</p>
      </div>
      <button class="btn closeModal" style="margin-top: 20px;">إغلاق</button>
    </div>
  </div>

  <!-- Analytics Modal -->
  <div class="modal" id="analyticsModal">
    <div class="modal-content" style="max-width: 450px; text-align: center;">
      <div class="modal-header">
        <h3><i class="fas fa-chart-pie"></i> إحصائيات المشاهدة الخاصة بك</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>
      <div style="padding: 15px; display: flex; flex-direction: column; gap: 12px; font-size: 14px; text-align: right;">
        <div style="background:var(--sidebar-bg); padding:10px; border-radius:6px; display:flex; justify-content:space-between;">
          <span>إجمالي الأعمال المشاهدة:</span>
          <strong id="statTotalWatched">0</strong>
        </div>
        <div style="background:var(--sidebar-bg); padding:10px; border-radius:6px; display:flex; justify-content:space-between;">
          <span>الأفلام في المفضلة:</span>
          <strong id="statTotalFavorites">0</strong>
        </div>
        <div style="background:var(--sidebar-bg); padding:10px; border-radius:6px; display:flex; justify-content:space-between;">
          <span>قائمة المشاهدة لاحقاً:</span>
          <strong id="statTotalWatchlist">0</strong>
        </div>
      </div>
      <button class="btn btn-secondary" onclick="exportUserStats()" style="margin-top: 5px;"><i class="fas fa-share-alt"></i> مشاركة إحصائياتي</button>
      <button class="btn closeModal" style="margin-top: 10px;">حسناً</button>
    </div>
  </div>

  <!-- Login Modal -->
  <div class="modal" id="loginModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3>دخول لوحة الإدارة</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <div class="admin-warning-box">
        <i class="fas fa-exclamation-triangle"></i>
        <div>
          <strong>تنبيه أمني مشدد:</strong> هذه اللوحة محمية بنظام WAF لصد الهجمات. أي محاولة حقن أو تخمين ستؤدي لحظر الجهاز فوراً!
        </div>
      </div>

      <form id="loginForm">
        <div class="form-group">
          <label for="adminPassword">كلمة المرور:</label>
          <input type="password" id="adminPassword" placeholder="أدخل كلمة المرور" required autocomplete="off">
        </div>
        <button type="submit" class="btn" id="loginSubmitBtn">دخول</button>
        <div id="lockoutTimer" class="lockout-msg"></div>
      </form>
    </div>
  </div>

  <!-- Admin Control Panel Modal -->
  <div class="modal" id="adminModal">
    <div class="modal-content">
      <div class="modal-header">
        <h3 id="adminModalTitle">لوحة التحكم والتنفيذ</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <div class="admin-tabs">
        <button class="tab-btn active" onclick="switchAdminTab('tab-shows')"><i class="fas fa-film"></i> المسلسلات والأفلام</button>
        <button class="tab-btn" onclick="switchAdminTab('tab-users')"><i class="fas fa-users"></i> إدارة المستخدمين</button>
        <button class="tab-btn" onclick="switchAdminTab('tab-ban')"><i class="fas fa-user-slash"></i> الحظر وفك الحظر</button>
        <button class="tab-btn" onclick="switchAdminTab('tab-backup')"><i class="fas fa-database"></i> النسخ الاحتياطي</button>
      </div>

      <!-- Tab 1: Shows & Movies -->
      <div id="tab-shows" class="tab-content active">
        <form id="saveShowForm" style="margin-bottom: 25px;">
          <input type="hidden" id="editShowId" value="">
          <h4 style="margin-bottom: 12px; color: var(--primary-color);" id="formSubTitle">إضافة عمل جديد (فيلم / مسلسل)</h4>
          
          <div class="form-group">
            <label for="showCategory">نوع العمل / التصنيف:</label>
            <select id="showCategory" required>
              <option value="series">مسلسل</option>
              <option value="movie">فيلم</option>
            </select>
          </div>

          <div class="form-group">
            <label for="showGenre">التصنيف الفرعي:</label>
            <select id="showGenre">
              <option value="action">أكشن ومغامرة</option>
              <option value="drama">دراما وتشويق</option>
              <option value="comedy">كوميدي</option>
              <option value="scifi">خيال علمي</option>
            </select>
          </div>

          <div class="form-group">
            <label for="showTitle">عنوان العمل:</label>
            <input type="text" id="showTitle" required placeholder="مثال: فيلم/مسلسل كامل">
          </div>
          
          <div class="form-group">
            <label for="showBadge">نص الشارة (مثال: حلقة 1 / 2:30 ساعة):</label>
            <input type="text" id="showBadge" placeholder="مثال: حلقة 1">
          </div>

          <div class="form-group">
            <label for="showYear">سنة الإصدار:</label>
            <input type="text" id="showYear" placeholder="مثال: 2026" value="2026">
          </div>

          <div class="form-group">
            <label for="showRating">التقييم (من 5 أو 10):</label>
            <input type="text" id="showRating" placeholder="مثال: 4.8" value="4.8">
          </div>

          <!-- إضافة صورة الغلاف من المعرض أو الرابط (مطلب المستخدم) -->
          <div class="form-group" style="background: var(--sidebar-bg); padding: 12px; border-radius: 8px; border: 1px dashed var(--primary-color);">
            <label for="showImageFile" style="color: var(--text-color); font-weight: bold;"><i class="fas fa-image"></i> صورة الغلاف الخارجية (من المعرض أو الرابط):</label>
            <input type="file" id="showImageFile" accept="image/*" style="margin-bottom: 8px;">
            <input type="url" id="showImage" placeholder="أو أدخل رابط صورة الغلاف مباشرة https://example.com/image.jpg">
          </div>

          <div class="form-group" style="background: var(--sidebar-bg); padding: 12px; border-radius: 8px; border: 1px dashed var(--primary-color);">
            <label for="showVideoFile" style="color: var(--text-color); font-weight: bold;"><i class="fas fa-video"></i> رفع أو اختيار فيديو الفيلم من المعرض (ملف محلي):</label>
            <input type="file" id="showVideoFile" accept="video/*" style="margin-bottom: 8px;">
            <small style="color:var(--text-secondary); display:block;">يمكنك اختيار فيديو محلي أو إدخال روابط يوتيوب، فيسبوك (Facebook Video Embed)، أو أي سيرفر آخر أدناه.</small>
          </div>

          <div class="form-group">
            <label for="showEpisodesInput">قائمة الحلقات (روابط يوتيوب، فيسبوك أو سيرفرات مفصولة بفاصلة أو سطر جديد):</label>
            <textarea id="showEpisodesInput" rows="3" placeholder="الحلقة 1: https://...&#10;الحلقة 2: https://..."></textarea>
          </div>

          <div class="form-group">
            <label for="showVideoUrl">سيرفر المشغل الرئيسي (Server 1 - يوتيوب / فيسبوك / رابط مباشر):</label>
            <input type="text" id="showVideoUrl" placeholder="https://www.youtube.com/embed/... أو رابط فيسبوك أو ملف">
          </div>

          <div class="form-group">
            <label for="showVideoUrl2">سيرفر المشغل الاحتياطي (Server 2):</label>
            <input type="text" id="showVideoUrl2" placeholder="https://...">
          </div>

          <div class="form-group">
            <label for="showVideoUrl3">سيرفر المشغل السريع (Server 3):</label>
            <input type="text" id="showVideoUrl3" placeholder="https://...">
          </div>

          <div class="form-group">
            <label for="showQuality">الجودة المتاحة:</label>
            <input type="text" id="showQuality" placeholder="مثال: 1080p, 720p" value="1080p Full HD">
          </div>

          <div class="form-group">
            <label for="showDownloadUrl">رابط تحميل الفيديو:</label>
            <input type="url" id="showDownloadUrl" placeholder="https://example.com/download.mp4">
          </div>

          <button type="submit" class="btn" id="saveBtn">حفظ وإضافة</button>
          <button type="button" class="btn btn-secondary" id="cancelEditBtn" style="display:none;">إلغاء التعديل</button>
        </form>

        <hr style="border-color: var(--border-color); margin-bottom: 15px;">
        <h4 style="margin-bottom: 12px;">قائمة الفيديوهات الحالية</h4>
        <div id="adminShowsList"></div>
      </div>

      <!-- Tab 2: Users List -->
      <div id="tab-users" class="tab-content">
        <h4 style="margin-bottom: 12px; color: var(--primary-color);">جميع المستخدمين المسجلين</h4>
        <div id="usersListContainer"></div>
      </div>

      <!-- Tab 3: Ban / Unban Control -->
      <div id="tab-ban" class="tab-content">
        <h4 style="margin-bottom: 12px; color: var(--primary-color);">حظر مستخدم جديد</h4>
        <form id="banUserForm" style="margin-bottom: 20px;">
          <div class="form-group">
            <label for="banEmail">بريد أو معرف المستخدم المراد حظره:</label>
            <input type="text" id="banEmail" placeholder="example@domain.com" required>
          </div>
          <div class="form-group">
            <label for="banReason">سبب الحظر:</label>
            <input type="text" id="banReason" placeholder="مثال: محاولة اختراق أو مخالفة القوانين">
          </div>
          <button type="submit" class="btn btn-del"><i class="fas fa-user-slash"></i> تأكيد الحظر</button>
        </form>

        <hr style="border-color: var(--border-color); margin: 20px 0;">

        <h4 style="margin-bottom: 12px; color: #27ae60;">قائمة المحظورين</h4>
        <div id="bannedUsersContainer"></div>
      </div>

      <!-- Tab 4: Backup & Restore -->
      <div id="tab-backup" class="tab-content">
        <h4 style="margin-bottom: 12px; color: var(--primary-color);">إدارة قاعدة البيانات (Backup & Restore)</h4>
        <p style="font-size: 13px; color: var(--text-secondary); margin-bottom: 15px;">يمكنك حفظ نسخة احتياطية لجميع أفلام المسلسلات والبيانات في ملف JSON أو استعادتها.</p>
        <button class="btn" onclick="exportDatabaseJSON()" style="margin-bottom: 10px;"><i class="fas fa-download"></i> تصدير قاعدة البيانات (JSON)</button>
        <div class="form-group">
          <label for="importJsonFile">استعادة البيانات من ملف:</label>
          <input type="file" id="importJsonFile" accept=".json" onchange="importDatabaseJSON(this)">
        </div>
      </div>

    </div>
  </div>

  <!-- Player Modal -->
  <div class="modal" id="playerModal">
    <div class="modal-content" style="max-width: 750px;">
      <div class="modal-header">
        <h3 id="playerTitle">عرض الفيديو</h3>
        <button class="close-btn closeModal">&times;</button>
      </div>

      <!-- Episodes Selector Bar -->
      <div class="episodes-section" id="episodesSectionBox" style="display:none;">
        <div class="episodes-title"><i class="fas fa-list"></i> قائمة الحلقات المتاحة</div>
        <div class="episodes-grid" id="episodesGridContainer"></div>
      </div>

      <!-- Server Selector Section -->
      <div id="serverSelectorContainer" class="server-btn-group"></div>

      <!-- Extra Action Bar -->
      <div class="extra-player-actions">
        <button class="action-badge-btn" id="favoriteToggleBtn" onclick="toggleCurrentFavorite()">
          <i class="far fa-heart" id="favoriteIcon"></i> <span id="favoriteBtnText">أضف للمفضلة</span>
        </button>

        <button class="action-badge-btn" id="watchlistToggleBtn" onclick="toggleCurrentWatchlist()">
          <i class="far fa-clock" id="watchlistIcon"></i> <span id="watchlistBtnText">المشاهدة لاحقاً</span>
        </button>

        <button class="action-badge-btn" onclick="toggleFullscreenPlayer()" title="ملء الشاشة">
          <i class="fas fa-expand"></i> تكبير
        </button>

        <button class="action-badge-btn" onclick="shareWhatsApp()" title="مشاركة عبر واتساب" style="color:#27ae60;">
          <i class="fab fa-whatsapp"></i> واتساب
        </button>

        <button class="action-badge-btn" onclick="shareCurrentShow()">
          <i class="fas fa-share-alt"></i> مشاركة
        </button>

        <div style="display: flex; align-items: center; gap: 8px;">
          <span style="font-size: 12px; color: var(--text-secondary);">تقييمك:</span>
          <div class="star-rating" id="starRatingContainer">
            <i class="fas fa-star star" onclick="rateShow(1)"></i>
            <i class="fas fa-star star" onclick="rateShow(2)"></i>
            <i class="fas fa-star star" onclick="rateShow(3)"></i>
            <i class="fas fa-star star" onclick="rateShow(4)"></i>
            <i class="fas fa-star star" onclick="rateShow(5)"></i>
          </div>
        </div>
      </div>

      <!-- Interactive Player Tools -->
      <div class="player-tools-bar" style="margin-top: 12px;">
        <div class="tool-row">
          <div class="tool-group">
            <i class="fas fa-closed-captioning" style="color:var(--primary-color);"></i>
            <label>الترجمة الآلية:</label>
            <select id="subtitleSelect" onchange="applySubtitleLanguage(this.value)">
              <option value="ar">العربية (تلقائي)</option>
              <option value="en">الإنجليزية (English)</option>
              <option value="fr">الفرنسية (Français)</option>
              <option value="off">إيقاف الترجمة</option>
            </select>
          </div>

          <div class="tool-group">
            <i class="fas fa-sliders-h" style="color:var(--primary-color);"></i>
            <label>نمط الجودة:</label>
            <select id="qualityBoostSelect" onchange="applyQualityBoost(this.value)">
              <option value="standard">1080p قياسي</option>
              <option value="vivid">4K AI محصّن (ألوان مشبعة)</option>
              <option value="sharp">Ultra Sharp (وضوح حدة)</option>
            </select>
          </div>

          <div class="tool-group">
            <i class="fas fa-bolt" style="color:#f39c12;"></i>
            <label>السرعة:</label>
            <button class="speed-badge" onclick="changePlaybackSpeed(0.5)">0.5x</button>
            <button class="speed-badge" onclick="changePlaybackSpeed(1)" style="background:var(--primary-color);color:#fff;">1x</button>
            <button class="speed-badge" onclick="changePlaybackSpeed(1.5)">1.5x</button>
          </div>
        </div>

        <div class="tool-row">
          <div class="slider-container">
            <i class="fas fa-volume-up" style="color:#27ae60;"></i>
            <span>مضخم الصوت (Boost):</span>
            <input type="range" id="volumeBoostSlider" min="100" max="200" value="100" oninput="applyVolumeBoost(this.value)">
            <span id="volumeVal">100%</span>
          </div>

          <div class="slider-container">
            <i class="fas fa-sun" style="color:#f39c12;"></i>
            <span>السطوع:</span>
            <input type="range" id="brightnessSlider" min="80" max="150" value="100" oninput="applyVideoFilters()">
          </div>

          <div class="slider-container">
            <i class="fas fa-adjust" style="color:#3498db;"></i>
            <span>التباين:</span>
            <input type="range" id="contrastSlider" min="80" max="150" value="100" oninput="applyVideoFilters()">
          </div>
        </div>

        <div class="tool-row" style="border-top: 1px dashed var(--border-color); padding-top: 10px;">
          <div class="tool-group">
            <i class="fas fa-bed" style="color:#9b59b6;"></i>
            <label>مؤقت النوم:</label>
            <select id="sleepTimerSelect" onchange="setSleepTimer(this.value)">
              <option value="0">إيقاف المؤقت</option>
              <option value="15">بعد 15 دقيقة</option>
              <option value="30">بعد 30 دقيقة</option>
              <option value="60">بعد 60 دقيقة</option>
            </select>
          </div>

          <div class="tool-group">
            <i class="fas fa-redo" style="color:#2ecc71;"></i>
            <label>تشغيل تلقائي للعمل التالي:</label>
            <input type="checkbox" id="autoplayNextCheck" checked style="cursor: pointer; width: 16px; height: 16px;">
          </div>
        </div>
      </div>

      <div class="video-container" id="videoPlayerBox"></div>

      <div class="video-details">
        <div class="quality-tags">
          <span style="font-size: 13px; color: var(--text-secondary);">الجودة المتاحة:</span>
          <span class="quality-tag" id="playerQuality">1080p</span>
        </div>
        <div id="downloadContainer"></div>
        
        <div class="download-progress-container" id="downloadProgressBox">
          <div style="display:flex; justify-content:space-between; font-size:12px; color:var(--text-secondary);">
            <span id="downloadStatusText">جاري تحضير ملف التحميل...</span>
            <span id="downloadPercentText">0%</span>
          </div>
          <div class="progress-bar-track">
            <div class="progress-bar-fill" id="progressBarFill"></div>
          </div>
        </div>
      </div>

      <!-- Comments Section -->
      <div class="comments-section">
        <div class="comments-title"><i class="fas fa-comments"></i> قسم التعليقات</div>
        
        <form id="commentForm" style="margin-bottom: 15px;">
          <div class="form-group">
            <input type="text" id="commentUserName" placeholder="اسمك (اختياري)" style="margin-bottom: 8px;">
            <textarea id="commentText" rows="2" placeholder="اكتب تعليقك هنا..." required></textarea>
          </div>
          <button type="submit" class="btn" style="padding: 8px 15px; font-size: 13px;">إرسال التعليق (+10 نقاط XP)</button>
        </form>

        <div id="commentsList"></div>
      </div>

    </div>
  </div>

  <script>
    /* =========================================================
       🔐 ADVANCED ANTI-HACK & SECURITY SYSTEM (WAF)
       ========================================================= */

    function checkGlobalBanStatus() {
      if (localStorage.getItem('mrstoud_verified_owner') === 'true') {
        return;
      }
      if (localStorage.getItem('mrstoud_is_hacker_banned') === 'true') {
        document.getElementById('hackerBlockedScreen').style.display = 'flex';
        throw new Error('Access denied: Security violation detected.');
      }
    }

    function triggerAutoHackerBan(reason) {
      if (localStorage.getItem('mrstoud_verified_owner') === 'true') {
        return;
      }

      localStorage.setItem('mrstoud_is_hacker_banned', 'true');
      
      let users = JSON.parse(localStorage.getItem('mrstoud_users')) || defaultUsers;
      users.push({
        id: Date.now(),
        name: "Hacker Detected",
        email: "HACK_ATTEMPT_" + Math.floor(Math.random() * 10000),
        status: "banned",
        banReason: "محاولة اختراق النظام (" + reason + ")"
      });
      localStorage.setItem('mrstoud_users', JSON.stringify(users));

      document.getElementById('hackerBlockedScreen').style.display = 'flex';
    }

    function inspectSecurityInput(inputStr) {
      if (!inputStr) return inputStr;

      const attackPatterns = [
        /<script\b[^>]*>([\s\S]*?)<\/script>/gi,
        /javascript:/gi,
        /onerror=/gi,
        /onload=/gi,
        /SELECT\s+.*\s+FROM/gi,
        /UNION\s+SELECT/gi,
        /INSERT\s+INTO/gi,
        /DELETE\s+FROM/gi,
        /DROP\s+TABLE/gi,
        /'\s*OR\s*'\d+'='\d+/gi,
        /--/g,
        /\.\.\//g
      ];

      for (let pattern of attackPatterns) {
        if (pattern.test(inputStr)) {
          triggerAutoHackerBan("حقن أكواد خبيثة: " + pattern.toString());
          return '';
        }
      }
      return inputStr;
    }

    let requestHistory = [];
    function checkRateLimit() {
      if (localStorage.getItem('mrstoud_verified_owner') === 'true') return;
      const now = Date.now();
      requestHistory.push(now);
      requestHistory = requestHistory.filter(timestamp => now - timestamp < 5000);
      
      if (requestHistory.length > 25) {
        triggerAutoHackerBan("هجوم إغراق DDoS / Rate-Limit Exceeded");
      }
    }

    document.addEventListener('input', (e) => {
      checkRateLimit();
      if (e.target.tagName === 'INPUT' || e.target.tagName === 'TEXTAREA') {
        inspectSecurityInput(e.target.value);
      }
    });

    function sanitizeInput(str) {
      if (!str) return '';
      if (str.startsWith('data:image/') || str.startsWith('blob:')) return str;
      inspectSecurityInput(str);
      const temp = document.createElement('div');
      temp.textContent = str;
      return temp.innerHTML;
    }

    checkGlobalBanStatus();

    /* =========================================================
       DATA & APPLICATION LOGIC
       ========================================================= */

    const defaultShows = [
      {
        id: 1,
        category: "series",
        genre: "drama",
        title: "مسلسل في السابعة عشر",
        badge: "حلقة 1",
        year: "2025",
        rating: "4.9",
        image: "https://images.unsplash.com/photo-1536440136628-849c177e76a1?auto=format&fit=crop&w=400&q=80",
        episodes: [
          { name: "الحلقة 1", url: "https://www.youtube.com/embed/dQw4w9WgXcQ" },
          { name: "الحلقة 2", url: "https://www.youtube.com/embed/dQw4w9WgXcQ" }
        ],
        videoUrl: "https://www.youtube.com/embed/dQw4w9WgXcQ",
        videoUrl2: "",
        videoUrl3: "",
        quality: "1080p Full HD",
        downloadUrl: "https://example.com/download.mp4"
      },
      {
        id: 2,
        category: "movie",
        genre: "action",
        title: "فيلم الأكشن والمغامرة",
        badge: "2:15 ساعة",
        year: "2026",
        rating: "4.7",
        image: "https://images.unsplash.com/photo-1489599849927-2ee91cede3ba?auto=format&fit=crop&w=400&q=80",
        episodes: [],
        videoUrl: "https://www.youtube.com/embed/dQw4w9WgXcQ",
        videoUrl2: "",
        videoUrl3: "",
        quality: "4K Ultra HD",
        downloadUrl: "https://example.com/download.mp4"
      }
    ];

    const defaultUsers = [
      { id: 101, name: "أحمد علي", email: "ahmed@example.com", status: "active" },
      { id: 102, name: "محمد ياسين", email: "mowin@example.com", status: "active" }
    ];

    let shows = JSON.parse(localStorage.getItem('mrstoud_shows')) || defaultShows;
    let users = JSON.parse(localStorage.getItem('mrstoud_users')) || defaultUsers;
    let commentsData = JSON.parse(localStorage.getItem('mrstoud_comments')) || {};
    let favoritesData = JSON.parse(localStorage.getItem('mrstoud_favorites')) || [];
    let watchlistData = JSON.parse(localStorage.getItem('mrstoud_watchlist')) || [];
    let historyData = JSON.parse(localStorage.getItem('mrstoud_history')) || [];
    let ratingsData = JSON.parse(localStorage.getItem('mrstoud_ratings')) || {};

    let currentUserSession = JSON.parse(localStorage.getItem('mrstoud_current_user')) || null;
    let userPoints = parseInt(localStorage.getItem('mrstoud_user_points') || '0');

    window.addPoints = function(amount) {
      userPoints += amount;
      localStorage.setItem('mrstoud_user_points', userPoints.toString());
      showToast(`+${amount} نقطة XP جديدة لصالحك!`);
    };

    window.getUserLevel = function(points) {
      if (points >= 200) return "محترف أسطوري ⭐";
      if (points >= 100) return "متابع نشيط 🎬";
      if (points >= 50) return "عضو متفاعل 🍿";
      return "مبتدئ جديد 🌱";
    };

    window.openAuthOrProfileModal = function() {
      if (currentUserSession) {
        document.getElementById('profileUserName').textContent = currentUserSession.name;
        document.getElementById('profileUserEmail').textContent = currentUserSession.email;
        document.getElementById('profileUserPoints').textContent = userPoints;
        document.getElementById('profileUserLevel').textContent = getUserLevel(userPoints);
        document.getElementById('userProfileModal').classList.add('active');
      } else {
        document.getElementById('authModal').classList.add('active');
      }
    };

    window.switchAuthTab = function(tab) {
      document.querySelectorAll('#authModal .tab-btn').forEach(b => b.classList.remove('active'));
      document.getElementById('authLoginTab').classList.remove('active');
      document.getElementById('authRegisterTab').classList.remove('active');

      if (tab === 'login') {
        event.currentTarget.classList.add('active');
        document.getElementById('authLoginTab').classList.add('active');
      } else {
        event.currentTarget.classList.add('active');
        document.getElementById('authRegisterTab').classList.add('active');
      }
    };

    document.getElementById('userLoginForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const email = document.getElementById('loginEmail').value.trim();
      const pass = document.getElementById('loginPassword').value.trim();
      
      const found = users.find(u => u.email.toLowerCase() === email.toLowerCase());
      if (found) {
        if (found.status === 'banned') {
          alert('عذراً، هذا الحساب محظور من قبل الإدارة.');
          return;
        }
        currentUserSession = found;
        localStorage.setItem('mrstoud_current_user', JSON.stringify(currentUserSession));
        document.getElementById('authModal').classList.remove('active');
        showToast(`مرحباً بك مجدداً يا ${found.name}!`);
      } else {
        alert('البريد الإلكتروني غير مسجل. يرجى إنشاء حساب جديد.');
      }
    });

    document.getElementById('userRegisterForm').addEventListener('submit', (e) => {
      e.preventDefault();
      const name = document.getElementById('regName').value.trim();
      const email = document.getElementById('regEmail').value.trim();
      const pass = document.getElementById('regPassword').value.trim();

      if (users.some(u => u.email.toLowerCase() === email.toLowerCase())) {
        alert('البريد الإلكتروني مسجل مسبقاً!');
        return;
      }

      const newUser = { id: Date.now(), name, email, status: 'active' };
      users.push(newUser);
      localStorage.setItem('mrstoud_users', JSON.stringify(users));

      currentUserSession = newUser;
      localStorage.setItem('mrstoud_current_user', JSON.stringify(currentUserSession));
      addPoints(20);

      document.getElementById('authModal').classList.remove('active');
      showToast('تم إنشاء الحساب وتسجيل الدخول بنجاح! +20 نقطة');
    });

    window.logoutUser = function() {
      currentUserSession = null;
      localStorage.removeItem('mrstoud_current_user');
      document.getElementById('userProfileModal').classList.remove('active');
      showToast('تم تسجيل الخروج بنجاح.');
    };

    let currentShowId = null;
    let currentCategory = 'all';
    let currentGenre = 'all';
    let isAdminLoggedIn = false;
    let sleepTimerTimeout = null;

    let loginAttempts = parseInt(localStorage.getItem('mrstoud_login_attempts') || '0');
    let lockoutUntil = parseInt(localStorage.getItem('mrstoud_lockout_until') || '0');
    let ownerCorrectStreak = parseInt(localStorage.getItem('mrstoud_owner_streak') || '0');

    window.closeTopWelcome = function() {
      document.getElementById('topWelcomeBanner').style.display = 'none';
      localStorage.setItem('mrstoud_top_welcome_closed', 'true');
    };
    if (localStorage.getItem('mrstoud_top_welcome_closed') === 'true') {
      document.getElementById('topWelcomeBanner').style.display = 'none';
    }

    window.toggleFullscreenPlayer = function() {
      const container = document.getElementById('videoPlayerBox');
      if (!document.fullscreenElement) {
        if (container.requestFullscreen) container.requestFullscreen();
        showToast('تم التكبير لملء الشاشة.');
      } else {
        if (document.exitFullscreen) document.exitFullscreen();
      }
    };

    window.shareWhatsApp = function() {
      const title = playerTitle.textContent;
      const url = window.location.href;
      const waText = encodeURIComponent(`شاهد معنا ${title} عبر منصة mrstoud الرائعة: ${url}`);
      window.open(`https://api.whatsapp.com/send?text=${waText}`, '_blank');
    };

    window.openNotificationsModal = function() {
      document.getElementById('notificationsModal').classList.add('active');
    };

    window.exportUserStats = function() {
      const text = `📊 إحصائياتي على منصة mrstoud:\n- الأعمال المشاهدة: ${historyData.length}\n- المفضلة: ${favoritesData.length}\n- نقاط XP: ${userPoints}`;
      navigator.clipboard.writeText(text);
      showToast('تم نسخ إحصائياتك لمشاركتها مع أصدقائك!');
    };

    window.exportDatabaseJSON = function() {
      const dataStr = "data:text/json;charset=utf-8," + encodeURIComponent(JSON.stringify(shows, null, 2));
      const downloadAnchor = document.createElement('a');
      downloadAnchor.setAttribute("href", dataStr);
      downloadAnchor.setAttribute("download", "mrstoud_backup.json");
      document.body.appendChild(downloadAnchor);
      downloadAnchor.click();
      downloadAnchor.remove();
      showToast('تم تصدير ملف النسخ الاحتياطي بنجاح!');
    };

    window.importDatabaseJSON = function(input) {
      const file = input.files[0];
      if (!file) return;
      const reader = new FileReader();
      reader.onload = function(e) {
        try {
          const imported = JSON.parse(e.target.result);
          if (Array.isArray(imported)) {
            shows = imported;
            saveData();
            showToast('تم استعادة قاعدة البيانات بنجاح!');
          }
        } catch (err) {
          alert('ملف غير صالح!');
        }
      };
      reader.readAsText(file);
    };

    window.scrollToTop = function() {
      window.scrollTo({ top: 0, behavior: 'smooth' });
    };

    window.addEventListener('scroll', () => {
      const scrollBtn = document.getElementById('scrollToTopBtn');
      if (window.scrollY > 300) {
        scrollBtn.style.display = 'flex';
      } else {
        scrollBtn.style.display = 'none';
      }
    });

    const currentTheme = localStorage.getItem('mrstoud_theme') || 'dark';
    if (currentTheme === 'light') {
      document.documentElement.setAttribute('data-theme', 'light');
      document.getElementById('themeIcon').className = 'fas fa-sun';
    }

    const savedAccentColor = localStorage.getItem('mrstoud_accent_color');
    if (savedAccentColor) {
      document.documentElement.style.setProperty('--primary-color', savedAccentColor);
    }
    window.changeAccentColor = function(color) {
      document.documentElement.style.setProperty('--primary-color', color);
      localStorage.setItem('mrstoud_accent_color', color);
      document.querySelectorAll('.color-dot').forEach(dot => dot.classList.remove('active'));
      event.target.classList.add('active');
      showToast('تم تغيير لون المنصة بنجاح!');
    };

    document.getElementById('themeToggleBtn').addEventListener('click', () => {
      const isLight = document.documentElement.getAttribute('data-theme') === 'light';
      if (isLight) {
        document.documentElement.removeAttribute('data-theme');
        localStorage.setItem('mrstoud_theme', 'dark');
        document.getElementById('themeIcon').className = 'fas fa-moon';
      } else {
        document.documentElement.setAttribute('data-theme', 'light');
        localStorage.setItem('mrstoud_theme', 'light');
        document.getElementById('themeIcon').className = 'fas fa-sun';
      }
    });

    const cinemaModeBtn = document.getElementById('cinemaModeBtn');
    let isCinemaMode = false;
    cinemaModeBtn.addEventListener('click', () => {
      isCinemaMode = !isCinemaMode;
      if (isCinemaMode) {
        document.body.classList.add('cinema-mode');
        cinemaModeBtn.style.color = 'var(--primary-color)';
        showToast('تم تفعيل وضع السينما المظلم!');
      } else {
        document.body.classList.remove('cinema-mode');
        cinemaModeBtn.style.color = '';
        showToast('تم إيقاف وضع السينما.');
      }
    });

    window.showToast = function(msg) {
      const toast = document.getElementById('toastNotification');
      document.getElementById('toastMessage').textContent = msg;
      toast.classList.add('show');
      setTimeout(() => {
        toast.classList.remove('show');
      }, 3000);
    };

    window.startVoiceSearch = function() {
      if (!('webkitSpeechRecognition' in window) && !('SpeechRecognition' in window)) {
        alert('عذراً، متصفحك لا يدعم ميزة البحث الصوتي.');
        return;
      }
      const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
      const recognition = new SpeechRecognition();
      recognition.lang = 'ar-SA';
      showToast('جاري الاستماع... تحدث الآن');
      recognition.onresult = (event) => {
        const speechToText = event.results[0][0].transcript;
        sidebarSearchInput.value = speechToText;
        renderShows(speechToText);
        showToast('تم البحث عن: ' + speechToText);
      };
      recognition.start();
    };

    window.playRandomShow = function() {
      if (shows.length === 0) {
        showToast('لا توجد أعمال متاحة حالياً.');
        return;
      }
      const randomIndex = Math.floor(Math.random() * shows.length);
      openPlayer(shows[randomIndex]);
      showToast('تم اختيار عمل عشوائي لك!');
    };

    window.openAnalyticsModal = function() {
      toggleSidebar();
      document.getElementById('statTotalWatched').textContent = historyData.length;
      document.getElementById('statTotalFavorites').textContent = favoritesData.length;
      document.getElementById('statTotalWatchlist').textContent = watchlistData.length;
      document.getElementById('analyticsModal').classList.add('active');
    };

    window.setSleepTimer = function(minutes) {
      if (sleepTimerTimeout) clearTimeout(sleepTimerTimeout);
      const mins = parseInt(minutes);
      if (mins > 0) {
        showToast(`تم ضبط مؤقت النوم بعد ${mins} دقيقة.`);
        sleepTimerTimeout = setTimeout(() => {
          document.getElementById('playerModal').classList.remove('active');
          videoPlayerBox.innerHTML = '';
          showToast('انتهى وقـت المشاهدة، تم إيقاف التشغيل تلقائياً.');
        }, mins * 60 * 1000);
      } else {
        showToast('تم إلغاء مؤقت النوم.');
      }
    };

    const showsGrid = document.getElementById('showsGrid');
    const menuToggleBtn = document.getElementById('menuToggleBtn');
    const closeSidebarBtn = document.getElementById('closeSidebarBtn');
    const sidebar = document.getElementById('sidebar');
    const overlay = document.getElementById('overlay');
    const sidebarSearchInput = document.getElementById('sidebarSearchInput');
    const sectionTitle = document.getElementById('sectionTitle');
    
    const countAll = document.getElementById('countAll');
    const countSeries = document.getElementById('countSeries');
    const countMovies = document.getElementById('countMovies');
    const countFavorites = document.getElementById('countFavorites');
    const countWatchlist = document.getElementById('countWatchlist');

    const adminBtn = document.getElementById('adminBtn');
    const privacyBtn = document.getElementById('privacyBtn');
    const loginModal = document.getElementById('loginModal');
    const adminModal = document.getElementById('adminModal');
    const playerModal = document.getElementById('playerModal');
    const welcomeModal = document.getElementById('welcomeModal');
    const privacyModal = document.getElementById('privacyModal');
    const analyticsModal = document.getElementById('analyticsModal');
    const loginForm = document.getElementById('loginForm');
    const saveShowForm = document.getElementById('saveShowForm');
    const adminShowsList = document.getElementById('adminShowsList');
    const closeModalBtns = document.querySelectorAll('.closeModal');
    const cancelEditBtn = document.getElementById('cancelEditBtn');
    const loginSubmitBtn = document.getElementById('loginSubmitBtn');
    const lockoutTimer = document.getElementById('lockoutTimer');
    const usersListContainer = document.getElementById('usersListContainer');
    const bannedUsersContainer = document.getElementById('bannedUsersContainer');
    const banUserForm = document.getElementById('banUserForm');

    const videoPlayerBox = document.getElementById('videoPlayerBox');
    const playerTitle = document.getElementById('playerTitle');
    const playerQuality = document.getElementById('playerQuality');
    const downloadContainer = document.getElementById('downloadContainer');
    const serverSelectorContainer = document.getElementById('serverSelectorContainer');
    const commentForm = document.getElementById('commentForm');
    const commentsList = document.getElementById('commentsList');

    const brightnessSlider = document.getElementById('brightnessSlider');
    const contrastSlider = document.getElementById('contrastSlider');
    const volumeBoostSlider = document.getElementById('volumeBoostSlider');
    const volumeVal = document.getElementById('volumeVal');
    const subtitleSelect = document.getElementById('subtitleSelect');
    const qualityBoostSelect = document.getElementById('qualityBoostSelect');

    window.applyVideoFilters = function() {
      const b = brightnessSlider.value;
      const c = contrastSlider.value;
      const target = videoPlayerBox.querySelector('iframe') || videoPlayerBox.querySelector('video');
      if (target) {
        target.style.filter = `brightness(${b}%) contrast(${c}%)`;
      }
    };

    window.applyVolumeBoost = function(val) {
      volumeVal.textContent = `${val}%`;
      const videoEl = videoPlayerBox.querySelector('video');
      if (videoEl) {
        videoEl.volume = Math.min(val / 100, 1.0);
      }
    };

    window.applySubtitleLanguage = function(lang) {
      const videoEl = videoPlayerBox.querySelector('video');
      if (videoEl && videoEl.textTracks && videoEl.textTracks.length > 0) {
        for (let i = 0; i < videoEl.textTracks.length; i++) {
          videoEl.textTracks[i].mode = (videoEl.textTracks[i].language === lang) ? 'showing' : 'disabled';
        }
      }
    };

    window.applyQualityBoost = function(type) {
      if (type === 'vivid') {
        brightnessSlider.value = 110;
        contrastSlider.value = 125;
      } else if (type === 'sharp') {
        brightnessSlider.value = 105;
        contrastSlider.value = 115;
      } else {
        brightnessSlider.value = 100;
        contrastSlider.value = 100;
      }
      applyVideoFilters();
    };

    window.changePlaybackSpeed = function(speed) {
      const videoEl = videoPlayerBox.querySelector('video');
      if (videoEl) {
        videoEl.playbackRate = speed;
        showToast(`تم تغيير سرعة التشغيل إلى ${speed}x`);
      } else {
        showToast('ميزة تغيير السرعة متاحة للفيديوهات المحلية المباشرة.');
      }
    };

    function resetVideoTools() {
      brightnessSlider.value = 100;
      contrastSlider.value = 100;
      volumeBoostSlider.value = 100;
      volumeVal.textContent = '100%';
      subtitleSelect.value = 'ar';
      qualityBoostSelect.value = 'standard';
      document.getElementById('sleepTimerSelect').value = '0';
    }

    function checkFirstVisit() {
      if (!localStorage.getItem('mrstoud_visited_before')) {
        welcomeModal.classList.add('active');
        localStorage.setItem('mrstoud_visited_before', 'true');
      }
    }

    window.switchAdminTab = function(tabId) {
      document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));
      document.querySelectorAll('.tab-content').forEach(content => content.classList.remove('active'));

      event.currentTarget.classList.add('active');
      document.getElementById(tabId).classList.add('active');
    };

    function updateCounters() {
      const seriesCount = shows.filter(s => s.category === 'series').length;
      const moviesCount = shows.filter(s => s.category === 'movie').length;

      countAll.textContent = shows.length;
      countSeries.textContent = seriesCount;
      countMovies.textContent = moviesCount;
      countFavorites.textContent = favoritesData.length;
      countWatchlist.textContent = watchlistData.length;
    }

    function checkLockoutStatus() {
      if (localStorage.getItem('mrstoud_verified_owner') === 'true') {
        return false;
      }

      const now = Date.now();
      if (lockoutUntil && now < lockoutUntil) {
        const remainingHours = Math.ceil((lockoutUntil - now) / (1000 * 60 * 60));
        loginSubmitBtn.disabled = true;
        lockoutTimer.innerHTML = `<i class="fas fa-lock"></i> تم حظر محاولات الدخول لكثرة الأخطاء! يرجى الانتظار ${remainingHours} ساعة.`;
        return true;
      } else if (lockoutUntil && now >= lockoutUntil) {
        localStorage.removeItem('mrstoud_lockout_until');
        localStorage.setItem('mrstoud_login_attempts', '0');
        loginAttempts = 0;
        loginSubmitBtn.disabled = false;
        lockoutTimer.innerHTML = '';
      }
      return false;
    }

    function renderShows(filterText = '') {
      showsGrid.innerHTML = '';
      const cleanFilter = sanitizeInput(filterText.toLowerCase());

      let filtered = shows;

      if (currentCategory === 'series') {
        filtered = filtered.filter(show => show.category === 'series');
      } else if (currentCategory === 'movie') {
        filtered = filtered.filter(show => show.category === 'movie');
      } else if (currentCategory === 'kids') {
        filtered = filtered.filter(show => show.genre === 'comedy' || (show.title && show.title.includes('أطفال')));
      } else if (currentCategory === 'favorites') {
        filtered = shows.filter(show => favoritesData.includes(show.id));
      } else if (currentCategory === 'history') {
        filtered = shows.filter(show => historyData.includes(show.id));
      } else if (currentCategory === 'watchlist') {
        filtered = shows.filter(show => watchlistData.includes(show.id));
      }

      if (currentGenre !== 'all') {
        filtered = filtered.filter(show => show.genre === currentGenre);
      }

      if (cleanFilter) {
        filtered = filtered.filter(show => show.title.toLowerCase().includes(cleanFilter) || (show.year && show.year.includes(cleanFilter)));
      }

      if (filtered.length === 0) {
        showsGrid.innerHTML = '<p style="grid-column: 1/-1; text-align: center; color: var(--text-secondary); padding: 30px;">لا توجد أية نتائج مطابقة لهذا القسم أو البحث</p>';
        return;
      }

      filtered.forEach(show => {
        const card = document.createElement('div');
        card.className = 'show-card';
        card.onclick = () => openPlayer(show);
        card.innerHTML = `
          ${show.badge ? `<div class="show-badge">${sanitizeInput(show.badge)}</div>` : ''}
          <div class="show-type-tag">${show.category === 'movie' ? 'فيلم' : 'مسلسل'}</div>
          <img src="${sanitizeInput(show.image) || 'https://via.placeholder.com/300x400/222/fff?text=mrstoud'}" alt="${sanitizeInput(show.title)}" class="show-thumb" onerror="this.src='https://via.placeholder.com/300x400/222/fff?text=mrstoud'">
          <div class="show-info">
            <div class="show-title">${sanitizeInput(show.title)}</div>
            <div class="meta-sub-info">
              <span><i class="fas fa-calendar-alt"></i> ${sanitizeInput(show.year || '2026')}</span>
              <span><i class="fas fa-star" style="color:#f1c40f;"></i> ${sanitizeInput(show.rating || '4.5')}</span>
            </div>
          </div>
        `;
        showsGrid.appendChild(card);
      });

      updateCounters();
    }

    window.filterByCategory = function(category, event = null) {
      currentCategory = category;
      
      document.querySelectorAll('.sidebar-menu a').forEach(a => a.classList.remove('active-link'));
      if (event && event.currentTarget) {
        event.currentTarget.classList.add('active-link');
      }

      const titleSpan = sectionTitle.querySelector('span') || sectionTitle;
      if (category === 'series') {
        titleSpan.innerHTML = '<i class="fas fa-tv"></i> قائمة المسلسلات';
      } else if (category === 'movie') {
        titleSpan.innerHTML = '<i class="fas fa-film"></i> قائمة الأفلام';
      } else if (category === 'kids') {
        titleSpan.innerHTML = '<i class="fas fa-child" style="color:#f1c40f;"></i> وضع الأطفال الآمن';
      } else if (category === 'favorites') {
        titleSpan.innerHTML = '<i class="fas fa-heart" style="color:var(--primary-color);"></i> قائمة المفضلة';
      } else if (category === 'history') {
        titleSpan.innerHTML = '<i class="fas fa-history"></i> سجل المشاهدة (Continue Watching)';
      } else if (category === 'watchlist') {
        titleSpan.innerHTML = '<i class="fas fa-clock"></i> قائمة المشاهدة لاحقاً';
      } else {
        titleSpan.innerHTML = '<i class="fas fa-play-circle"></i> جميع الأعمال';
      }

      renderShows(sidebarSearchInput.value);
    };

    window.filterByGenre = function(genre, element) {
      currentGenre = genre;
      document.querySelectorAll('.filter-chip').forEach(chip => chip.classList.remove('active'));
      element.classList.add('active');
      renderShows(sidebarSearchInput.value);
    };

    sidebarSearchInput.addEventListener('input', (e) => {
      renderShows(e.target.value);
    });

    function renderAdminList() {
      adminShowsList.innerHTML = '';
      shows.forEach(show => {
        const item = document.createElement('div');
        item.className = 'admin-item';
        item.innerHTML = `
          <div class="admin-item-title">[${show.category === 'movie' ? 'فيلم' : 'مسلسل'}] ${sanitizeInput(show.title)}</div>
          <div class="admin-actions">
            <button class="sm-btn btn-edit" onclick="editShow(${show.id})"><i class="fas fa-edit"></i> تعديل</button>
            <button class="sm-btn btn-del" onclick="deleteShow(${show.id})"><i class="fas fa-trash"></i> حذف</button>
          </div>
        `;
        adminShowsList.appendChild(item);
      });
    }

    function renderUsersAndBans() {
      usersListContainer.innerHTML = '';
      bannedUsersContainer.innerHTML = '';
      let bannedCount = 0;

      users.forEach(user => {
        const userCard = document.createElement('div');
        userCard.className = 'user-card';
        userCard.innerHTML = `
          <div class="user-info">
            <span class="user-name">${sanitizeInput(user.name)}</span>
            <span class="user-email">${sanitizeInput(user.email)}</span>
          </div>
          <div>
            <span class="status-badge ${user.status === 'banned' ? 'status-banned' : 'status-active'}">
              ${user.status === 'banned' ? 'محظور' : 'نشط'}
            </span>
            ${user.status === 'active' ? `<button class="sm-btn btn-ban" style="margin-right:6px;" onclick="banUserDirect('${user.email}')">حظر</button>` : ''}
          </div>
        `;
        usersListContainer.appendChild(userCard);

        if (user.status === 'banned') {
          bannedCount++;
          const banCard = document.createElement('div');
          banCard.className = 'user-card';
          banCard.innerHTML = `
            <div class="user-info">
              <span class="user-name">${sanitizeInput(user.name)} (${sanitizeInput(user.email)})</span>
              <span class="user-email" style="color: #e74c3c;">السبب: ${sanitizeInput(user.banReason || 'غير محدد')}</span>
            </div>
            <button class="sm-btn btn-unban" onclick="unbanUser('${user.email}')"><i class="fas fa-unlock"></i> فك الحظر</button>
          `;
          bannedUsersContainer.appendChild(banCard);
        }
      });

      if (bannedCount === 0) {
        bannedUsersContainer.innerHTML = '<p style="color:var(--text-secondary); font-size:13px; text-align:center;">لا يوجد مستخدمين محظورين حالياً</p>';
      }
    }

    window.banUserDirect = function(email) {
      const reason = prompt('أدخل سبب الحظر:');
      if (reason !== null) {
        performBan(email, reason);
      }
    };

    function performBan(email, reason) {
      const targetUser = users.find(u => u.email.toLowerCase() === email.toLowerCase());
      if (targetUser) {
        targetUser.status = 'banned';
        targetUser.banReason = reason || 'تم الحظر بقرار من المدير';
      } else {
        users.push({
          id: Date.now(),
          name: email.split('@')[0],
          email: email,
          status: 'banned',
          banReason: reason || 'تم الحظر بقرار من المدير'
        });
      }
      saveUserData();
      showToast(`تم حظر المستخدم (${email}) بنجاح!`);
    }

    window.unbanUser = function(email) {
      const user = users.find(u => u.email.toLowerCase() === email.toLowerCase());
      if (user) {
        user.status = 'active';
        delete user.banReason;
        saveUserData();
        showToast(`تم فك الحظر عن المستخدم (${email}) بنجاح!`);
      }
    };

    banUserForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const email = document.getElementById('banEmail').value;
      const reason = document.getElementById('banReason').value;
      performBan(email, reason);
      banUserForm.reset();
    });

    function saveUserData() {
      localStorage.setItem('mrstoud_users', JSON.stringify(users));
      renderUsersAndBans();
    }

    function playVideoServer(url) {
      if (url && url.trim() !== '') {
        const safeUrl = sanitizeInput(url);
        if (safeUrl.startsWith('blob:') || safeUrl.startsWith('data:video/') || safeUrl.endsWith('.mp4') || safeUrl.endsWith('.webm') || safeUrl.endsWith('.ogg')) {
          videoPlayerBox.innerHTML = `<video controls autoplay style="width:100%; height:100%; background:#000;"><source src="${safeUrl}" type="video/mp4">متصفحك لا يدعم عرض الفيديو.</video>`;
        } else {
          videoPlayerBox.innerHTML = `<iframe id="videoIframe" src="${safeUrl}" allowfullscreen></iframe>`;
        }
      } else {
        videoPlayerBox.innerHTML = `<div style="padding:40px; text-align:center; color:var(--primary-color);"><i class="fas fa-exclamation-circle" style="font-size:30px; margin-bottom:10px;"></i><br>عذراً، لا يوجد فيديو أو رابط تشغيل صالح متاح في هذا السيرفر</div>`;
      }
      applyVideoFilters();
    }

    function renderEpisodesList(show) {
      const episodesBox = document.getElementById('episodesSectionBox');
      const episodesGrid = document.getElementById('episodesGridContainer');
      episodesGrid.innerHTML = '';

      if (show.episodes && show.episodes.length > 0) {
        episodesBox.style.display = 'block';
        show.episodes.forEach((ep, idx) => {
          const btn = document.createElement('div');
          btn.className = `episode-chip ${idx === 0 ? 'active' : ''}`;
          btn.innerHTML = `<i class="fas fa-play"></i> ${sanitizeInput(ep.name)}`;
          btn.onclick = () => {
            document.querySelectorAll('.episode-chip').forEach(c => c.classList.remove('active'));
            btn.classList.add('active');
            playVideoServer(ep.url);
            addPoints(5);
          };
          episodesGrid.appendChild(btn);
        });
        playVideoServer(show.episodes[0].url);
      } else {
        episodesBox.style.display = 'none';
        if (show.videoUrl) {
          playVideoServer(show.videoUrl);
        }
      }
    }

    function renderServerButtons(show) {
      serverSelectorContainer.innerHTML = '';
      const servers = [];

      if (show.videoUrl && show.videoUrl.trim() !== '') {
        servers.push({ name: 'سيرفر 1 (الرئيسي)', url: show.videoUrl });
      }
      if (show.videoUrl2 && show.videoUrl2.trim() !== '') {
        servers.push({ name: 'سيرفر 2 (احتياطي)', url: show.videoUrl2 });
      }
      if (show.videoUrl3 && show.videoUrl3.trim() !== '') {
        servers.push({ name: 'سيرفر 3 (سريع)', url: show.videoUrl3 });
      }

      if (servers.length > 0) {
        servers.forEach((srv, index) => {
          const btn = document.createElement('button');
          btn.className = `server-btn ${index === 0 ? 'active' : ''}`;
          btn.innerHTML = `<i class="fas fa-server"></i> ${srv.name}`;
          btn.onclick = () => {
            document.querySelectorAll('.server-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            playVideoServer(srv.url);
          };
          serverSelectorContainer.appendChild(btn);
        });
      }
    }

    window.toggleCurrentFavorite = function() {
      if (!currentShowId) return;
      const index = favoritesData.indexOf(currentShowId);
      if (index > -1) {
        favoritesData.splice(index, 1);
        document.getElementById('favoriteIcon').className = 'far fa-heart';
        document.getElementById('favoriteBtnText').textContent = 'أضف للمفضلة';
        showToast('تمت الإزالة من المفضلة.');
      } else {
        favoritesData.push(currentShowId);
        document.getElementById('favoriteIcon').className = 'fas fa-heart';
        document.getElementById('favoriteIcon').style.color = 'var(--primary-color)';
        document.getElementById('favoriteBtnText').textContent = 'تم الإضافة للمفضلة';
        addPoints(10);
        showToast('تمت الإضافة إلى المفضلة بنجاح! +10 نقاط');
      }
      localStorage.setItem('mrstoud_favorites', JSON.stringify(favoritesData));
      updateCounters();
    };

    window.toggleCurrentWatchlist = function() {
      if (!currentShowId) return;
      const index = watchlistData.indexOf(currentShowId);
      if (index > -1) {
        watchlistData.splice(index, 1);
        document.getElementById('watchlistIcon').className = 'far fa-clock';
        document.getElementById('watchlistBtnText').textContent = 'المشاهدة لاحقاً';
        showToast('تمت الإزالة من المشاهدة لاحقاً.');
      } else {
        watchlistData.push(currentShowId);
        document.getElementById('watchlistIcon').className = 'fas fa-clock';
        document.getElementById('watchlistIcon').style.color = 'var(--primary-color)';
        document.getElementById('watchlistBtnText').textContent = 'في قائمة المشاهدة';
        showToast('تمت الإضافة إلى المشاهدة لاحقاً!');
      }
      localStorage.setItem('mrstoud_watchlist', JSON.stringify(watchlistData));
      updateCounters();
    };

    window.shareCurrentShow = function() {
      if (navigator.share) {
        navigator.share({
          title: playerTitle.textContent,
          text: 'شاهد هذا العمل الرائع على منصة mrstoud',
          url: window.location.href,
        }).catch(() => {});
      } else {
        navigator.clipboard.writeText(window.location.href);
        showToast('تم نسخ رابط العمل بنجاح!');
      }
    };

    window.rateShow = function(stars) {
      if (!currentShowId) return;
      ratingsData[currentShowId] = stars;
      localStorage.setItem('mrstoud_ratings', JSON.stringify(ratingsData));
      updateStarDisplay(stars);
      addPoints(5);
      showToast(`شكراً لتقييمك! (${stars} نجوم) +5 نقاط.`);
    };

    function updateStarDisplay(stars) {
      const starsEls = document.querySelectorAll('#starRatingContainer .star');
      starsEls.forEach((st, idx) => {
        if (idx < stars) {
          st.classList.add('rated');
        } else {
          st.classList.remove('rated');
        }
      });
    }

    function renderComments(showId) {
      commentsList.innerHTML = '';
      const list = commentsData[showId] || [];

      if (list.length === 0) {
        commentsList.innerHTML = '<p style="color:var(--text-secondary); font-size:12px; text-align:center;">لا توجد تعليقات بعد. كن أول من يعلق!</p>';
        return;
      }

      list.forEach(item => {
        const commentBox = document.createElement('div');
        commentBox.className = 'comment-item';
        commentBox.innerHTML = `
          <div class="comment-header">
            <span><i class="fas fa-user-circle"></i> ${sanitizeInput(item.user)}</span>
            <span>${item.date}</span>
          </div>
          <div>${sanitizeInput(item.text)}</div>
        `;
        commentsList.appendChild(commentBox);
      });
    }

    commentForm.addEventListener('submit', (e) => {
      e.preventDefault();
      if (!currentShowId) return;
      const text = sanitizeInput(document.getElementById('commentText').value);
      let userNameInput = sanitizeInput(document.getElementById('commentUserName').value.trim());
      if (!userNameInput) {
        userNameInput = currentUserSession ? currentUserSession.name : 'مستخدم زائر';
      }

      if (!commentsData[currentShowId]) {
        commentsData[currentShowId] = [];
      }

      commentsData[currentShowId].push({
        user: userNameInput,
        text: text,
        date: new Date().toLocaleDateString('ar-EG')
      });

      localStorage.setItem('mrstoud_comments', JSON.stringify(commentsData));
      document.getElementById('commentText').value = '';
      renderComments(currentShowId);
      addPoints(10);
      showToast('تم إرسال التعليق بنجاح! +10 نقاط');
    });

    function openPlayer(show) {
      currentShowId = show.id;
      playerTitle.textContent = show.title;
      playerQuality.textContent = show.quality || '1080p Full HD';

      if (!historyData.includes(show.id)) {
        historyData.push(show.id);
        localStorage.setItem('mrstoud_history', JSON.stringify(historyData));
      }

      if (favoritesData.includes(show.id)) {
        document.getElementById('favoriteIcon').className = 'fas fa-heart';
        document.getElementById('favoriteIcon').style.color = 'var(--primary-color)';
        document.getElementById('favoriteBtnText').textContent = 'تم الإضافة للمفضلة';
      } else {
        document.getElementById('favoriteIcon').className = 'far fa-heart';
        document.getElementById('favoriteIcon').style.color = '';
        document.getElementById('favoriteBtnText').textContent = 'أضف للمفضلة';
      }

      if (watchlistData.includes(show.id)) {
        document.getElementById('watchlistIcon').className = 'fas fa-clock';
        document.getElementById('watchlistIcon').style.color = 'var(--primary-color)';
        document.getElementById('watchlistBtnText').textContent = 'في قائمة المشاهدة';
      } else {
        document.getElementById('watchlistIcon').className = 'far fa-clock';
        document.getElementById('watchlistIcon').style.color = '';
        document.getElementById('watchlistBtnText').textContent = 'المشاهدة لاحقاً';
      }

      const userRating = ratingsData[show.id] || 0;
      updateStarDisplay(userRating);

      if (show.downloadUrl && show.downloadUrl.trim() !== '') {
        downloadContainer.innerHTML = `<a href="${sanitizeInput(show.downloadUrl)}" class="download-btn" target="_blank"><i class="fas fa-download"></i> تحميل الفيلم / العمل بجودة عالية</a>`;
      } else {
        downloadContainer.innerHTML = '';
      }

      renderServerButtons(show);
      renderEpisodesList(show);
      renderComments(show.id);
      resetVideoTools();

      playerModal.classList.add('active');
    }

    menuToggleBtn.addEventListener('click', () => {
      sidebar.classList.add('open');
      overlay.classList.add('active');
    });

    closeSidebarBtn.addEventListener('click', () => {
      sidebar.classList.remove('open');
      overlay.classList.remove('active');
    });

    overlay.addEventListener('click', () => {
      sidebar.classList.remove('open');
      overlay.classList.remove('active');
    });

    closeModalBtns.forEach(btn => {
      btn.addEventListener('click', () => {
        document.querySelectorAll('.modal').forEach(m => m.classList.remove('active'));
        videoPlayerBox.innerHTML = '';
        if (sleepTimerTimeout) clearTimeout(sleepTimerTimeout);
      });
    });

    adminBtn.addEventListener('click', () => {
      sidebar.classList.remove('open');
      overlay.classList.remove('active');
      if (localStorage.getItem('mrstoud_verified_owner') === 'true') {
        isAdminLoggedIn = true;
        renderAdminList();
        renderUsersAndBans();
        adminModal.classList.add('active');
      } else {
        checkLockoutStatus();
        loginModal.classList.add('active');
      }
    });

    privacyBtn.addEventListener('click', () => {
      sidebar.classList.remove('open');
      overlay.classList.remove('active');
      privacyModal.classList.add('active');
    });

    loginForm.addEventListener('submit', (e) => {
      e.preventDefault();
      if (checkLockoutStatus()) return;

      const pass = document.getElementById('adminPassword').value;
      if (pass === 'admin2026' || pass === 'mrstoudadmin' || pass === 'admin123') {
        isAdminLoggedIn = true;
        localStorage.setItem('mrstoud_verified_owner', 'true');
        localStorage.setItem('mrstoud_login_attempts', '0');
        loginModal.classList.remove('active');
        document.getElementById('adminPassword').value = '';
        renderAdminList();
        renderUsersAndBans();
        adminModal.classList.add('active');
        showToast('مرحباً بك في لوحة الإدارة بصلاحيات كاملة!');
      } else {
        loginAttempts++;
        localStorage.setItem('mrstoud_login_attempts', loginAttempts);
        if (loginAttempts >= 3) {
          lockoutUntil = Date.now() + (24 * 60 * 60 * 1000);
          localStorage.setItem('mrstoud_lockout_until', lockoutUntil);
          checkLockoutStatus();
        } else {
          alert(`كلمة المرور غير صحيحة! محاولات متبقية: ${3 - loginAttempts}`);
        }
      }
    });

    // حفظ أو إضافة عمل جديد مع قراءة الصور والفيديوهات من المعرض ونقله للرئيسية تلقائياً
    saveShowForm.addEventListener('submit', (e) => {
      e.preventDefault();
      
      const editId = document.getElementById('editShowId').value;
      const category = document.getElementById('showCategory').value;
      const genre = document.getElementById('showGenre').value;
      const title = document.getElementById('showTitle').value;
      const badge = document.getElementById('showBadge').value;
      const year = document.getElementById('showYear').value;
      const rating = document.getElementById('showRating').value;
      
      let imageUrl = document.getElementById('showImage').value.trim();
      let videoUrl = document.getElementById('showVideoUrl').value.trim();
      const videoUrl2 = document.getElementById('showVideoUrl2').value.trim();
      const videoUrl3 = document.getElementById('showVideoUrl3').value.trim();
      const quality = document.getElementById('showQuality').value;
      const downloadUrl = document.getElementById('showDownloadUrl').value;
      const episodesText = document.getElementById('showEpisodesInput').value;

      const imageFile = document.getElementById('showImageFile').files[0];
      const videoFile = document.getElementById('showVideoFile').files[0];

      let pendingReads = 0;
      let finalImageUrl = imageUrl;
      let finalVideoUrl = videoUrl;

      if (imageFile) {
        pendingReads++;
        const reader = new FileReader();
        reader.onload = function(evt) {
          finalImageUrl = evt.target.result;
          pendingReads--;
          checkAndSave();
        };
        reader.readAsDataURL(imageFile);
      }

      if (videoFile) {
        pendingReads++;
        const readerVid = new FileReader();
        readerVid.onload = function(evt) {
          finalVideoUrl = evt.target.result;
          pendingReads--;
          checkAndSave();
        };
        readerVid.readAsDataURL(videoFile);
      }

      function checkAndSave() {
        if (pendingReads > 0) return;

        let episodes = [];
        if (episodesText.trim() !== '') {
          const lines = episodesText.split('\n');
          lines.forEach(line => {
            const parts = line.split(':');
            if (parts.length >= 2) {
              const epName = parts[0].trim();
              const epUrl = parts.slice(1).join(':').trim();
              episodes.push({ name: epName, url: epUrl });
            } else if (line.trim() !== '') {
              episodes.push({ name: `حلقة`, url: line.trim() });
            }
          });
        }

        if (editId) {
          const showObj = shows.find(s => s.id == editId);
          if (showObj) {
            showObj.category = category;
            showObj.genre = genre;
            showObj.title = title;
            showObj.badge = badge;
            showObj.year = year;
            showObj.rating = rating;
            if (finalImageUrl) showObj.image = finalImageUrl;
            if (finalVideoUrl) showObj.videoUrl = finalVideoUrl;
            showObj.videoUrl2 = videoUrl2;
            showObj.videoUrl3 = videoUrl3;
            showObj.quality = quality;
            showObj.downloadUrl = downloadUrl;
            showObj.episodes = episodes;
          }
          showToast('تم تحديث العمل بنجاح!');
        } else {
          const newShow = {
            id: Date.now(),
            category,
            genre,
            title,
            badge,
            year,
            rating,
            image: finalImageUrl || 'https://via.placeholder.com/300x400/222/fff?text=mrstoud',
            videoUrl: finalVideoUrl,
            videoUrl2,
            videoUrl3,
            quality,
            downloadUrl,
            episodes
          };
          // إضافة العمل الجديد في بداية القائمة لينتقل تلقائياً للصفحة الرئيسية
          shows.unshift(newShow);
          showToast('تمت إضافة العمل بنجاح وتم نقله إلى الصفحة الرئيسية!');
        }

        saveData();
        renderAdminList();
        
        // إعادة تعيين النموذج والعودة للقسم الرئيسي
        saveShowForm.reset();
        document.getElementById('editShowId').value = '';
        document.getElementById('formSubTitle').textContent = 'إضافة عمل جديد (فيلم / مسلسل)';
        document.getElementById('saveBtn').textContent = 'حفظ وإضافة';
        cancelEditBtn.style.display = 'none';

        // الانتقال تلقائياً للرئيسية وعرض الأعمال
        filterByCategory('all');
      }

      if (pendingReads === 0) {
        checkAndSave();
      }
    });

    window.editShow = function(id) {
      const show = shows.find(s => s.id === id);
      if (!show) return;

      document.getElementById('editShowId').value = show.id;
      document.getElementById('showCategory').value = show.category;
      document.getElementById('showGenre').value = show.genre || 'action';
      document.getElementById('showTitle').value = show.title;
      document.getElementById('showBadge').value = show.badge || '';
      document.getElementById('showYear').value = show.year || '2026';
      document.getElementById('showRating').value = show.rating || '4.8';
      document.getElementById('showImage').value = show.image && !show.image.startsWith('data:') ? show.image : '';
      document.getElementById('showVideoUrl').value = show.videoUrl && !show.videoUrl.startsWith('data:') ? show.videoUrl : '';
      document.getElementById('showVideoUrl2').value = show.videoUrl2 || '';
      document.getElementById('showVideoUrl3').value = show.videoUrl3 || '';
      document.getElementById('showQuality').value = show.quality || '1080p';
      document.getElementById('showDownloadUrl').value = show.downloadUrl || '';

      let epStr = '';
      if (show.episodes && show.episodes.length > 0) {
        epStr = show.episodes.map(ep => `${ep.name}: ${ep.url}`).join('\n');
      }
      document.getElementById('showEpisodesInput').value = epStr;

      document.getElementById('formSubTitle').textContent = 'تعديل بيانات العمل';
      document.getElementById('saveBtn').textContent = 'حفظ التعديلات';
      cancelEditBtn.style.display = 'block';

      adminModal.querySelector('.modal-content').scrollTop = 0;
    };

    cancelEditBtn.addEventListener('click', () => {
      saveShowForm.reset();
      document.getElementById('editShowId').value = '';
      document.getElementById('formSubTitle').textContent = 'إضافة عمل جديد (فيلم / مسلسل)';
      document.getElementById('saveBtn').textContent = 'حفظ وإضافة';
      cancelEditBtn.style.display = 'none';
    });

    window.deleteShow = function(id) {
      if (confirm('هل أنت متأكد من حذف هذا العمل نهائياً؟')) {
        shows = shows.filter(s => s.id !== id);
        saveData();
        renderAdminList();
        showToast('تم حذف العمل بنجاح.');
      }
    };

    function saveData() {
      localStorage.setItem('mrstoud_shows', JSON.stringify(shows));
      renderShows();
      updateCounters();
    }

    // التهيئة الأولية
    checkFirstVisit();
    renderShows();
    updateCounters();
  </script>
</body>
</html>
