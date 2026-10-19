<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>AI Cinema Studio - اصنع فيلمك بالذكاء الاصطناعي</title>
    <style>
        :root {
            --bg-color: #0f1016;
            --card-bg: #1a1c29;
            --accent-color: #6366f1;
            --accent-hover: #4f46e5;
            --text-color: #ffffff;
            --text-muted: #9ca3af;
            --success-color: #10b981;
            --gold-color: #f59e0b;
            --blue-color: #3b82f6;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
        }

        header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            background: linear-gradient(45deg, #6366f1, #a855f7);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }

        header p {
            color: var(--text-muted);
            font-size: 1.1rem;
        }

        .container {
            background-color: var(--card-bg);
            width: 100%;
            max-width: 800px;
            padding: 30px;
            border-radius: 16px;
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
            border: 1px solid rgba(255, 255, 255, 0.05);
        }

        .form-group {
            margin-bottom: 20px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #d1d5db;
        }

        textarea, input[type="file"], select {
            width: 100%;
            padding: 12px;
            border-radius: 8px;
            border: 1px solid #374151;
            background-color: #111827;
            color: white;
            font-size: 1rem;
        }

        textarea {
            resize: vertical;
            height: 120px;
        }

        textarea:focus, input:focus, select:focus {
            outline: none;
            border-color: var(--accent-color);
        }

        .options-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 15px;
            margin-bottom: 20px;
        }

        /* صندوق ميزة الذكاء الاصطناعي الذاتي للصور */
        .ai-image-box {
            background: rgba(59, 130, 246, 0.08);
            border: 1px solid rgba(59, 130, 246, 0.3);
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 20px;
        }

        .ai-image-title {
            color: var(--blue-color);
            font-size: 1rem;
            font-weight: bold;
            margin-bottom: 8px;
        }

        /* قسم اللمسة البشرية والإخراج */
        .human-touch-box {
            background: rgba(245, 158, 11, 0.05);
            border: 1px solid rgba(245, 158, 11, 0.3);
            border-radius: 10px;
            padding: 18px;
            margin-bottom: 20px;
        }

        .human-touch-title {
            color: var(--gold-color);
            font-size: 1.1rem;
            font-weight: bold;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .checkbox-group {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 12px;
            margin-top: 10px;
        }

        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 8px;
            font-size: 0.9rem;
            color: #d1d5db;
            cursor: pointer;
        }

        .checkbox-item input {
            width: 18px;
            height: 18px;
            accent-color: var(--gold-color);
            cursor: pointer;
        }

        .badge-info {
            font-size: 0.85rem;
            color: var(--success-color);
            margin-top: 5px;
            display: block;
        }

        button {
            width: 100%;
            padding: 14px;
            background: linear-gradient(45deg, var(--accent-color), #8b5cf6);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 1.1rem;
            font-weight: bold;
            cursor: pointer;
            transition: opacity 0.3s;
        }

        button:hover {
            opacity: 0.9;
        }

        /* شاشة التحميل والتقدم */
        #loading-section {
            display: none;
            text-align: center;
            margin-top: 25px;
        }

        .spinner {
            border: 4px solid rgba(255, 255, 255, 0.1);
            width: 50px;
            height: 50px;
            border-radius: 50%;
            border-left-color: var(--accent-color);
            animation: spin 1s linear infinite;
            margin: 0 auto 15px auto;
        }

        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }

        /* نتيجة الفيلم */
        #result-section {
            display: none;
            margin-top: 30px;
            text-align: center;
            background: #111827;
            padding: 20px;
            border-radius: 12px;
            border: 1px solid var(--success-color);
        }

        #result-section h3 {
            color: var(--success-color);
            margin-bottom: 10px;
        }

        .movie-details {
            color: var(--text-muted);
            font-size: 0.95rem;
            margin-bottom: 15px;
        }

        video {
            width: 100%;
            border-radius: 8px;
            max-
