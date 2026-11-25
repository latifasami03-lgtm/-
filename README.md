# -<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
  <title>من هدف إلى إنجاز</title>
  <link rel="preconnect" href="https://googleapis.com">
  <link rel="preconnect" href="https://gstatic.com" crossorigin>
  <link href="https://googleapis.com/css2?family=Tajawal:wght@500;700;800&display=swap" rel="stylesheet">
  <style>
    :root {
      --bg-offwhite: #FAF8F5;
      --card-white: #FFFFFF;
      --blue-light: #E6F2FA;
      --blue-soft: #B8DCF2;
      --blue-primary: #3B8AC4;
      --blue-dark: #235B85;
      --text-main: #1E3A52;
      --text-muted: #5A768E;
      --success-bg: #E3F6EC;
      --success-border: #34A853;
      --error-bg: #FDECEA;
      --error-border: #EA4335;
      --shadow: 0 6px 18px rgba(35, 91, 133, 0.08);
    }

    * {
      box-sizing: border-box;
      -webkit-tap-highlight-color: transparent;
      user-select: none;
    }

    body {
      margin: 0;
      padding: 0;
      font-family: 'Tajawal', sans-serif;
      background-color: var(--bg-offwhite);
      color: var(--text-main);
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
    }

    .game-container {
      width: 94%;
      max-width: 960px;
      background: var(--card-white);
      border-radius: 28px;
      padding: 28px 32px;
      box-shadow: var(--shadow);
      border: 2px solid var(--blue-light);
      margin: 16px auto;
    }

    header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 2px solid var(--blue-light);
      padding-bottom: 16px;
      margin-bottom: 22px;
      flex-wrap: wrap;
      gap: 12px;
    }

    .title-group h1 {
      margin: 0;
      font-size: 1.9rem;
      color: var(--blue-dark);
      font-weight: 800;
    }

    .title-group p {
      margin: 4px 0 0;
      font-size: 1rem;
      color: var(--text-muted);
    }

    .stats {
      display: flex;
      gap: 12px;
      align-items: center;
    }

    .badge {
      background: var(--blue-light);
      color: var(--blue-dark);
      padding: 8px 18px;
      border-radius: 50px;
      font-weight: 700;
      font-size: 1.05rem;
    }

    .goal-box {
      background: linear-gradient(135deg, var(--blue-light) 0%, #D4EAF8 100%);
      border-right: 6px solid var(--blue-primary);
      border-radius: 18px;
      padding: 18px 24px;
      margin-bottom: 24px;
      text-align: center;
    }

    .goal-label {
      display: inline-block;
      background: var(--blue-primary);
      color: #fff;
      font-size: 0.9rem;
      font-weight: 700;
      padding: 4px 14px;
      border-radius: 20px;
      margin-bottom: 8px;
    }

    .goal-text {
      margin: 0;
      font-size: 1.55rem;
      font-weight: 800;
      color: var(--blue-dark);
    }

    .section-title {
      font-size: 1.1rem;
      font-weight: 700;
      color: var(--text-muted);
      margin-bottom: 12px;
    }

    /* منطقة البطاقات المبعثرة */
    .cards-pool {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 14px;
      min-height: 115px;
      background: var(--bg-offwhite);
      padding: 14px;
      border-radius: 20px;
      border: 2px dashed var(--blue-soft);
      margin-bottom: 26px;
    }

    /* خانات الترتيب من 1 إلى 4 */
    .slots-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 14px;
      margin-bottom: 24px;
    }

    .slot {
      background: var(--bg-offwhite);
      border: 2.5px dashed var(--blue-primary);
      border-radius: 20px;
      min-height: 145px;
      padding: 12px;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: flex-start;
      transition: all 0.2s ease;
      position: relative;
    }

    .slot.drag-over {
      background: var(--blue-light);
      transform: scale(1.02);
    }

    .slot.correct {
      background: var(--success-bg);
      border-color: var(--success-border);
      border-style: solid;
    }

    .slot.wrong {
      background: var(--error-bg);
      border-color: var(--error-border);
      border-style: solid;
    }

    .slot-header {
      background: var(--blue-light);
      color: var(--blue-dark);
      font-weight: 800;
      font-size: 0.95rem;
      padding: 4px 14px;
      border-radius: 12px;
      margin-bottom: 10px;
      width: 100%;
      text-align: center;
    }

    .slot-body {
      width: 100%;
      flex: 1;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    /* البطاقة القابلة للسحب */
    .step-card {
      background: var(--card-white);
      border: 2px solid var(--blue-soft);
      border-radius: 16px;
      padding: 14px 12px;
      width: 100%;
      min-height: 85px;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      font-size: 1.1rem;
      font-weight: 700;
      color: var(--text-main);
      box-shadow: 0 4px 10px rgba(35, 91, 133, 0.08);
      cursor: grab;
      touch-action: none;
      transition: transform 0.15s ease, box-shadow 0.15s ease, border-color 0.15s ease;
    }

    .step-card:active {
      cursor: grabbing;
    }

    .step-card.selected {
      border: 3px solid var(--blue-primary);
      background: var(--blue-light);
      transform: translateY(-3px);
    }

    .dragging-clone {
      position: fixed;
      z-index: 9999;
      pointer-events: none;
      opacity: 0.92;
      transform: scale(1.05);
      box-shadow: 0 12px 28px rgba(35, 91, 133, 0.22);
    }

    /* الرسالة والأزرار */
    .feedback {
      text-align: center;
      font-size: 1.2rem;
      font-weight: 800;
      min-height: 32px;
      margin-bottom: 18px;
      color: var(--blue-dark);
    }

    .controls {
      display: flex;
      justify-content: center;
      gap: 16px;
      flex-wrap: wrap;
    }

    button {
      font-family: 'Tajawal', sans-serif;
      font-size: 1.2rem;
      font-weight: 800;
      padding: 14px 36px;
      border-radius: 16px;
      border: none;
      cursor: pointer;
      transition: all 0.2s ease;
      min-width: 170px;
    }

    .btn-check {
      background: var(--blue-primary);
      color: #fff;
      box-shadow: 0 4px 12px rgba(59, 138, 196, 0.3);
    }

    .btn-check:hover {
      background: var(--blue-dark);
    }

    .btn-next {
      background: var(--blue-light);
      color: var(--blue-dark);
      border: 2px solid var(--blue-primary);
      display: none;
    }

    .btn-next:hover {
      background: var(--blue-soft);
    }

    .btn-reset {
      background: transparent;
      color: var(--text-muted);
      border: 2px solid var(--blue-soft);
      min-width: 130px;
    }

    /* التجاوب مع وضع الآيباد الطولي */
    @media (max-width: 820px) {
      .cards-pool, .slots-grid {
        grid-template-columns: repeat(2, 1fr);
      }
      .goal-text {
        font-size: 1.35rem;
      }
    }
  </style>
</head>
<body>

<div class="game-container">
  <header>
    <div class="title-group">
      <h1>من هدف إلى إنجاز 🎯</h1>
      <p>اسحب البطاقات ورتّب خطوات تحقيق الهدف من الأولى إلى الرابعة</p>
    </div>
    <div class="stats">
      <div class="badge" id="progressBadge">الهدف 1 من 5</div>
      <div class="badge" id="scoreBadge">النقاط: 0</div>
    </div>
  </header>

  <div class="goal-box">
    <span class="goal-label">الهدف المطلوب</span>
    <h2 class="goal-text" id="goalTitle">...</h2>
  </div>

  <div class="section-title">الخطوات المبعثرة (اسحب البطاقة أو انقر عليها ثم اختر الخانة):</div>
  <div class="cards-pool" id="cardsPool"></div>

  <div class="section-title">رتّب الخطوات بالترتيب الصحيح:</div>
  <div class="slots-grid" id="slotsGrid">
    <div class="slot" data-slot="0">
      <div class="slot-header">الخطوة الأولى</div>
      <div class="slot-body"></div>
    </div>
    <div class="slot" data-slot="1">
      <div class="slot-header">الخطوة الثانية</div>
      <div class="slot-body"></div>
    </div>
    <div class="slot" data-slot="2">
      <div class="slot-header">الخطوة الثالثة</div>
      <div class="slot-body"></div>
    </div>
    <div class="slot" data-slot="3">
      <div class="slot-header">الخطوة الرابعة</div>
      <div class="slot-body"></div>
    </div>
  </div>

  <div class="feedback" id="feedbackMsg"></div>

  <div class="controls">
    <button class="btn-check" id="checkBtn">تحقّق</button>
    <button class="btn-next" id="nextBtn">الهدف التالي ⬅</button>
    <button class="btn-reset" id="resetBtn">إعادة الترتيب</button>
  </div>
</div>

<script>
  const goalsData = [
    {
      goal: "زراعة نبتة في حديقة المنزل",
      steps: [
        "تجهيز الأصيص وملؤه بالتربة المناسبة",
        "وضع البذور في التربة وتغطيتها برفق",
        "سقي التربة بكمية معتدلة من الماء",
        "وضع الأصيص في مكان تصله أشعة الشمس"
      ]
    },
    {
      goal: "الاستعداد لاختبار نهاية الفصل بنجاح",
      steps: [
        "حصر الدروس المطلوبة وتقسيمها على الأيام",
        "مذاكرة الدروس وتلخيص الأفكار الرئيسية",
        "حل نماذج أسئلة وتدريبات سابقة",
        "النوم مبكرًا ليلة الاختبار للتركيز"
      ]
    },
    {
      goal: "إعداد عرض تقديمي متميز أمام الفصل",
      steps: [
        "اختيار موضوع العرض وتحديد أهدافه",
        "جمع المعلومات الموثوقة وتنظيمها",
        "تصميم الشرائح وإضافة الصور التوضيحية",
        "التدرب على الإلقاء وضبط الوقت"
      ]
    },
    {
      goal: "كتابة قصة قصيرة مشوّقة",
      steps: [
        "تحديد الفكرة والشخصيات والزمان والمكان",
        "كتابة بداية القصة وتصاعد الأحداث",
        "الوصول إلى ذروة المشكلة ثم حلّها",
        "مراجعة القصة وتصحيح الأخطاء الإملائية"
      ]
    },
    {
      goal: "الادخار لشراء دراجة جديدة",
      steps: [
        "معرفة سعر الدراجة وتحديد المبلغ المطلوب",
        "تخصيص حصالة وتحديد مبلغ ادخار أسبوعي",
