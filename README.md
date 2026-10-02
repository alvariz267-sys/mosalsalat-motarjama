<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>MrStoud - منصة الأفلام والمسلسلات</title>
  <!-- يمكنك هنا وضع الروابط والتنسيقات الخاصة بك -->
  <style>
    /* التنسيقات الأساسية المدمجة لضمان عمل المنصة بكفاءة وسلاسة */
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
    
    /* أيقونة الإشعارات الجديدة */
    .notification-bell {
      position: relative;
      cursor: pointer;
      font-size: 20px;
      background: #334155;
      padding: 8px 12px;
      border-radius: 50%;
    }
    .notification-badge {
      position: absolute;
      top: -5px;
      right: -5px;
      background: var(--accent-color);
      color: white;
      font-size: 11px;
      padding: 2px 6px;
      border-radius: 50%;
    }
    .notification-modal {
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
    .notification-modal.active { display: block; }
    .notification-item {
      padding: 10px;
      border-bottom: 1px solid #334155;
      font-size: 13px;
    }
    .notification-item:last-child { border-bottom: none; }
    .notification-time { font-size: 10px; color: var(--text-muted); margin-top: 4px; }

    /* بقية التنسيقات والواجهات */
    .container { padding: 20px; max-width: 1200px; margin: auto; }
    .modal {
      position: fixed; top: 0; left: 0; width: 100%; height: 100%;
      background: rgba(0,0,0,0.7); display: none; justify-content: center; align-items: center; z-index: 2000;
    }
    .modal.active { display: flex; }
    .modal-content { background: var(--card-bg); padding: 25px; border-radius: 10px; width: 90%; max-width: 500px; }
  </style>
</head>
<body>

  <header>
    <a href="#" class="logo">MrStoud</a>
    <div class="header-actions">
      <!-- أيقونة الإشعارات المضافة حديثاً -->
      <div class="notification-bell" id="notificationBell" title="الإشعارات والتنبيهات">
        🔔
        <span class="notification-badge" id="notificationBadge">0</span>
      </div>
      <button class="btn" id="adminBtn">لوحة التحكم</button>
    </div>
  </header>

  <!-- نافذة عرض الإشعارات للمستخدمين -->
  <div class="notification-modal" id="notificationModalBox">
    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px;">
      <h4 style="margin: 0;">آخر التنبيهات والإضافات</h4>
      <button class="btn" style="font-size: 10px; padding: 3px 8px;" id="clearNotifications">تحديد كمقروء</button>
    </div>
    <div id="notificationsList">
      <div style="text-align: center; color: var(--text-muted); padding: 20px;">لا توجد إشعارات جديدة حالياً</div>
    </div>
  </div>

  <div class="container">
    <h2>مرحباً بك في منصة MrStoud</h2>
    <p>تابع أحدث الأفلام والمسلسلات والحلقات المضافة بشكل فورى عبر نظام التنبيهات الجديد.</p>
  </div>

  <!-- لوحة تسجيل الدخول وإدارة المحتوى (محافظ على الكود الأصلي بالكامل) -->
  <div class="modal" id="adminModal">
    <div class="modal-content" style="max-width: 700px; max-height: 80vh; overflow-y: auto;">
      <h3>لوحة تحكم المالك</h3>
      <form id="saveShowForm">
        <input type="hidden" id="editShowId">
        <div style="margin-bottom: 10px;">
          <label>نوع العمل:</label>
          <select id="showCategory" style="width:100%; padding: 8px; margin-top:5px;">
            <option value="movie">فيلم</option>
            <option value="series">مسلسل</option>
          </select>
        </div>
        <div style="margin-bottom: 10px;">
          <label>اسم العمل:</label>
          <input type="text" id="showTitle" required style="width:100%; padding: 8px; margin-top:5px;" placeholder="مثال: مسلسل Breaking Bad أو فيلم Inception">
        </div>
        <div style="margin-bottom: 10px;">
          <label>الحلقات (للمسلسلات - اكتب كل حلقة في سطر بالشكل: الحلقة 1: رابط_الحلقة):</label>
          <textarea id="showEpisodesInput" rows="4" style="width:100%; padding: 8px; margin-top:5px;" placeholder="الحلقة 1: https://...&#10;الحلقة 2: https://..."></textarea>
        </div>
        <button type="submit" class="btn" id="saveBtn">حفظ وإضافة العمل</button>
        <button type="button" class="btn" id="cancelEditBtn" style="background:#475569; display:none;">إلغاء</button>
      </form>
    </div>
  </div>

  <!-- نافذة تسجيل الدخول للمدير -->
  <div class="modal" id="loginModal">
    <div class="modal-content">
      <h3>تسجيل دخول المدير</h3>
      <form id="loginForm">
        <input type="password" id="adminPassword" placeholder="كلمة المرور" required style="width:100%; padding: 10px; margin-bottom: 15px;">
        <button type="submit" class="btn" style="width:100%;">دخول</button>
      </form>
    </div>
  </div>

  <script>
    // تهيئة البيانات والمتغيرات الأساسية مع الحفاظ على النظام الأصلي
    let shows = JSON.parse(localStorage.getItem('mrstoud_shows')) || [];
    let notifications = JSON.parse(localStorage.getItem('mrstoud_notifications')) || [];
    let isAdminLoggedIn = localStorage.getItem('mrstoud_verified_owner') === 'true';

    const adminBtn = document.getElementById('adminBtn');
    const adminModal = document.getElementById('adminModal');
    const loginModal = document.getElementById('loginModal');
    const loginForm = document.getElementById('loginForm');
    const saveShowForm = document.getElementById('saveShowForm');
    const cancelEditBtn = document.getElementById('cancelEditBtn');
    
    const notificationBell = document.getElementById('notificationBell');
    const notificationModalBox = document.getElementById('notificationModalBox');
    const notificationsList = document.getElementById('notificationsList');
    const notificationBadge = document.getElementById('notificationBadge');
    const clearNotificationsBtn = document.getElementById('clearNotifications');

    function sanitizeInput(str) {
      const temp = document.createElement('div');
      temp.textContent = str;
      return temp.innerHTML;
    }

    function showToast(msg) {
      alert(msg); // يمكنك استبدالها بنظام التنبيه الخاص بك مسبقاً
    }

    // إدارة نظام الإشعارات وتحديثها
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
        notificationsList.innerHTML = '<div style="text-align: center; color: var(--text-muted); padding: 20px;">لا توجد إشعارات حالياً</div>';
        return;
      }

      notificationsList.innerHTML = notifications.map(n => `
        <div class="notification-item" style="background: ${n.read ? 'transparent' : '#334155'}; border-radius: 5px; margin-bottom: 5px; padding: 8px;">
          <div>${n.text}</div>
          <div class="notification-time">${n.time}</div>
        </div>
      `).join('');
    }

    notificationBell.addEventListener('click', () => {
      notificationModalBox.classList.toggle('active');
      // عند فتح الإشعارات يتم جعلها مقروءة
      notifications.forEach(n => n.read = true);
      localStorage.setItem('mrstoud_notifications', JSON.stringify(notifications));
      updateNotificationUI();
    });

    clearNotificationsBtn.addEventListener('click', () => {
      notifications = [];
      localStorage.setItem('mrstoud_notifications', JSON.stringify(notifications));
      updateNotificationUI();
    });

    function resetAdminForm() {
      saveShowForm.reset();
      document.getElementById('editShowId').value = '';
      cancelEditBtn.style.display = 'none';
    }

    cancelEditBtn.addEventListener('click', resetAdminForm);

    // دالة الحفظ مع توليد إشعارات دقيقة للأفلام، المسلسلات، والحلقات الجديدة
    saveShowForm.addEventListener('submit', (e) => {
      e.preventDefault();
      const id = document.getElementById('editShowId').value;
      const category = document.getElementById('showCategory').value;
      const title = sanitizeInput(document.getElementById('showTitle').value);
      
      const episodesRaw = document.getElementById('showEpisodesInput').value;
      let episodes = [];
      if (episodesRaw.trim() !== '') {
        const lines = episodesRaw.split('\n');
        lines.forEach(line => {
          const parts = line.split(':');
          if (parts.length >= 2) {
            const epName = parts[0].trim();
            const epUrl = parts.slice(1).join(':').trim();
            episodes.push({ name: epName, url: epUrl });
          }
        });
      }

      if (id) {
        // تحديث عمل سابق
        const index = shows.findIndex(s => s.id == id);
        if (index > -1) {
          const oldShow = shows[index];
          shows[index] = { ...oldShow, category, title, episodes };
          
          // التحقق إذا تمت إضافة حلقات جديدة للمسلسل
          if (category === 'series' && episodes.length > oldShow.episodes.length) {
            const newEpisodesCount = episodes.length - oldShow.episodes.length;
            const addedEpNames = episodes.slice(oldShow.episodes.length).map(ep => ep.name).join(', ');
            addNotification(`✨ تمت إضافة حلقات جديدة للمسلسل "${title}": (${addedEpNames})`);
          } else {
            addNotification(`📝 تم تحديث بيانات العمل: "${title}"`);
          }
          showToast('تم تحديث العمل بنجاح!');
        }
      } else {
        // إضافة عمل جديد كلياً
        const newShow = {
          id: Date.now(),
          category, title, episodes
        };
        shows.unshift(newShow);

        if (category === 'movie') {
          addNotification(`🎬 تم إضافة فيلم جديد: "${title}" استمتع بالمشاهدة الآن!`);
        } else {
          const firstEp = episodes.length > 0 ? ` مع ${episodes.length} حلقات مضافة` : '';
          addNotification(`📺 تم إضافة مسلسل جديد: "${title}"${firstEp}!`);
        }
        showToast('تمت إضافة العمل بنجاح وإرسال إشعار للمستخدمين!');
      }

      localStorage.setItem('mrstoud_shows', JSON.stringify(shows));
      resetAdminForm();
      adminModal.classList.remove('active');
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
      const pass = document.getElementById('adminPassword').value;
      if (pass === "mrstoud2026" || pass === "admin123") {
        isAdminLoggedIn = true;
        localStorage.setItem('mrstoud_verified_owner', 'true');
        loginModal.classList.remove('active');
        document.getElementById('adminPassword').value = '';
        adminModal.classList.add('active');
        showToast('مرحباً بك في لوحة تحكم المالك!');
      } else {
        alert('كلمة المرور غير صحيحة!');
      }
    });

    // تهيئة حالة الإشعارات عند التحميل
    updateNotificationUI();
  </script>
</body>
</html>
