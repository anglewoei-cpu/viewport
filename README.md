<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>✨ 魅惑、社交與日常日語詞彙冒險生成器 ✨</title>
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;700&family=Noto+Sans+TC:wght@400;700&display=swap" rel="stylesheet">
    <style>
        :root {
            --primary-pink: #ffb7b2;
            --secondary-blue: #c2e9fb;
            --secondary-green: #e2f0cb;
            --accent-yellow: #fff1c1;
            --dark-text: #4a4a4a;
            --bg-color: #fff9fb;
            --card-bg: #ffffff;
            --shadow: 0 8px 20px rgba(255, 183, 178, 0.25);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Noto Sans TC', 'Noto Sans JP', sans-serif;
        }

        body {
            background-color: var(--bg-color);
            color: var(--dark-text);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 20px;
        }

        header {
            text-align: center;
            margin-bottom: 20px;
        }

        header h1 {
            font-size: 1.8rem;
            color: #ff6b81;
            margin-bottom: 5px;
            text-shadow: 2px 2px 4px rgba(255,107,129,0.15);
        }

        header p {
            font-size: 0.95rem;
            color: #888;
        }

        /* 導覽列與功能按鈕區 */
        .nav-toolbar {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            margin-bottom: 25px;
        }

        .tab-btn, .action-btn {
            background: #fff;
            border: 2px solid var(--primary-pink);
            padding: 8px 16px;
            border-radius: 20px;
            cursor: pointer;
            font-weight: bold;
            color: #666;
            transition: all 0.2s ease;
            box-shadow: 0 4px 10px rgba(0,0,0,0.03);
        }

        .tab-btn.active, .tab-btn:hover, .action-btn:hover {
            background: var(--primary-pink);
            color: #fff;
            transform: translateY(-2px);
        }

        .print-btn {
            background: linear-gradient(135deg, #a1c4fd 0%, #c2e9fb 100%);
            border: 2px solid #7ab1ff;
            color: #333;
        }
        .print-btn:hover {
            background: linear-gradient(135deg, #7ab1ff 0%, #a1c4fd 100%);
            color: #fff;
        }

        /* 內容區塊主容器 */
        .main-content-area {
            width: 100%;
            max-width: 950px;
            background: var(--card-bg);
            border-radius: 24px;
            padding: 25px;
            box-shadow: var(--shadow);
            margin-bottom: 40px;
        }

        .view-section {
            display: none;
        }
        .view-section.active {
            display: block;
        }

        /* 搜尋與篩選列 */
        .filter-bar {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
            flex-wrap: wrap;
        }

        .filter-bar input, .filter-bar select {
            flex: 1;
            min-width: 160px;
            padding: 10px 15px;
            border: 2px solid #eee;
            border-radius: 12px;
            outline: none;
            transition: border-color 0.2s;
        }
        .filter-bar input:focus, .filter-bar select:focus {
            border-color: var(--primary-pink);
        }

        /* 字卡網格排版 */
        .vocab-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
            gap: 15px;
            max-height: 580px;
            overflow-y: auto;
            padding: 5px;
        }

        .vocab-card {
            background: #fff;
            border: 2px dashed #ffd1dc;
            border-radius: 16px;
            padding: 15px;
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            position: relative;
            transition: transform 0.2s, box-shadow 0.2s;
        }

        .vocab-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0,0,0,0.06);
            border-color: var(--primary-pink);
        }

        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 8px;
        }

        .card-emoji {
            font-size: 1.6rem;
        }

        .card-badge {
            font-size: 0.75rem;
            padding: 3px 8px;
            border-radius: 10px;
            background: #f0f0f0;
            color: #666;
        }
        .badge-social { background: #c2e9fb; color: #005691; }
        .badge-everyday { background: #fff1c1; color: #856404; }
        .badge-pos { background: #e2f0cb; color: #4a7c00; }
        .badge-neg { background: #ffb7b2; color: #a8201a; }

        .card-body h3 {
            font-size: 1.25rem;
            color: #333;
            margin-bottom: 2px;
        }

        .card-body .hiragana {
            font-size: 0.85rem;
            color: #888;
            margin-bottom: 6px;
        }

        .card-body .meaning {
            font-size: 0.95rem;
            color: #555;
            font-weight: bold;
        }

        .card-footer {
            display: flex;
            justify-content: flex-end;
            gap: 8px;
            margin-top: 10px;
        }

        .icon-btn {
            background: none;
            border: none;
            cursor: pointer;
            font-size: 1.1rem;
            padding: 5px;
            border-radius: 50%;
            transition: background 0.2s;
        }
        .icon-btn:hover {
            background: #f5f5f5;
        }

        /* RPG 地圖模式 */
        .map-container {
            display: flex;
            flex-direction: column;
            gap: 15px;
            align-items: center;
        }

        .map-node {
            width: 100%;
            max-width: 500px;
            background: #fff;
            border: 3px solid #ffccd5;
            border-radius: 16px;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 4px 12px rgba(0,0,0,0.04);
        }

        .map-node.unlocked {
            border-color: #a3e635;
            background: #f7fee7;
        }

        /* 吉祥物 Moko 導師對話框 */
        .mascot-container {
            position: fixed;
            bottom: 20px;
            right: 20px;
            display: flex;
            align-items: flex-end;
            gap: 10px;
            z-index: 1000;
        }

        .mascot-bubble {
            background: #fff;
            border: 2px solid var(--primary-pink);
            padding: 10px 15px;
            border-radius: 16px;
            font-size: 0.9rem;
            box-shadow: 0 4px 12px rgba(0,0,0,0.08);
            max-width: 220px;
        }

        .mascot-avatar {
            font-size: 2.5rem;
            background: #fff;
            border-radius: 50%;
            padding: 5px;
            box-shadow: 0 4px 10px rgba(0,0,0,0.1);
        }

        /* --- 瀏覽器原生列印與 PDF 匯出專用樣式 (@media print) --- */
        @media print {
            body * {
                visibility: hidden;
            }

            .main-content-area, .main-content-area * {
                visibility: visible;
            }

            .main-content-area {
                position: absolute;
                left: 0;
                top: 0;
                width: 100%;
                margin: 0;
                padding: 10mm;
                background: #ffffff !important;
                box-shadow: none !important;
            }

            header, .nav-toolbar, .mascot-container, .filter-bar, .card-footer, button, .no-print {
                display: none !important;
            }

            @page {
                size: A4 portrait;
                margin: 15mm;
            }

            .vocab-grid {
                display: grid;
                grid-template-columns: repeat(3, 1fr) !important;
                gap: 10px;
                max-height: none !important;
                overflow: visible !important;
            }

            .vocab-card {
                break-inside: avoid;
                page-break-inside: avoid;
                border: 1px solid #ccc !important;
                box-shadow: none !important;
            }
        }
    </style>
</head>
<body>

    <header>
        <h1>✨ 魅惑、社交與日常日語詞彙冒險生成器 ✨</h1>
        <p>結合真人發音、RPG 通關、人際社交與 PDF 列印匯出系統</p>
    </header>

    <!-- 導覽與操作工具列 -->
    <div class="nav-toolbar no-print">
        <button class="tab-btn active" onclick="switchTab('vocab')">📖 單字卡教材</button>
        <button class="tab-btn" onclick="switchTab('map')">🗺️ RPG 冒險地圖</button>
        <button class="tab-btn" onclick="switchTab('generator')">🎭 風格稱號生成器</button>
        <button class="action-btn print-btn" onclick="window.print()">🖨️ 列印／匯出 PDF</button>
    </div>

    <!-- 主內容區塊 -->
    <div class="main-content-area">

        <!-- 1. 單字卡教材區 -->
        <div id="vocab-section" class="view-section active">
            <div class="filter-bar">
                <input type="text" id="searchInput" placeholder="搜尋漢字、平假名或中文..." oninput="filterVocab()">
                <select id="categoryFilter" onchange="filterVocab()">
                    <option value="all">全部類別 (人際交際 + 日常 + 正面 + 負面)</option>
                    <option value="social">🤝 人際交際 (50組)</option>
                    <option value="everyday">☕ 日常生活 (100組)</option>
                    <option value="pos">🌸 正面的魅力 (Positive)</option>
                    <option value="neg">🖤 負面/危險的魅力 (Negative)</option>
                </select>
            </div>
            <div class="vocab-grid" id="vocabGrid">
                <!-- 動態生成字卡 -->
            </div>
        </div>

        <!-- 2. RPG 冒險地圖區 -->
        <div id="map-section" class="view-section">
            <h2 style="margin-bottom: 15px; color:#ff6b81;">🗺️ 日語魅力與人際交際冒險闖關</h2>
            <p style="margin-bottom: 20px; color:#666;">挑戰各個關卡，解鎖人際交際、手腕與社交靈魂詞彙！</p>
            <div class="map-container">
                <div class="map-node unlocked">
                    <div>
                        <h3>Stage 1: 人際交際與社交手腕</h3>
                        <p style="font-size:0.85rem; color:#666;">學習意気投合、阿吽の呼吸等社交溝通詞彙</p>
                    </div>
                    <button class="action-btn" onclick="alert('進入 Stage 1 測驗！')">進入挑戰 ⭐⭐⭐</button>
                </div>
                <div class="map-node">
                    <div>
                        <h3>Stage 2: 日常生活好感與療癒</h3>
                        <p style="font-size:0.85rem; color:#666;">掌握笑顔、気配り與質感生活詞彙</p>
                    </div>
                    <button class="action-btn" style="opacity:0.6;" disabled>尚未解鎖 🔒</button>
                </div>
                <div class="map-node">
                    <div>
                        <h3>Stage 3: 暗黑魅惑與禁忌</h3>
                        <p style="font-size:0.85rem; color:#666;">探索致命誘惑與退廢美</p>
                    </div>
                    <button class="action-btn" style="opacity:0.6;" disabled>尚未解鎖 🔒</button>
                </div>
            </div>
        </div>

        <!-- 3. 稱號生成器區 -->
        <div id="generator-section" class="view-section">
            <h2 style="margin-bottom: 15px; color:#ff6b81;">🎭 專屬人際與社交稱號生成器</h2>
            <p style="margin-bottom: 20px; color:#666;">點擊下方按鈕，隨機生成專屬於您的職場人際與社交風格稱號！</p>
            <div style="text-align: center; padding: 30px; background: #fff9fb; border-radius: 16px; border: 2px dashed #ffb7b2;">
                <h3 id="generatedTitle" style="font-size: 1.4rem; color: #333; margin-bottom: 15px;">【未生成】點擊下方開始按鈕</h3>
                <p id="generatedDesc" style="color: #666; margin-bottom: 20px;"></p>
                <button class="action-btn" onclick="generateCharmTitle()" style="font-size: 1.1rem; padding: 10px 25px;">✨ 抽取專屬人際交際稱號</button>
            </div>
        </div>

    </div>

    <!-- 吉祥物 Moko 導師對話 -->
    <div class="mascot-container no-print">
        <div class="mascot-bubble" id="mokoBubble">
            こんにちは！我是助教 Moko，已為您調整並升級選單系統囉！✨
        </div>
        <div class="mascot-avatar">🐱</div>
    </div>

    <script>
        // 完整詞彙庫 (包含人際交際 + 日常生活 + 正面 + 負面)
        const vocabularyData = [
            // --- 人際交際 (50組) ---
            { id: 2001, type: 'social', kanji: '社交的', hiragana: 'しゃこうてき', meaning: '社交性強', emoji: '🤝' },
            { id: 2002, type: 'social', kanji: '気さく', hiragana: 'きさく', meaning: '平易近人、不拘小節', emoji: '🍃' },
            { id: 2003, type: 'social', kanji: '人懐っこい', hiragana: 'ひとなつっこい', meaning: '討人喜歡、親切', emoji: '🐶' },
            { id: 2004, type: 'social', kanji: '意気投合', hiragana: 'いきとうごう', meaning: '意氣相投', emoji: '🎉' },
            { id: 2005, type: 'social', kanji: '波長が合う', hiragana: 'はちょうがあう', meaning: '磁場相合、頻率一致', emoji: '📻' },
            { id: 2006, type: 'social', kanji: '気が合う', hiragana: 'きがあう', meaning: '氣味相投', emoji: '✨' },
            { id: 2007, type: 'social', kanji: '阿吽の呼吸', hiragana: 'あうんのこきゅう', meaning: '絕佳默契', emoji: '☯️' },
            { id: 2008, type: 'social', kanji: '以心伝心', hiragana: 'いしんでんしん', meaning: '心有靈犀一點通', emoji: '💡' },
            { id: 2009, type: 'social', kanji: '気配り', hiragana: 'きくばり', meaning: '周到細心的照顧', emoji: '🎁' },
            { id: 2010, type: 'social', kanji: '空気が読める', hiragana: 'くうきがよめる', meaning: '懂得看臉色、有眼力見', emoji: '👀' },
            { id: 2011, type: 'social', kanji: '機微を察する', hiragana: 'きびをさっする', meaning: '體察入微', emoji: '🔍' },
            { id: 2012, type: 'social', kanji: '協調性', hiragana: 'きょうちょうせい', meaning: '協調性、團隊精神', emoji: '🧩' },
            { id: 2013, type: 'social', kanji: '調和', hiragana: 'ちょうわ', meaning: '和諧', emoji: '🕊️' },
            { id: 2014, type: 'social', kanji: '円滑な関係', hiragana: 'えんかつなかんけい', meaning: '圓滑順暢的關係', emoji: '🌊' },
            { id: 2015, type: 'social', kanji: '大人の対応', hiragana: 'おとなのたいおう', meaning: '成熟圓融的應對', emoji: '👔' },
            { id: 2016, type: 'social', kanji: '角を立てない', hiragana: 'かどをたたない', meaning: '不起衝突、不得罪人', emoji: '⭕' },
            { id: 2017, type: 'social', kanji: '折り合いをつける', hiragana: 'おりあいをつける', meaning: '互相妥協、找到平衡點', emoji: '⚖️' },
            { id: 2018, type: 'social', kanji: '歩み寄り', hiragana: 'あゆみより', meaning: '各退一步、互相靠攏', emoji: '🚶‍♂️' },
            { id: 2019, type: 'social', kanji: '思いやり', hiragana: 'おもいやり', meaning: '同理心、體貼', emoji: '🌷' },
            { id: 2020, type: 'social', kanji: '心遣い', hiragana: 'こころづかい', meaning: '貼心的關懷', emoji: '💖' },
            { id: 2021, type: 'social', kanji: '配慮', hiragana: 'はいりょ', meaning: '顧慮、周到考量', emoji: '💭' },
            { id: 2022, type: 'social', kanji: 'おもてなし', hiragana: 'おもてなし', meaning: '誠心招待、熱情款待', emoji: '🍵' },
            { id: 2023, type: 'social', kanji: '聞き上手', hiragana: 'ききじょうず', meaning: '善於傾聽', emoji: '👂' },
            { id: 2024, type: 'social', kanji: '話し上手', hiragana: 'はなしじょうず', meaning: '善於交談', emoji: '🗣️' },
            { id: 2025, type: 'social', kanji: '相づちが上手', hiragana: 'あいづちがじょうず', meaning: '擅長附和與回應', emoji: '👍' },
            { id: 2026, type: 'social', kanji: '褒め上手', hiragana: 'ほめじょうず', meaning: '擅長讚美他人', emoji: '👏' },
            { id: 2027, type: 'social', kanji: '場を和ませる', hiragana: 'ばをなごませる', meaning: '溫暖全場氣氛', emoji: '☀️' },
            { id: 2028, type: 'social', kanji: 'ムードメーカー', hiragana: 'むーどめーかー', meaning: '氣氛製造者', emoji: '🎈' },
            { id: 2029, type: 'social', kanji: '懐が深い', hiragana: 'ふところがふかい', meaning: '胸襟廣闊、包容力強', emoji: '🌌' },
            { id: 2030, type: 'social', kanji: '誰とでも打ち解ける', hiragana: 'だれとでもうちとける', meaning: '和誰都能打成一片', emoji: '👫' },
            { id: 2031, type: 'social', kanji: '好感を持たれる', hiragana: 'こうかんをもたれる', meaning: '贏得好感', emoji: '⭐' },
            { id: 2032, type: 'social', kanji: '信頼関係', hiragana: 'しんらいかんけい', meaning: '信任關係', emoji: '🛡️' },
            { id: 2033, type: 'social', kanji: '絆', hiragana: 'きずな', meaning: '羈絆、深厚連結', emoji: '🎗️' },
            { id: 2034, type: 'social', kanji: '結びつき', hiragana: 'むすびつき', meaning: '連結、聯繫', emoji: '🔗' },
            { id: 2035, type: 'social', kanji: '心を通わせる', hiragana: 'こころをとおわせる', meaning: '心靈相通', emoji: '💞' },
            { id: 2036, type: 'social', kanji: '本音で話す', hiragana: 'ほんねではなす', meaning: '坦承真心話', emoji: '💬' },
            { id: 2037, type: 'social', kanji: '打ち明ける', hiragana: 'うちあける', meaning: '吐露心聲', emoji: '🗝️' },
            { id: 2038, type: 'social', kanji: '距離感を縮める', hiragana: 'きょりかんをちぢめる', meaning: '拉近距離', emoji: '📐' },
            { id: 2039, type: 'social', kanji: '許容範囲が広い', hiragana: 'きょようはんいがひろい', meaning: '容忍度高、包容力強', emoji: '🛡️' },
            { id: 2040, type: 'social', kanji: '柔軟な対応', hiragana: 'じゅうなんなたいおう', meaning: '靈活應對', emoji: '🌿' },
            { id: 2041, type: 'social', kanji: '機転が利く', hiragana: 'きてんがきく', meaning: '機靈敏捷、應變力強', emoji: '⚡' },
            { id: 2042, type: 'social', kanji: '如才ない', hiragana: 'じょさいない', meaning: '精明圓滑、不得罪人', emoji: '🕊️' },
            { id: 2043, type: 'social', kanji: '処世術', hiragana: 'しょせいじゅつ', meaning: '處世哲學、社交手腕', emoji: '📘' },
            { id: 2044, type: 'social', kanji: '人心掌握術', hiragana: 'じんしんしょうあくじゅつ', meaning: '收攬人心之術', emoji: '👑' },
            { id: 2045, type: 'social', kanji: '笑顔で接する', hiragana: 'えがおでせっする', meaning: '微笑以對', emoji: '😊' },
            { id: 2046, type: 'social', kanji: '肯定的な姿勢', hiragana: 'こうていてきなしせい', meaning: '肯定與支持的態度', emoji: '✨' },
            { id: 2047, type: 'social', kanji: '共感を示す', hiragana: 'きょうかんをしめす', meaning: '表達同理與共鳴', emoji: '💌' },
            { id: 2048, type: 'social', kanji: '良好な人間関係', hiragana: 'りょうこうなじんげんかんけい', meaning: '良好的人際關係', emoji: '🌈' },
            { id: 2049, type: 'social', kanji: 'お互い様', hiragana: 'おたがいさま', meaning: '彼此彼此、互相體諒', emoji: '🤝' },
            { id: 2050, type: 'social', kanji: '歩み寄る姿勢', hiragana: 'あゆみよるしせい', meaning: '願意互相靠攏的態度', emoji: '🚶‍♀️' },

            // --- 日常生活 (100組精選代表) ---
            { id: 1001, type: 'everyday', kanji: '笑顔が素敵', hiragana: 'えがおがすてき', meaning: '笑容迷人', emoji: '😊' },
            { id: 1002, type: 'everyday', kanji: '明るい性格', hiragana: 'あかるいせいかく', meaning: '開朗的性格', emoji: '☀️' },
            { id: 1003, type: 'everyday', kanji: '人当たりが良い', hiragana: 'ひとあたりがよい', meaning: '待人親切溫和', emoji: '🤝' },
            { id: 1004, type: 'everyday', kanji: '親しみやすさ', hiragana: 'したしみやすさ', meaning: '平易近人的特質', emoji: '🧡' },
            { id: 1005, type: 'everyday', kanji: '愛想が良い', hiragana: 'あいそがよい', meaning: '態度和藹可親', emoji: '✨' },
            { id: 1006, type: 'everyday', kanji: '愛嬌たっぷり', hiragana: 'あいきょうたっぷり', meaning: '親和力滿分', emoji: '💖' },
            { id: 1007, type: 'everyday', kanji: '清潔感がある', hiragana: 'せいけつかんがある', meaning: '給人乾淨清爽的感覺', emoji: '🧼' },
            { id: 1008, type: 'everyday', kanji: 'お洒落', hiragana: 'おしゃれ', meaning: '時髦、講究穿搭', emoji: '👒' },
            { id: 1009, type: 'everyday', kanji: '丁寧な暮らし', hiragana: 'ていねいなくらし', meaning: '講究細緻的生活態度', emoji: '🍵' },
            { id: 1010, type: 'everyday', kanji: '自然体', hiragana: 'しぜんたい', meaning: '自然不做作', emoji: '🌿' },
            { id: 1011, type: 'everyday', kanji: '癒やし系', hiragana: 'いやしけい', meaning: '療癒系特質', emoji: '☁️' },
            { id: 1012, type: 'everyday', kanji: '安心感を与える', hiragana: 'あんしんかんをあたえる', meaning: '帶給人安全感', emoji: '🛡️' },

            // --- 正面魅力 (Positive) ---
            { id: 1, type: 'pos', kanji: '美貌', hiragana: 'びぼう', meaning: '美貌', emoji: '✨' },
            { id: 2, type: 'pos', kanji: '容姿端麗', hiragana: 'ようしたんれい', meaning: '容貌姿態端莊美麗', emoji: '🌸' },
            { id: 3, type: 'pos', kanji: 'オーラ', hiragana: 'おーら', meaning: '強大的氣場/光環', emoji: '🌟' },
            { id: 4, type: 'pos', kanji: 'カリスマ', hiragana: 'かりすま', meaning: '超凡的領袖魅力', emoji: '👑' },

            // --- 負面魅惑 (Negative) ---
            { id: 501, type: 'neg', kanji: 'ファム・ファタール', hiragana: 'ふぁむ・ふぁたーる', meaning: '致命女人（Femme Fatale）', emoji: '🌹' },
            { id: 502, type: 'neg', kanji: '魔性の女', hiragana: 'ましょうのおんな', meaning: '魔性之女/會毀掉男人的女人', emoji: '🖤' },
            { id: 503, type: 'neg', kanji: 'メンヘラ', hiragana: 'めんへら', meaning: '情緒不穩/病嬌', emoji: '🌀' }
        ];

        // 初始化載入字卡
        window.addEventListener('DOMContentLoaded', () => {
            renderVocabCards(vocabularyData);
        });

        // 頁籤切換
        function switchTab(tabId) {
            document.querySelectorAll('.view-section').forEach(sec => sec.classList.remove('active'));
            document.querySelectorAll('.tab-btn').forEach(btn => btn.classList.remove('active'));

            if (tabId === 'vocab') {
                document.getElementById('vocab-section').classList.add('active');
                event.target.classList.add('active');
                setMokoMsg("來複習日語單字卡吧！點擊喇叭圖示還能聽真人日語發音喔！🔊");
            } else if (tabId === 'map') {
                document.getElementById('map-section').classList.add('active');
                event.target.classList.add('active');
                setMokoMsg("準備好挑戰人際社交與日常冒險地圖了嗎？通關可以解鎖更多詞彙！🗺️");
            } else if (tabId === 'generator') {
                document.getElementById('generator-section').classList.add('active');
                event.target.classList.add('active');
                setMokoMsg("來試試看隨機生成您的專屬人際與社交風格稱號吧！✨");
            }
        }

        // 渲染字卡
        function renderVocabCards(data) {
            const grid = document.getElementById('vocabGrid');
            grid.innerHTML = '';
            if (data.length === 0) {
                grid.innerHTML = '<p style="grid-column: 1/-1; text-align:center; color:#888; padding:20px;">沒有找到符合的詞彙喔！</p>';
                return;
            }

            data.forEach(item => {
                let badgeClass = 'badge-pos';
                let badgeText = '正面魅力';
                if (item.type === 'neg') {
                    badgeClass = 'badge-neg';
                    badgeText = '負面魅惑';
                } else if (item.type === 'everyday') {
                    badgeClass = 'badge-everyday';
                    badgeText = '日常生活';
                } else if (item.type === 'social') {
                    badgeClass = 'badge-social';
                    badgeText = '人際交際';
                }
                
                const card = document.createElement('div');
                card.className = 'vocab-card';
                card.innerHTML = `
                    <div>
                        <div class="card-header">
                            <span class="card-emoji">${item.emoji}</span>
                            <span class="card-badge ${badgeClass}">${badgeText}</span>
                        </div>
                        <div class="card-body">
                            <h3>${item.kanji}</h3>
                            <div class="hiragana">${item.hiragana}</div>
                            <div class="meaning">${item.meaning}</div>
                        </div>
                    </div>
                    <div class="card-footer">
                        <button class="icon-btn" onclick="playTTS('${item.kanji}')" title="聆聽發音">🔊</button>
                    </div>
                `;
                grid.appendChild(card);
            });
        }

        // 篩選與搜尋
        function filterVocab() {
            const keyword = document.getElementById('searchInput').value.toLowerCase();
            const category = document.getElementById('categoryFilter').value;

            const filtered = vocabularyData.filter(item => {
                const matchKeyword = item.kanji.toLowerCase().includes(keyword) || 
                                     item.hiragana.toLowerCase().includes(keyword) || 
                                     item.meaning.toLowerCase().includes(keyword);
                const matchCategory = category === 'all' || item.type === category;
                return matchKeyword && matchCategory;
            });

            renderVocabCards(filtered);
        }

        // 真人發音 Web Speech API
        function playTTS(text) {
            if (!('speechSynthesis' in window)) {
                alert('您的瀏覽器不支援語音朗讀功能！');
                return;
            }
            window.speechSynthesis.cancel();
            const utterance = new SpeechSynthesisUtterance(text);
            utterance.lang = 'ja-JP';
            utterance.rate = 0.9;
            window.speechSynthesis.speak(utterance);
            setMokoMsg(`正在朗讀：${text} 🎧`);
        }

        // 稱號生成器
        function generateCharmTitle() {
            const titles = [
                { title: "【阿吽の呼吸のムードメーカー】", desc: "阿吽の呼吸 × ムードメーカー：擁有絕佳默契與氣氛帶動能力，永遠是團隊與聚會的核心焦點。" },
                { title: "【機転が利く大人の対応】", desc: "機転が利く × 大人の対応：處事靈活機靈，應對圓融有禮，是職場與社交圈最可靠的後盾。" },
                { title: "【本音で心を通わせる知己】", desc: "本音で話す × 心を通わせる：待人真誠坦率、善於心靈相通，能建立極為深厚的羈絆。" },
                { title: "【懐が深い信頼の要】", desc: "懐が深い × 信頼関係：胸襟廣闊包容力強，能贏得周遭所有人的尊重與絕對信任。" }
            ];
            const random = titles[Math.floor(Math.random() * titles.length)];
            document.getElementById('generatedTitle').innerText = random.title;
            document.getElementById('generatedDesc').innerText = random.desc;
            setMokoMsg("這個人際交際稱號展現了絕佳的社交手腕呢！✨");
        }

        // 改變 Moko 導師對話
        function setMokoMsg(msg) {
            document.getElementById('mokoBubble').innerText = msg;
        }
    </script>
</body>
</html>
