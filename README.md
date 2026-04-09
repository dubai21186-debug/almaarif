<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>لعبة الصقر 2 | مدرسة المعارف</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none;
        }

        body {
            min-height: 100vh;
            background: linear-gradient(145deg, #1e3c2c 0%, #2a4a35 100%);
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: 'Segoe UI', 'Tahoma', 'Cairo', 'Amiri', serif;
            padding: 20px;
        }

        /* الحاوية الرئيسية */
        .game-container {
            width: 100%;
            max-width: 850px;
            background: #fdf8e7;
            background-image: radial-gradient(circle at 10% 20%, rgba(210, 180, 140, 0.1) 2%, transparent 2.5%);
            background-size: 25px 25px;
            border-radius: 65px 45px 80px 50px;
            box-shadow: 25px 30px 40px rgba(0,0,0,0.4), inset 1px 1px 4px rgba(255,255,200,0.8);
            overflow: hidden;
            transition: all 0.2s;
        }

        /* الرأس: المدرسة والمعلم */
        .school-header {
            background: #8b5a2b;
            background: linear-gradient(135deg, #9b6a3a, #6e3e1a);
            padding: 14px 20px;
            color: #ffefcf;
            display: flex;
            justify-content: space-between;
            align-items: baseline;
            flex-wrap: wrap;
            border-bottom: 5px solid #e6c87a;
            text-shadow: 2px 2px 0 #4a2a10;
        }
        .school-name {
            font-size: 1.4rem;
            font-weight: bold;
            letter-spacing: 1px;
        }
        .teacher-name {
            font-size: 1.1rem;
            background: #2c221b;
            padding: 5px 14px;
            border-radius: 40px;
            font-family: monospace;
        }

        /* منطقة السؤال */
        .question-area {
            padding: 25px 25px 15px;
            background: #fffaf0;
            border-bottom: 2px dashed #d4b88c;
        }
        .question-text {
            font-size: 1.6rem;
            font-weight: bold;
            color: #3b2a1f;
            line-height: 1.4;
            background: #fef3db;
            padding: 18px;
            border-radius: 50px 20px 50px 20px;
            box-shadow: inset 0 0 0 2px white, 0 8px 12px rgba(0,0,0,0.05);
        }

        /* خيارات الإجابة */
        .options-area {
            padding: 20px 25px 30px;
        }
        .option-btn {
            display: block;
            width: 100%;
            background: #e9e0cf;
            border: 2px solid #bb9e6b;
            border-radius: 60px;
            padding: 14px 20px;
            margin-bottom: 14px;
            font-size: 1.2rem;
            font-family: inherit;
            font-weight: bold;
            color: #2d2b20;
            text-align: right;
            cursor: pointer;
            transition: 0.1s linear;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        .option-btn:hover {
            background: #ecd9b4;
            transform: scale(0.99);
            border-color: #a57c3e;
        }
        .option-btn.disabled-btn, .option-btn:active {
            pointer-events: none;
            opacity: 0.7;
        }

        /* تذييل السؤال */
        .question-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 25px 20px;
            font-weight: bold;
            color: #5c3f1a;
        }
        .counter {
            background: #d9c294;
            padding: 6px 18px;
            border-radius: 40px;
            font-size: 1.2rem;
        }
        .next-btn {
            background: #3c7a3e;
            border: none;
            padding: 10px 28px;
            font-size: 1.2rem;
            font-weight: bold;
            color: white;
            border-radius: 40px;
            cursor: pointer;
            transition: 0.1s;
            font-family: inherit;
            box-shadow: 0 4px 6px black;
        }
        .next-btn:active {
            transform: scale(0.96);
        }
        .next-btn.hidden {
            display: none;
        }

        /* لوحة النتيجة النهائية */
        .result-panel {
            background: #2e4e35e6;
            backdrop-filter: blur(8px);
            text-align: center;
            padding: 35px 20px;
            border-top: 6px solid gold;
        }
        .score-display {
            font-size: 3rem;
            font-weight: bold;
            background: #fbe9c3;
            display: inline-block;
            padding: 15px 35px;
            border-radius: 90px;
            margin: 15px 0;
        }
        .emoji-big {
            font-size: 4rem;
        }
        .restart-btn {
            background: #ffbb77;
            border: none;
            padding: 12px 30px;
            font-size: 1.3rem;
            margin-top: 25px;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
        }

        .feedback {
            text-align: center;
            margin-top: 8px;
            font-size: 1.2rem;
        }
        .hide {
            display: none;
        }
        button:active {
            transform: scale(0.96);
        }
        @media (max-width: 550px) {
            .question-text { font-size: 1.2rem; }
            .option-btn { font-size: 0.9rem; }
        }
    </style>
</head>
<body>
<div class="game-container" id="gameContainer">
    <div class="school-header">
        <span class="school-name">🏫 مدرسة المعارف - الحلقة الثالثة</span>
        <span class="teacher-name">📖 الأستاذ: محمود الرياطي</span>
    </div>
    <div id="dynamicContent">
        <!-- المحتوى سيتم حقنه بواسطة js -->
    </div>
</div>

<script>
    // ========== الأسئلة المأخوذة من رواية "الصقر 2" ==========
    const questions = [
        { text: "في أي عام وقعت أحداث البداية في واحة العين (سبتمبر) ؟", type: "choice", options: ["1945", "1948", "1950", "1952"], correct: "1948" },
        { text: "ما اسم القصر القديم الذي ورد في النص؟", type: "choice", options: ["قصر الحصن", "قصر المويجعي", "قلعة الجاهلي", "حصن الفهيدي"], correct: "قصر المويجعي" },
        { text: "من هو المغامر الإنجليزي الذي تحدى صحراء الصحاري؟", type: "choice", options: ["توماس إدوارد", "ولفريد ثيسيغر", "جون فيلبي", "ويليام شكسبير"], correct: "ولفريد ثيسيغر" },
        { text: "الشيخ شخبوط كان يولي أهمية أكبر للماء أم للنفط؟", type: "tf", options: ["للماء", "للنفط"], correct: "للماء" },
        { text: "ماذا طلب الشيخ شخبوط من الجيولوجيين البريطانيين عندما أخبروه عن النفط؟", type: "choice", options: ["أعطوني بئر نفط", "ماء، حدوا لي الماء", "أريد خط أنابيب بترول", "لا أريد شيئاً"], correct: "ماء، حدوا لي الماء" },
        { text: "ما اسم المعاهدة التي أنهت القرصنة في الساحل وأصبح اسمه 'الساحل المتصالح'؟", type: "choice", options: ["معاهدة الصداقة", "معاهدة السلم الدائم", "اتفاقية السلام البحري", "عهد حماية السواحل"], correct: "معاهدة السلم الدائم" },
        { text: "حسب النص، الشيخ زايد قال عن العنف أنه مناقض لتعاليم الإسلام.", type: "tf", options: ["صحيح", "خطأ"], correct: "صحيح" },
        { text: "كم سنة كانت مدة امتياز التنقيب عن النفط الذي منحته شركة PDTC؟", type: "choice", options: ["50 سنة", "75 سنة", "100 سنة", "25 سنة"], correct: "75 سنة" },
        { text: "في حوار الشيخ زايد، قال: 'المدروب' قد يكون موجوداً بيننا، والمدروب هو:", type: "choice", options: ["الغريب", "الجاسوس", "الخارج على القانون", "التاجر"], correct: "الخارج على القانون" },
        { text: "مولود الشيخ زايد الجديد وُلد في أي يوم (حسب النص)؟", type: "choice", options: ["7 سبتمبر", "15 أغسطس", "1 أكتوبر", "14 يناير"], correct: "7 سبتمبر" }
    ];

    // أصوات بسيطة باستخدام Web Audio API (نغمات قصيرة)
    function playSound(type) {
        try {
            const audioCtx = new (window.AudioContext || window.webkitAudioContext)();
            const oscillator = audioCtx.createOscillator();
            const gainNode = audioCtx.createGain();
            oscillator.connect(gainNode);
            gainNode.connect(audioCtx.destination);
            oscillator.type = "sine";
            let frequency = type === "correct" ? 880 : 440;
            oscillator.frequency.value = frequency;
            gainNode.gain.value = 0.3;
            oscillator.start();
            if (type === "correct") {
                gainNode.gain.exponentialRampToValueAtTime(0.00001, audioCtx.currentTime + 0.6);
                oscillator.stop(audioCtx.currentTime + 0.6);
                // إضافة صوت "صفقة" إضافي بسيط باستخدام نبضة
                setTimeout(() => {
                    try {
                        const clapCtx = new (window.AudioContext || window.webkitAudioContext)();
                        const osc2 = clapCtx.createOscillator();
                        const gain2 = clapCtx.createGain();
                        osc2.connect(gain2);
                        gain2.connect(clapCtx.destination);
                        osc2.frequency.value = 1200;
                        gain2.gain.value = 0.2;
                        osc2.start();
                        gain2.gain.exponentialRampToValueAtTime(0.00001, clapCtx.currentTime + 0.2);
                        osc2.stop(clapCtx.currentTime + 0.2);
                    } catch(e) {}
                }, 50);
            } else {
                gainNode.gain.exponentialRampToValueAtTime(0.00001, audioCtx.currentTime + 0.4);
                oscillator.stop(audioCtx.currentTime + 0.4);
            }
        } catch(e) { console.log("صوت غير مدعوم بالمتصفح"); }
    }

    let currentIndex = 0;
    let userScore = 0;
    let answered = false;
    let selectedValue = null;
    let gameFinished = false;

    const container = document.getElementById("dynamicContent");

    function renderQuestion() {
        if (currentIndex >= questions.length) {
            showFinalResult();
            return;
        }
        const q = questions[currentIndex];
        let optionsHtml = "";
        if (q.type === "choice") {
            q.options.forEach(opt => {
                optionsHtml += `<button class="option-btn" data-value="${opt}">🔹 ${opt}</button>`;
            });
        } else { // true/false
            optionsHtml = `<button class="option-btn" data-value="صحيح">✅ صحيح</button>
                           <button class="option-btn" data-value="خطأ">❌ خطأ</button>`;
            // لكن يجب مقارنة القيمة الصحيحة "صحيح" أو "خطأ" بناء على text الصواب
        }

        const html = `
            <div class="question-area">
                <div class="question-text">📖 السؤال ${currentIndex+1} من 10: <br> ${q.text}</div>
            </div>
            <div class="options-area" id="optionsArea">
                ${optionsHtml}
            </div>
            <div class="feedback" id="feedbackMsg"></div>
            <div class="question-footer">
                <span class="counter">🏆 النقاط: ${userScore}</span>
                <button class="next-btn" id="nextBtn">التالي ➡️</button>
            </div>
        `;
        container.innerHTML = html;

        // تعطيل زر التالي في البداية
        const nextBtn = document.getElementById("nextBtn");
        nextBtn.classList.add("hidden");

        // إضافة مستمعين للخيارات
        const btns = document.querySelectorAll(".option-btn");
        btns.forEach(btn => {
            btn.addEventListener("click", (e) => {
                if (answered) return;
                let chosen = btn.getAttribute("data-value");
                const currentQ = questions[currentIndex];
                let isCorrect = false;
                // معالجة الصواب
                if (currentQ.type === "choice") {
                    if (chosen === currentQ.correct) isCorrect = true;
                } else { // true/false
                    // نسخ النص: currentQ.correct هو "للماء" أو "صحيح" مثلاً ولكن في سؤال tf يجب ضبط:
                    // نحدد بناءً على السؤال رقم 4 ورقم 7:
                    if (currentIndex === 3) { // سؤال الماء والنفط
                        if ((chosen === "صحيح" && currentQ.correct === "للماء") || (chosen === "خطأ" && currentQ.correct !== "للماء")) isCorrect = (chosen === "صحيح");
                        else isCorrect = false;
                        // تبسيط: أعد كتابة منطق tf
                    } else if (currentIndex === 6) { // سؤال العنف مناقض للإسلام
                        if ((chosen === "صحيح" && currentQ.correct === "صحيح") || (chosen === "خطأ" && currentQ.correct !== "صحيح")) isCorrect = (chosen === "صحيح");
                        else isCorrect = false;
                    } else {
                        // لأي سؤال tf عام قادم
                        if (chosen === currentQ.correct) isCorrect = true;
                        else isCorrect = false;
                    }
                    // تصحيح بسيط لمنطق tf: بما أن عندنا سؤالين tf فقط
                    if (currentIndex === 3) {
                        isCorrect = (chosen === "صحيح" && currentQ.correct === "للماء");
                    }
                    if (currentIndex === 6) {
                        isCorrect = (chosen === "صحيح" && currentQ.correct === "صحيح");
                    }
                }
                // لسؤال الاختيار العادي:
                if (currentQ.type === "choice") isCorrect = (chosen === currentQ.correct);

                answered = true;
                const feedbackDiv = document.getElementById("feedbackMsg");
                if (isCorrect) {
                    userScore++;
                    playSound("correct");
                    feedbackDiv.innerHTML = "✅ ✅ إجابة صحيحة! (صفقة) ✅ ✅";
                    feedbackDiv.style.color = "#1f6d1a";
                    // حركة سعادة مؤقتة
                    document.querySelector(".game-container").style.transform = "scale(1.01)";
                    setTimeout(()=> document.querySelector(".game-container").style.transform = "", 200);
                } else {
                    playSound("wrong");
                    let correctAnswerShow = currentQ.correct;
                    if (currentIndex === 3 && currentQ.type === "tf") correctAnswerShow = "للماء (صحيح)";
                    if (currentIndex === 6) correctAnswerShow = "صحيح";
                    feedbackDiv.innerHTML = `❌ خطأ! الإجابة الصحيحة: ${correctAnswerShow} ❌`;
                    feedbackDiv.style.color = "#b13b2d";
                    // حركة حزن
                    const containerDiv = document.querySelector(".game-container");
                    containerDiv.style.transform = "translateX(4px)";
                    setTimeout(()=> containerDiv.style.transform = "", 150);
                }
                // تحديث العداد
                const counterSpan = document.querySelector(".counter");
                if(counterSpan) counterSpan.innerHTML = `🏆 النقاط: ${userScore}`;
                // تعطيل كل أزرار الخيارات
                document.querySelectorAll(".option-btn").forEach(b => {
                    b.style.pointerEvents = "none";
                    b.style.opacity = "0.7";
                });
                // إظهار زر التالي
                nextBtn.classList.remove("hidden");
            });
        });

        nextBtn.addEventListener("click", () => {
            if (!answered) return;
            currentIndex++;
            answered = false;
            renderQuestion();
        });
    }

    function showFinalResult() {
        const total = questions.length;
        const percent = (userScore / total) * 100;
        let emoji = "";
        let happyMoves = "";
        if (userScore >= 7) {
            emoji = "🎉🎊😄🏆 نجم الصقر! 🦅🎉🎊";
            happyMoves = "⭐✨🌟";
        } else if (userScore >= 5) {
            emoji = "👍📘 جيد، يمكنك تحسين النتيجة! 🌟";
        } else {
            emoji = "😔💔 للأسف .. أعد قراءة قصة الصقر 2 وحاول مجدداً";
        }
        const finalHtml = `
            <div class="result-panel">
                <div class="emoji-big">${userScore >=7 ? "🦅🏆🎉" : (userScore>=5?"📚👍":"😢")}</div>
                <div class="score-display">${userScore} / ${total}</div>
                <p style="font-size:1.6rem; font-weight:bold;">${emoji}</p>
                <p style="margin-top:15px;">${happyMoves}</p>
                <p>🏫 مدرسة المعارف | الأستاذ محمود الرياطي  ✨</p>
                <button class="restart-btn" id="restartGameBtn">🔄 العب من جديد 🔄</button>
            </div>
        `;
        container.innerHTML = finalHtml;
        const restartBtn = document.getElementById("restartGameBtn");
        if (restartBtn) {
            restartBtn.addEventListener("click", () => {
                currentIndex = 0;
                userScore = 0;
                answered = false;
                gameFinished = false;
                renderQuestion();
            });
        }
    }

    // بدء اللعبة
    renderQuestion();
</script>
</body>
</html>
