# 2-1
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MBTI로 찾는 나의 포켓몬</title>
    <style>
        :root {
            --bg-cream: #FFFDF0;
            --card-bg: #FFFFFF;
            --primary-yellow: #FFDE00;
            --primary-border: #E6C200;
            --accent-blue: #3B4CCA;
            --text-dark: #2B2B2B;
            --text-muted: #666666;
            --shadow-soft: 0 10px 25px -5px rgba(230, 194, 0, 0.25), 0 8px 10px -6px rgba(0, 0, 0, 0.05);
            --shadow-card: 0 4px 15px rgba(0, 0, 0, 0.05);
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Pretendard', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            background-color: var(--bg-cream);
            color: var(--text-dark);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px 16px;
            background-image: radial-gradient(#FFE866 1.5px, transparent 1.5px);
            background-size: 24px 24px;
        }

        .container {
            width: 100%;
            max-width: 680px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 28px;
        }

        .main-title {
            font-size: 2rem;
            font-weight: 800;
            color: #2A2A2A;
            margin-bottom: 8px;
            word-break: keep-all;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .main-title span.badge {
            background-color: var(--primary-yellow);
            color: var(--accent-blue);
            padding: 4px 12px;
            border-radius: 20px;
            font-size: 1.1rem;
            border: 2px solid var(--accent-blue);
        }

        .subtitle {
            font-size: 1.1rem;
            color: var(--text-muted);
            font-weight: 500;
        }

        .mbti-grid-card {
            background: var(--card-bg);
            border-radius: 24px;
            padding: 28px 20px;
            box-shadow: var(--shadow-soft);
            border: 3px solid #FFF3B0;
            transition: all 0.3s ease;
        }

        .section-label {
            text-align: center;
            font-size: 1.25rem;
            font-weight: 700;
            margin-bottom: 20px;
            color: var(--accent-blue);
        }

        .mbti-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
        }

        @media (max-width: 480px) {
            .mbti-grid {
                grid-template-columns: repeat(2, 1fr);
                gap: 10px;
            }
            .main-title {
                font-size: 1.6rem;
            }
        }

        .mbti-btn {
            background-color: #FFF9D6;
            border: 2px solid #FFE866;
            border-radius: 16px;
            padding: 16px 8px;
            font-size: 1.2rem;
            font-weight: 800;
            color: #4A3E00;
            cursor: pointer;
            transition: all 0.2s ease;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            gap: 4px;
            box-shadow: 0 4px 0 #E6C200;
        }

        .mbti-btn:hover {
            background-color: var(--primary-yellow);
            transform: translateY(-2px);
            box-shadow: 0 6px 0 #D4B200;
        }

        .mbti-btn:active {
            transform: translateY(2px);
            box-shadow: 0 2px 0 #D4B200;
        }

        .mbti-btn .desc-tag {
            font-size: 0.75rem;
            font-weight: 600;
            color: #8C7300;
        }

        .result-card {
            display: none;
            background: var(--card-bg);
            border-radius: 28px;
            padding: 32px 24px;
            box-shadow: var(--shadow-soft);
            border: 3px solid var(--primary-yellow);
            text-align: center;
            animation: fadeIn 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            position: relative;
            overflow: hidden;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.95) translateY(10px); }
            to { opacity: 1; transform: scale(1) translateY(0); }
        }

        .mbti-badge {
            display: inline-block;
            background-color: var(--accent-blue);
            color: white;
            font-size: 1.1rem;
            font-weight: 700;
            padding: 6px 18px;
            border-radius: 50px;
            margin-bottom: 16px;
            box-shadow: 0 3px 6px rgba(59, 76, 202, 0.3);
        }

        .pokemon-emoji {
            font-size: 6rem;
            line-height: 1;
            margin: 16px 0;
            filter: drop-shadow(0 8px 12px rgba(0, 0, 0, 0.1));
            animation: bounce 2s infinite alternate ease-in-out;
        }

        @keyframes bounce {
            0% { transform: translateY(0); }
            100% { transform: translateY(-10px); }
        }

        .pokemon-title {
            font-size: 1.1rem;
            color: #888;
            font-weight: 600;
            margin-bottom: 4px;
        }

        .pokemon-name {
            font-size: 2.2rem;
            font-weight: 900;
            color: var(--text-dark);
            margin-bottom: 20px;
        }

        .reason-box {
            background-color: #FFFDF0;
            border: 2px dashed #FFE066;
            border-radius: 18px;
            padding: 20px;
            font-size: 1.05rem;
            line-height: 1.6;
            color: #333333;
            text-align: left;
            margin-bottom: 24px;
            word-break: keep-all;
        }

        .reason-box p {
            margin-bottom: 8px;
        }

        .reason-box p:last-child {
            margin-bottom: 0;
        }

        .compatibility-box {
            background-color: #F0F4FF;
            border-radius: 18px;
            padding: 16px;
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 28px;
            border: 1.5px solid #D0DCFF;
        }

        .compat-title {
            font-size: 0.95rem;
            font-weight: 700;
            color: #3B4CCA;
            text-align: left;
        }

        .compat-value {
            font-size: 1.15rem;
            font-weight: 800;
            color: #1A2B99;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .reset-btn {
            width: 100%;
            background-color: var(--primary-yellow);
            color: #222222;
            border: none;
            border-radius: 18px;
            padding: 18px;
            font-size: 1.2rem;
            font-weight: 800;
            cursor: pointer;
            box-shadow: 0 5px 0 #D4B200;
            transition: all 0.2s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .reset-btn:hover {
            background-color: #FFE533;
            transform: translateY(-2px);
            box-shadow: 0 7px 0 #C4A200;
        }

        .reset-btn:active {
            transform: translateY(2px);
            box-shadow: 0 2px 0 #C4A200;
        }

        footer {
            text-align: center;
            margin-top: 32px;
            font-size: 0.9rem;
            color: #A09050;
        }
    </style>
</head>
<body>

    <div class="container">
        <header>
            <h1 class="main-title">
                <span>MBTI</span> 포켓몬 찾기 ⚡
            </h1>
            <p class="subtitle">나의 성격 유형과 가장 닮은 포켓몬은 누구일까요?</p>
        </header>

        <!-- MBTI Grid Selection Card -->
        <div id="selectionCard" class="mbti-grid-card">
            <div class="section-label">👇 당신의 MBTI를 선택해 주세요!</div>
            <div class="mbti-grid">
                <button class="mbti-btn" onclick="showResult('ISTJ')">
                    ISTJ
                    <span class="desc-tag">원칙주의자</span>
                </button>
                <button class="mbti-btn" onclick="showResult('ISFJ')">
                    ISFJ
                    <span class="desc-tag">수호자</span>
                </button>
                <button class="mbti-btn" onclick="showResult('INFJ')">
                    INFJ
                    <span class="desc-tag">통찰가</span>
                </button>
                <button class="mbti-btn" onclick="showResult('INTJ')">
                    INTJ
                    <span class="desc-tag">전략가</span>
                </button>
                <button class="mbti-btn" onclick="showResult('ISTP')">
                    ISTP
                    <span class="desc-tag">장인</span>
                </button>
                <button class="mbti-btn" onclick="showResult('ISFP')">
                    ISFP
                    <span class="desc-tag">예술가</span>
                </button>
                <button class="mbti-btn" onclick="showResult('INFP')">
                    INFP
                    <span class="desc-tag">중재자</span>
                </button>
                <button class="mbti-btn" onclick="showResult('INTP')">
                    INTP
                    <span class="desc-tag">아이디어상</span>
                </button>
                <button class="mbti-btn" onclick="showResult('ESTP')">
                    ESTP
                    <span class="desc-tag">활동가</span>
                </button>
                <button class="mbti-btn" onclick="showResult('ESFP')">
                    ESFP
                    <span class="desc-tag">연예인</span>
                </button>
                <button class="mbti-btn" onclick="showResult('ENFP')">
                    ENFP
                    <span class="desc-tag">활동가</span>
                </button>
                <button class="mbti-btn" onclick="showResult('ENTP')">
                    ENTP
                    <span class="desc-tag">변론가</span>
                </button>
                <button class="mbti-btn" onclick="showResult('ESTJ')">
                    ESTJ
                    <span class="desc-tag">경영자</span>
                </button>
                <button class="mbti-btn" onclick="showResult('ESFJ')">
                    ESFJ
                    <span class="desc-tag">친선도모자</span>
                </button>
                <button class="mbti-btn" onclick="showResult('ENFJ')">
                    ENFJ
                    <span class="desc-tag">선도자</span>
                </button>
                <button class="mbti-btn" onclick="showResult('ENTJ')">
                    ENTJ
                    <span class="desc-tag">지휘관</span>
                </button>
            </div>
        </div>

        <!-- Result View Card -->
        <div id="resultCard" class="result-card">
            <div id="mbtiBadge" class="mbti-badge">ISTJ</div>
            <div id="pokemonEmoji" class="pokemon-emoji">🐢</div>
            <div id="pokemonTitle" class="pokemon-title">단단한 원칙주의자</div>
            <div id="pokemonName" class="pokemon-name">거북왕</div>

            <div class="reason-box">
                <p id="reasonText1">철저한 계획과 강한 책임감으로 무장한 모습이 꼭 닮았습니다.</p>
                <p id="reasonText2">어떤 시련이 와도 흔들리지 않는 단단한 방어력과 신뢰감을 줍니다.</p>
                <p id="reasonText3">묵묵히 자신의 역할을 완수하는 신뢰할 수 있는 리더 타입입니다.</p>
            </div>

            <div class="compatibility-box">
                <div class="compat-title">❤️ 환상의 짝꿍 (잘 맞는 유형)</div>
                <div id="compatText" class="compat-value">ENFP (피카츄) ⚡</div>
            </div>

            <button class="reset-btn" onclick="resetSelection()">
                🔄 다시 고르기
            </button>
        </div>

        <footer>
            포켓몬으로 알아보는 나의 성격 유형 이야기
        </footer>
    </div>

    <script>
        // 16가지 MBTI 매칭 포켓몬 데이터베이스
        const pokemonData = {
            'ISTJ': {
                name: '거북왕',
                title: '철저하고 단단한 원칙주의자',
                emoji: '🐢',
                reasons: [
                    '매사에 철저하고 책임감이 강하여 어떤 임무든 완벽하게 해냅니다.',
                    '묵묵히 자신의 자리를 지키며 단단한 방어력으로 주변에 깊은 신뢰를 줍니다.',
                    '규칙과 질서를 중요하게 생각하여 언제나 믿을 수 있는 든든한 조력자입니다.'
                ],
                compat: 'ENFP (피카츄)'
            },
            'ISFJ': {
                name: '해피너스',
                title: '다정하고 따뜻한 수호자',
                emoji: '🌸',
                reasons: [
                    '타인의 아픔을 깊이 공감하고 언제나 세심하게 챙겨주는 따뜻한 마음씨를 가졌습니다.',
                    '상대방이 필요한 것을 먼저 파악하여 헌신적으로 도와주는 평화주의자입니다.',
                    '조용하지만 강한 책임감으로 주변 사람들의 행복을 끝까지 지켜줍니다.'
                ],
                compat: 'ESFP (푸린)'
            },
            'INFJ': {
                name: '뮤츠',
                title: '깊은 통찰력을 지닌 신비로운 전략가',
                emoji: '🔮',
                reasons: [
                    '생각이 깊고 통찰력이 뛰어나 세상의 이치와 상대방의 본심을 잘 파악합니다.',
                    '혼자만의 시간을 중요하게 생각하며 자신만의 명확한 철학을 가지고 있습니다.',
                    '겉은 차가워 보일 수 있지만 내면에는 이상적인 세상을 꿈꾸는 신념이 있습니다.'
                ],
                compat: 'ENFP (피카츄)'
            },
            'INTJ': {
                name: '아머까오',
                title: '냉철하고 치밀한 전략가',
                emoji: '🦅',
                reasons: [
                    '장기적인 목표를 세우고 치밀한 계획에 따라 능숙하게 상황을 지배합니다.',
                    '감정에 휘둘리지 않고 합리적이고 효율적인 선택을 내리는 데 탁월합니다.',
                    '높은 기준을 가지고 자신과 타인을 계속해서 발전시키고자 노력합니다.'
                ],
                compat: 'ENTP (팬텀)'
            },
            'ISTP': {
                name: '루카리오',
                title: '침착하고 조용한 만능 해결사',
                emoji: '🐺',
                reasons: [
                    '위기 상황에서도 침착함을 잃지 않고 상황을 신속하고 정확하게 해결합니다.',
                    '말보다는 행동으로 보여주며 실용적이고 기계나 기술 다루기에 능숙합니다.',
                    '자유로운 영혼으로 혼자서도 문제를 척척 해결하는 마이웨이 스타일입니다.'
                ],
                compat: 'ESFJ (라이츄)'
            },
            'ISFP': {
                name: '메타몽',
                title: '유연하고 감성적인 예술가',
                emoji: '🟣',
                reasons: [
                    '온화하고 유연한 성격으로 어떤 환경이나 사람과도 잘 어우러집니다.',
                    '예술적 감각과 감성이 풍부하여 자신만의 방식으로 마음을 표현합니다.',
                    '틀에 매이는 것을 싫어하고 현재의 자유와 일상의 소소한 기쁨을 즐깁니다.'
                ],
                compat: 'ESTJ (윈디)'
            },
            'INFP': {
                name: '이브이',
                title: '무한한 가능성을 품은 몽상가',
                emoji: '🦊',
                reasons: [
                    '무궁무진한 잠재력과 상상력을 가지고 있어 어떤 형태(진화)로든 발전할 수 있습니다.',
                    '순수하고 따뜻한 마음을 품고 있어 가치관과 이상을 매우 중요하게 여깁니다.',
                    '상대방의 감정에 깊이 공감해주며 조용히 자신만의 꿈을 키워나갑니다.'
                ],
                compat: 'ENTJ (괴력몬)'
            },
            'INTP': {
                name: '폴리곤',
                title: '호기심 많은 논리적 탐구가',
                emoji: '💻',
                reasons: [
                    '새로운 지식과 원리를 탐구하는 것을 좋아하며 논리적인 사고 능력이 뛰어납니다.',
                    '복잡한 문제를 단순하게 분석하고 독창적인 새로운 아이디어를 잘 떠올립니다.',
                    '감정적인 논쟁보다는 객관적인 사실과 호기심 충족을 우선시합니다.'
                ],
                compat: 'ENTJ (괴력몬)'
            },
            'ESTP': {
                name: '리자몽',
                title: '열정적이고 모험을 즐기는 활동가',
                emoji: '🔥',
                reasons: [
                    '스릴과 모험을 즐기며 강한 에너지로 현장의 분위기를 주도합니다.',
                    '직관적이고 빠르게 행동에 옮기며 문제에 부딪혀 직접 해결하는 것을 선호합니다.',
                    '자신감이 넘치고 솔직하여 누구와도 금방 친해지는 위풍당당한 타입입니다.'
                ],
                compat: 'ISFJ (해피너스)'
            },
            'ESFP': {
                name: '푸린',
                title: '사랑스러운 분위기 메이커',
                emoji: '🎤',
                reasons: [
                    '언제나 통통 튀는 매력과 밝은 에너지로 사람들의 주목을 받는 것을 즐깁니다.',
                    '사교성이 뛰어나 분위기를 흥겹게 만들며 주변 사람들에게 즐거움을 선사합니다.',
                    '감정에 솔직하고 열정적이라 같이 있으면 시간 가는 줄 모르는 인싸입니다.'
                ],
                compat: 'ISFJ (해피너스)'
            },
            'ENFP': {
                name: '피카츄',
                title: '톡톡 튀는 에너자이저',
                emoji: '⚡',
                reasons: [
                    '풍부한 상상력과 밝고 긍정적인 에너지로 주변을 환하게 밝혀줍니다.',
                    '호기심이 많아 새로운 일에 주저 없이 도전하며 정이 많아 친구를 잘 만듭니다.',
                    '자유로운 분위기 속에서 자신만의 통통 튀는 아이디어를 거침없이 발휘합니다.'
                ],
                compat: 'INTJ (아머까오)'
            },
            'ENTP': {
                name: '팬텀',
                title: '재치 있고 재기발랄한 변론가',
                emoji: '👻',
                reasons: [
                    '장난기 많고 두뇌 회전이 빨라 독창적이고 예상치 못한 아이디어를 쏟아냅니다.',
                    '기존의 틀을 깨는 고정관념 파괴를 즐기며 호기심 어린 논쟁을 좋아합니다.',
                    '지루한 것을 참지 못하며 솔직하고 당당한 매력으로 주변을 사로잡습니다.'
                ],
                compat: 'INFJ (뮤츠)'
            },
            'ESTJ': {
                name: '윈디',
                title: '당당하고 추진력 있는 리더',
                emoji: '🦁',
                reasons: [
                    '체계적이고 리더십이 뛰어나 집단을 안정감 있게 끌어나가는 능력이 있습니다.',
                    '목표가 정해지면 강한 추진력과 결단력으로 화끈하게 완수해냅니다.',
                    '자신의 사람들을 의리 있게 챙기며 정의롭고 확실한 기준을 가지고 있습니다.'
                ],
                compat: 'ISFP (메타몽)'
            },
            'ESFJ': {
                name: '라이츄',
                title: '친절하고 사교적인 분위기 조율자',
                emoji: '🐭',
                reasons: [
                    '친화력이 좋아 누구와도 금방 친해지며 따뜻한 에너지로 주변을 다독입니다.',
                    '주변 사람들의 기분을 잘 살피고 조화를 이루도록 돕는 모범적인 사교가입니다.',
                    '타인에게 도움을 줄 때 큰 보람을 느끼며 관계를 진실되게 유지합니다.'
                ],
                compat: 'ISTP (루카리오)'
            },
            'ENFJ': {
                name: '망나뇽',
                title: '너그럽고 카리스마 있는 선도자',
                emoji: '🐉',
                reasons: [
                    '상대방을 포용하는 온화함과 동시에 선한 영향력을 넓히는 카리스마를 갖췄습니다.',
                    '다른 사람들의 성장을 진심으로 응원하며 비전과 희망을 제시해 줍니다.',
                    '어려움에 처한 이들을 외면하지 않고 나서서 도와주는 성인군자 같은 타입입니다.'
                ],
                compat: 'INFP (이브이)'
            },
            'ENTJ': {
                name: '괴력몬',
                title: '자신감 넘치는 카리스마 지휘관',
                emoji: '💪',
                reasons: [
                    '확고한 비전과 열정으로 목표를 향해 무섭게 돌진하는 단호함이 있습니다.',
                    '어려운 장애물도 압도적인 해결 능력과 리더십으로 돌파해냅니다.',
                    '자기관리가 철저하며 효율적인 팀워크와 확실한 성과를 이끌어냅니다.'
                ],
                compat: 'INTP (폴리곤)'
            }
        };

        function showResult(mbti) {
            const data = pokemonData[mbti];
            if (!data) return;

            // Update UI elements with data
            document.getElementById('mbtiBadge').innerText = mbti;
            document.getElementById('pokemonEmoji').innerText = data.emoji;
            document.getElementById('pokemonTitle').innerText = data.title;
            document.getElementById('pokemonName').innerText = data.name;
            
            document.getElementById('reasonText1').innerText = "• " + data.reasons[0];
            document.getElementById('reasonText2').innerText = "• " + data.reasons[1];
            document.getElementById('reasonText3').innerText = "• " + data.reasons[2];

            document.getElementById('compatText').innerText = data.compat;

            // Switch views
            document.getElementById('selectionCard').style.display = 'none';
            document.getElementById('resultCard').style.display = 'block';

            // Scroll smoothly to top
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }

        function resetSelection() {
