<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MrStoud - منصة الأفلام والمسلسلات</title>
  <style>
    :root {
      --bg-color: #0f172a;
      --card-bg: #1e293b;
      --accent-color: #e50914;
      --text-color: #f8fafc;
      --text-muted: #94a3b8;
    }
    body {
      background-color: var(--bg-color);
      color: var(--text-color);
      font-family: Tahoma, sans-serif;
      margin: 0;
      padding: 0;
    }
    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      padding: 15px 30px;
      background: var(--card-bg);
      border-bottom: 1px solid #334155;
    }
    .logo { color: var(--accent-color); font-size: 24px; font-weight: bold; text-decoration: none; }
    .header-actions { display: flex; gap: 15px; align-items: center; }
    .btn { background: var(--accent-color); color: #fff; border: none; padding: 8px 15px; border-radius: 5px; cursor: pointer; font-weight: bold; }
    .btn:hover { opacity: 0.9; }
    
    /* أزرار الإشعارات والمفضلة العلويّة */
    .icon-btn {
      position: relative;
      cursor: pointer;
      font-size: 18px;
      background: #334155;
      padding: 8px 12px;
      border-radius: 50%;
      border: none;
      color: white;
    }
    .badge {
      position: absolute;
      top: -5px;
      right: -5px;
      background: var(--accent-color);
      color: white;
      font-size: 11px;
      padding: 2px 6px;
      border-radius: 50%;
    }
    
    /* النوافذ المنبثقة */
    .dropdown-modal {
      position: fixed;
      top: 70px;
      left: 20px;
      width: 320px;
      background: var(--card-bg);
      border: 1px solid #334155;
      border-radius: 10px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.5);
      display: none;
      z-index: 1000;
      max-height: 400px;
      overflow-y: auto;
      padding: 15px;
    }
    .dropdown-modal.active { display: block; }
    
    .container { padding: 20px; max-width: 1200px; margin: auto; }
    .shows-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); gap: 20px; margin-top: 20px; }
    .show-card { background: var(--card-bg); border-radius: 8px; overflow: hidden; border: 1px solid #334155; padding: 15px; text-align: center; }
    
    .modal {
      position: fixed; top: 0; left: 0; width: 100%; height: 100%;
      background: rgba(0,0,0,0.85); display: none; justify-content: center; align-items: center; z-index: 3000;
    }
    .modal.active { display: flex; }
    .modal-content { background: var(--card-bg); padding: 25px; border-radius: 10px; width: 90%; max-width: 450px; border: 1px solid #334155; }
  </style>
</head>
<body>

  <!-- بوابة حماية تسجيل الدخول وتأكيد البريد الإلكتروني (الميزة الجديدة الإجبارية للتشغيل) -->
  <div class="modal active" id="authGateModal">
    <div class="modal-content" style="text-align: center;">
      <h3 style="color: var(--accent-color); margin-top: 0;">MrStoud - بوابة التحقق الأمني</h3>
      <p style="color: var(--text-muted); font-size: 13px; line-height: 1.6;">عذراً، لا يمكن تصفح الموقع أو مشاهدة المحتوى إلا بعد تسجيل الدخول وتأكيد مصدقية بريدك الإلكتروني.</p>
      
      <!-- الخطوة الأولى: إدخال البريد -->
      <div id="authStep1">
        <input type="email" id="gateEmailInput" placeholder="أدخل بريدك الإلكتروني الشخصي" required style="width:100%; padding: 10px; margin-bottom: 12px; border-radius: 5px; border: 1px solid #334155; background: #0f172a; color: white; box-sizing: border-box;">
        <button class="btn" id="gateSendCodeBtn" style="width: 100%;">إرسال كود التحقق</button>
      </div>

      <!-- الخطوة الثانية: إدخال كود التحقق -->
      <div id="authStep2" style="display: none; margin-top: 15px;">
        <p style="font-size: 12px; color: #10b981; margin-bottom: 10px;">تم إرسال كود التحقق (تجاربي: 1234) إلى بريدك بنجاح.</p>
        <input type="text" id="gateCodeInput" placeholder="أدخل كود التحقق (4 أرقام)" style="width:100%; padding: 10px; margin-bottom: 12px; border-radius: 5px; border: 1px solid #334155; background: #0f172a; color: white; text-align: center; letter-spacing: 5px; box-sizing: border-box;" maxlength="4">
        <button class="btn" id="gateVerifyBtn" style="width: 100%;">تأكيد ودخول الموقع</button>
      </div>
    </div>
  </div>

  <header>
    <a href="#" class="logo">MrStoud</a>
    <div class="header-actions">
      <!-- زر المفضلة -->
      <button class="icon-btn" id="watchlistBtn" title="قائمتي المفضلة">
        ❤️
        <span class="badge" id="watchlistBadge">0</span>
      </button>

      <!-- زر الإشعارات -->
      <button class="icon-btn" id="notificationBell" title="الإشعارات">
        🔔
        <span class="badge" id="notificationBadge">0</span>
      </button>

      <button class="btn" id="adminBtn">لوحة التحكم</button>
    </div>
  </header>

  <!-- نافذة قائمة المفضلة -->
  <div class="dropdown-modal" id="watchlistModalBox" style="left: 75px;">
    <h4 style="margin-top: 0; border-bottom: 1px solid #334155; padding-bottom: 8px;">قائمة المفضلة ❤️</h4>
    <div id="watchlistItemsList">
      <div style="text-align: center; color: var(--text-muted); padding: 15px;">قائمتك فارغة حالياً</div>
    </div>
  </div>

  <!-- نافذة الإشعارات -->
  <div class="dropdown-modal" id="notificationModalBox">
    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
      <h4 style="margin: 0;">آخر التنبيهات</h4>
      <button class="btn" style="font-size: 10px; padding: 3px 8px;" id="clearNotifications">تحديد كمقروء</button>
    </div>
    <div id="notificationsList">
      <div style="text-align: center; color: var(--text-muted); padding: 20px;">لا توجد إشعارات جديدة</div>
    </div>
  </div>

  <div class="container">
    <h2>أحدث الأفلام والمسلسلات</h2>
    <div class="shows-grid" id="showsContainer">
      <!-- يتم تعبئة الأعمال برمجياً هنا -->
    </div>
  </div>

  <!-- لوحة تحكم المالك -->
  <div class="modal" id="adminModal" style="background: rgba(0,0,0,0.7);">
    <div class="modal-content" style="max-width: 700px; max-height: 80vh; overflow-y: auto;">
      <h3>لوحة تحكم المالك</h3>
      <form id="saveShowForm">
        <input type="hidden" id="editShowId">
        <div style="margin-bottom: 10px;">
          <label>نوع العمل:</label>
          <select id="showCategory" style="width:100%; padding: 8px; margin-top:5px; background:#0f172a; color:white; border:1px solid #334155;">
            <option value="movie">فيلم</option>
            <option value="series">مسلسل</option>
          </select>
        </div>
        <div style="margin-bottom: 10px;">
          <label>اسم العمل:</label>
          <input type="text" id="showTitle" required style="width:100%; padding: 8px; margin-top:5px; background:#0f172a; color:white; border:1px solid #334155; box-sizing:border-box;">
        </div>
        <div style="margin-bottom: 10px;">
          <label>الحلقات (اكتب كل حلقة في سطر: الحلقة 1: رابط):</label>
          <textarea id="showEpisodesInput" rows="3" style="width:100%; padding: 8px; margin-top:5px; background:#0f172a; color:white; border:1px solid #334155; box-sizing:border-box;"></textarea>
        </div>
        <button type="submit" class="btn" id="saveBtn">حفظ وإضافة العمل</button>
      </form>
    </div>
  </div>

  <!-- نافذة تسجيل الدخول للمدير -->
  <div class="modal" id="loginModal" style="background: rgba(0,0,0,0.7);">
    <div class="modal-content">
      <h3>تسجيل دخول المدير</h3>
      <form id="loginForm">
        <input type="password" id="adminPassword" placeholder="كلمة المرور" required style="width:100%; padding: 10px; margin-bottom: 15px; background:#0f172a; color:white; border:1px solid #334155; box-sizing:border-box;">
        <button type="submit" class="btn" style="width:100%;">دخول</button>
      </form>
    </div>
  </div>

  <script>
    // نظام التحقق الإجباري من البريد قبل تشغيل الموقع
    const authGateModal = document.getElementById('authGateModal');
    const authStep1 = document.getElementById('authStep1');
    const authStep2 = document.getElementById('authStep2');
    const gateEmailInput = document.getElementById('gateEmailInput');
    const gateSendCodeBtn = document.getElementById('gateSendCodeBtn');
    const gateCodeInput = document.getElementById('gateCodeInput');
    const gateVerifyBtn = document.getElementById('gateVerifyBtn');

    let isUserVerified = localStorage.getItem('mrstoud_user_verified') === 'true';

    // فحص حالة التحقق عند تحميل الصفحة
    if (isUserVerified) {
      authGateModal.classList.remove('active');
    } else {
      authGateModal.classList.add('active');
    }

    gateSendCodeBtn.addEventListener('click', () => {
      const email = gateEmailInput.value.trim();
      if (!email || !email.includes('@') || !email.includes('.')) {
        alert('الرجاء إدخال بريد إلكتروني صالح وموثق!');
        return;
      }
      localStorage.setItem('mrstoud_temp_email', email);
      authStep1.style.display = 'none';
      authStep2.style.display = 'block';
    });

    gateVerifyBtn.addEventListener('click', () => {
      const code = gateCodeInput.value.trim();
      if (code === '1234') { // الكود التجريبي المعتمد للتحقق
        localStorage.setItem('mrstoud_user_verified', 'true');
        authGateModal.classList.remove('active');
        alert('تم تأكيد بريدك الإلكتروني بنجاح! مرحباً بك في منصة MrStoud.');
        renderShows();
      } else {
        alert('كود التحقق غير صحيح! (الكود التجريبي هو: 1234)');
      }
    });

    // البيانات والمتغيرات الأساسية للمنصة
    let shows = JSON.parse(localStorage.getItem('mrstoud_shows')) || [
      { id: 1, category: 'movie', title: 'فيلم تجريبي', episodes: [] }
    ];
    let notifications = JSON.parse(localStorage.getItem('mrstoud_notifications')) || [];
    let watchlist = JSON.parse(localStorage.getItem('mrstoud_watchlist')) || [];
    let isAdminLoggedIn = localStorage.getItem('mrstoud_verified_owner') === 'true';

    const adminBtn = document.getElementById('adminBtn');
    const adminModal = document.getElementById('adminModal');
    const loginModal = document.getElementById('loginModal');
    const loginForm = document.getElementById('loginForm');
    const saveShowForm = document.getElementById('saveShowForm');
    const showsContainer = document.getElementById('showsContainer');

    const notificationBell = document.getElementById('notificationBell');
    const notificationModalBox = document.getElementById('notificationModalBox');
    const notificationsList = document.getElementById('notificationsList');
    const notificationBadge = document.getElementById('notificationBadge');
    const clearNotificationsBtn = document.getElementById('clearNotifications');

    const watchlistBtn = document.getElementById('watchlistBtn');
    const watchlistModalBox = document.getElementById('watchlistModalBox');
    const watchlistItemsList = document.getElementById('watchlistItemsList');
    const watchlistBadge = document.getElementById('watchlistBadge');

    function sanitizeInput(str) {
      const temp = document.createElement('div');
      temp.textContent = str;
      return temp.innerHTML;
    }

    function showToast(msg) {
      alert(msg);
    }

    function renderShows() {
      if (!localStorage.getItem('mrstoud_user_verified')) return;
      if (shows.length === 0) {
        showsContainer.innerHTML = '<p style="color: var(--text-muted);">لا توجد أعمال مضافة حالياً.</p>';
        return;
      }

      showsContainer.innerHTML = shows.map(show => {
        const isFav = watchlist.some(item => item.id === show.id);
        return `
          <div class="show-card">
            <h4>${show.title}</h4>
            <p style="font-size: 12px; color: var(--text-muted);">${show.category === 'movie' ? '🎬 فيلم' : '📺 مسلسل'}</p>
            <button class="btn" style="background: ${isFav ? '#334155' : 'var(--accent-color)'}; font-size: 12px; padding: 5px 10px;" onclick="toggleWatchlist(${show.id})">
              ${isFav ? '❤️ إزالة من المفضلة' : '🤍 إضافة للمفضلة'}
            </button>
          </div>
        `;
      }).join('');
    }

    window.toggleWatchlist = function(showId) {
      const show = shows.find(s => s.id === showId);
      if (!show) return;

      const index = watchlist.findIndex(item => item.id === showId);
      if (index > -1) {
        watchlist.splice(index, 1);
        showToast('تمت الإزالة من قائمتك المفضلة');
      } else {
        watchlist.push(show);
        showToast('تمت الإضافة إلى قائمتك المفضلة ❤️');
      }

      localStorage.setItem('mrstoud_watchlist', JSON.stringify(watchlist));
      updateWatchlistUI();
      renderShows();
    };

    function updateWatchlistUI() {
      watchlistBadge.textContent = watchlist.length;
      watchlistBadge.style.display = watchlist.length > 0 ? 'inline-block' : 'none';

      if (watchlist.length === 0) {
        watchlistItemsList.innerHTML = '<div style="text-align: center; color: var(--text-muted); padding: 15px;">قائمتك فارغة حالياً</div>';
        return;
      }

      watchlistItemsList.innerHTML = watchlist.map(item => `
        <div style="display: flex; justify-content: space-between; align-items: center; padding: 8px 0; border-bottom: 1px solid #334155; font-size: 13px;">
          <span>${item.title}</span>
          <button onclick="toggleWatchlist(${item.id})" style="background:none; border:none; color: #e50914; cursor:pointer; font-size: 14px;" title="حذف">❌</button>
        </div>
      `).join('');
    }

    watchlistBtn.addEventListener('click', () => {
      watchlistModalBox.classList.toggle('active');
      notificationModalBox.classList.remove('active');
    });

    function addNotification(text) {
      const newNotif = {
        id: Date.now(),
        text: text,
        time: new Date().toLocaleTimeString('ar-EG', { hour: '2-digit', minute: '2-digit' }),
        read: false
      };
      notifications.unshift(newNotif);
      localStorage.setItem('mrstoud_notifications', JSON.stringify(notifications));
      updateNotificationUI();
    }

    function updateNotificationUI() {
      const unreadCount = notifications.filter(n => !n.read).length;
      notificationBadge.textContent = unreadCount;
      notificationBadge.style.display = unreadCount > 0 ? 'inline-block' : 'none';

      if (notifications.length === 0) {
        notificationsList.innerHTML = '<div style="text-align: center; color: var(--text-muted); padding: 20px;">لا توجد إشعارات جديدة</div>';
        return;
      }

      notificationsList.innerHTML = notifications.map(n => `
        <div style="background: ${n.read ? 'transparent' : '#334155'}; border-radius: 5px; margin-bottom: 5px; padding: 8px; font-size: 13px;">
          <div>${n.text}</div>
          <div style="font-size: 10px; color: var(--text-muted); margin-top: 4px;">${n.time}</div>
        </div>
      `).join('');
    }

    notificationBell.addEventListener('click', () => {
      notificationModalBox.classList.toggle('active');
      watchlistModalBox.classList.remove('active');
      notifications.forEach(n => n.read = true);
      localStorage.setItem('mrstoud_notifications', JSON.stringify(notifications));
      updateNotificationUI();
    });

    clearNotificationsBtn.addEventListener('click', () => {
      notifications = [];
      localStorage.setItem('mrstoud_notifications', JSON.stringify(notifications));
      updateNotificationUI();
    });

    saveShowForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const category = document.getElementById('showCategory').value;
      const title = sanitizeInput(document.getElementById('showTitle').value);
      
      const episodesRaw = document.getElementById('showEpisodesInput').value;
      let episodes = [];
      if (episodesRaw.trim() !== '') {
        episodesRaw.split('\n').forEach(line => {
          const parts = line.split(':');
          if (parts.length >= 2) {
            episodes.push({ name: parts[0].trim(), url: parts.slice(1).join(':').trim() });
          }
        });
      }

      const newShow = { id: Date.now(), category, title, episodes };
      shows.unshift(newShow);
      localStorage.setItem('mrstoud_shows', JSON.stringify(shows));

      if (category === 'movie') {
        addNotification(`🎬 تم إضافة فيلم جديد: "${title}"`);
      } else {
        addNotification(`📺 تم إضافة مسلسل جديد: "${title}"`);
      }

      saveShowForm.reset();
      adminModal.classList.remove('active');
      renderShows();
      showToast('تمت إضافة العمل بنجاح!');
    });

    adminBtn.addEventListener('click', () => {
      if (isAdminLoggedIn) {
        adminModal.classList.add('active');
      } else {
        loginModal.classList.add('active');
      }
    });

    loginForm.addEventListener('submit', (e) => {
      e.preventDefault();
      if (document.getElementById('adminPassword').value === "mrstoud2026") {
        isAdminLoggedIn = true;
        localStorage.setItem('mrstoud_verified_owner', 'true');
        loginModal.classList.remove('active');
        document.getElementById('adminPassword').value = '';
        adminModal.classList.add('active');
        showToast('مرحباً بك في لوحة التحكم!');
      } else {
        alert('كلمة المرور غير صحيحة!');
      }
    });

    // التهيئة الأولية للموقع بعد التحقق
    if (isUserVerified) {
      renderShows();
    }
    updateNotificationUI();
    updateWatchlistUI();
  </script>
</body>
</html>
