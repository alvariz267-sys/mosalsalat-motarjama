<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
  <title>mrstoud - منصة الأفلام والمسلسلات</title>
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

    html, body {
      width: 100%;
      max-width: 100%;
      overflow-x: hidden;
      margin: 0;
      padding: 0;
      background-color: var(--bg-color);
      color: var(--text-color);
      direction: rtl;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      -webkit-tap-highlight-color: transparent;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    /* Navbar */
    .navbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      background-color: #050505;
      padding: 12px 15px;
      position: sticky;
      top: 0;
      z-index: 100;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.8);
      border-bottom: 1px solid var(--border-color);
      width: 100%;
    }

    .brand {
      font-size: 22px;
      font-weight: 800;
      color: var(--primary-color);
      text-decoration: none;
      letter-spacing: 1px;
    }

    .nav-actions {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .icon-btn {
      background: none;
      border: none;
      color: var(--text-color);
      font-size: 18px;
      padding: 8px;
      cursor: pointer;
      border-radius: 50%;
      transition: background 0.2s, color 0.2s;
    }

    .icon-btn:hover, .icon-btn:active {
      background-color: #222;
      color: var(--primary-color);
    }

    /* Sidebar */
    .sidebar {
      position: fixed;
      top: 0;
      right: -280px;
      width: 260px;
      max-width: 80%;
      height: 100%;
      background-color: var(--sidebar-bg);
      box-shadow: -4px 0 15px rgba(0, 0, 0, 0.8);
      transition: right 0.3s cubic-bezier(0.4, 0, 0.2, 1);
      z-index: 200;
      padding: 20px 15px;
      display: flex;
      flex-direction: column;
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
      font-size: 18px;
      color: var(--primary-color);
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
      gap: 12px;
      padding: 12px;
      border-radius: 6px;
      background: none;
      border: none;
      cursor: pointer;
      width: 100%;
      text-align: right;
      transition: background 0.2s;
    }

    .sidebar-menu a:hover, .sidebar-menu button:hover {
      background-color: #222;
      color: var(--primary-color);
    }

    .overlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0,0,0,0.7);
      backdrop-filter: blur(2px);
      display: none;
      z-index: 150;
    }

    .overlay.active {
      display: block;
    }

    /* Search Box */
    .search-container {
      padding: 10px 15px;
      max-width: 1200px;
      margin: 0 auto;
      display: none;
    }

    .search-container.active {
      display: block;
    }

    .search-input {
      width: 100%;
      padding: 10px 14px;
      border-radius: 8px;
      border: 1px solid var(--border-color);
      background-color: #1a1a1a;
      color: #fff;
      font-size: 14px;
      outline: none;
    }

    .search-input:focus {
      border-color: var(--primary-color);
    }

    /* Main Container & Grid */
    .container {
      width: 100%;
      max-width: 1200px;
      margin: 15px auto;
      padding: 0 10px;
    }

    /* Ad Banner */
    .ad-banner {
      background: linear-gradient(135deg, #1f1f1f, #141414);
      border: 1px dashed var(--primary-color);
      color: var(--text-secondary);
      text-align: center;
      padding: 12px;
      margin-bottom: 15px;
      border-radius: 8px;
      font-size: 12px;
      word-break: break-word;
    }

    /* Responsive Grid for all mobile screens */
    .shows-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
      gap: 10px;
      width: 100%;
    }

    @media (min-width: 480px) {
      .shows-grid {
        grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
        gap: 14px;
      }
    }

    @media (min-width: 768px) {
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
      box-shadow: 0 4px 12px rgba(0,0,0,0.4);
      transition: transform 0.2s;
      cursor: pointer;
      width: 100%;
    }

    .show-card:hover {
      transform: translateY(-3px);
    }

    .show-badge {
      position: absolute;
      top: 6px;
      right: 6px;
      background-color: var(--primary-color);
      color: #fff;
      padding: 2px 6px;
      font-size: 10px;
      border-radius: 4px;
      font-weight: bold;
      z-index: 2;
    }

    .show-thumb {
      width: 100%;
      height: 190px;
      object-fit: cover;
      display: block;
    }

    @media (min-width: 480px) {
      .show-thumb {
        height: 230px;
      }
    }

    .show-info {
      padding: 8px;
      text-align: center;
    }

    .show-title {
      font-size: 13px;
      font-weight: 600;
      color: #fff;
      white-space: nowrap;
      overflow: hidden;
      text-overflow: ellipsis;
    }

    /* Modals */
    .modal {
      display: none;
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background-color: rgba(0,0,0,0.85);
      z-index: 300;
      justify-content: center;
      align-items: center;
      padding: 10px;
      overflow-y: auto;
    }

    .modal.active {
      display: flex;
    }

    .modal-content {
      background-color: var(--card-bg);
      border-radius: 10px;
      max-width: 550px;
      width: 100%;
      padding: 18px;
      box-shadow: 0 8px 24px rgba(0,0,0,0.7);
      max-height: 90vh;
      overflow-y: auto;
      border: 1px solid var(--border-color);
    }

    .modal-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 15px;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 8px;
    }

    .close-btn {
      background: none;
      border: none;
      color: #fff;
      font-size: 20px;
      cursor: pointer;
    }

    /* Admin Tabs */
    .admin-tabs {
      display: flex;
      gap: 8px;
      margin-bottom: 15px;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 8px;
    }

    .tab-btn {
      flex: 1;
      padding: 8px;
      background: #111;
      border: 1px solid var(--border-color);
      color: #fff;
      border-radius: 6px;
      font-size: 13px;
      cursor: pointer;
    }

    .tab-btn.active {
      background: var(--primary-color);
      border-color: var(--primary-color);
      font-weight: bold;
    }

    .tab-content {
      display: none;
    }

    .tab-content.active {
      display: block;
    }

    .form-group {
      margin-bottom: 12px;
    }

    .form-group label {
      display: block;
      margin-bottom: 5px;
      font-size: 12px;
      color: var(--text-secondary);
    }

    .form-group input, .form-group select {
      width: 100%;
      padding: 10px;
      border-radius: 6px;
      border: 1px solid var(--border-color);
      background-color: #121212;
      color: #fff;
      font-size: 13px;
      outline: none;
    }

    .form-group input:focus {
      border-color: var(--primary-color);
    }

    .btn {
      width: 100%;
      padding: 11px;
      background-color: var(--primary-color);
      color: #fff;
      border: none;
      border-radius: 6px;
      font-size: 14px;
      cursor: pointer;
      font-weight: bold;
      transition: background 0.2s;
    }

    .btn:hover {
      background-color: var(--primary-hover);
    }

    .btn-secondary {
      background-color: #333;
      margin-top: 8px;
    }

    /* Video Player Modal Elements */
    .video-container {
      position: relative;
      padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
      height: 0;
      overflow: hidden;
      border-radius: 8px;
      background-color: #000;
      margin-bottom: 15px;
      width: 100%;
    }

    .video-container iframe, .video-container video {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      border: 0;
    }

    .video-details {
      display: flex;
      flex-direction: column;
      gap: 10px;
    }

    .quality-tags {
      display: flex;
      gap: 8px;
      align-items: center;
      flex-wrap: wrap;
    }

    .quality-tag {
      background-color: #2a2a2a;
      color: #fff;
      padding: 3px 8px;
      border-radius: 4px;
      font-size: 11px;
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
      padding: 10px;
      border-radius: 6px;
      font-weight: bold;
      font-size: 13px;
      text-al