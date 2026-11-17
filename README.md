# study
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <meta name="theme-color" content="#0f172a">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="MY STUDY AI">
    <title>MY STUDY AI - 스마트 학습 스튜디오</title>
    <link rel="manifest" href="data:application/manifest+json,{
        %22name%22:%22MY%20STUDY%20AI%22,
        %22short_name%22:%22MY%20STUDY%20AI%22,
        %22start_url%22:%22.%22,
        %22display%22:%22standalone%22,
        %22background_color%22:%22%230f172a%22,
        %22theme_color%22:%22%234f46e5%22,
        %22icons%22:[{%22src%22:%22https://cdn-icons-png.flaticon.com/512/3135/3135715.png%22,%22sizes%22:%22512x512%22,%22type%22:%22image/png%22}]
    }">
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        @import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard.css');
        body { font-family: 'Pretendard', sans-serif; -webkit-tap-highlight-color: transparent; }
    </style>
</head>
<body class="bg-slate-950 text-slate-100 min-h-screen flex flex-col">
    <div id="app" class="w-full max-w-5xl mx-auto min-h-screen bg-slate-900 shadow-2xl flex flex-col relative border-x border-slate-800">
        
        <!-- Header -->
        <header class="bg-slate-900/95 backdrop-blur border-b border-slate-800 px-5 sm:px-6 py-4 sticky top-0 z-50 flex justify-between items-center">
            <div class="flex items-center space-x-3">
                <span class="bg-indigo-600 text-white font-bold p-2.5 rounded-2xl text-lg sm:text-xl shadow-lg shadow-indigo-500/30">
                    <i class="fa-solid fa-graduation-cap"></i>
                </span>
                <div>
                    <h1 class="font-extrabold text-lg sm:text-xl text-white tracking-tight flex items-center space-x-2">
                        <span>MY STUDY AI</span>
                        <span class="text-[11px] bg-indigo-500/20 text-indigo-400 border border-indigo-500/30 px-2 py-0.5 rounded-full font-semibold">Pro</span>
                    </h1>
                    <span id="streak-badge" class="text-xs text-orange-400 font-semibold flex items-center space-x-1 mt-0.5">
                        <i class="fa-solid fa-fire"></i><span>연속 출석 1일째</span>
                    </span>
                </div>
            </div>
            <div class="flex items-center space-x-2">
                <button onclick="openInstallModal()" id="install-btn" class="bg-indigo-600/20 hover:bg-indigo-600/30 text-indigo-300 border border-indigo-500/30 px-3 py-2 rounded-xl text-xs font-bold transition flex items-center space-x-1.5">
                    <i class="fa-solid fa-mobile-screen-button"></i><span class="hidden sm:inline">앱 설치</span>
                </button>
                <button onclick="openSaveModal()" class="bg-slate-800 hover:bg-slate-700 text-slate-300 px-3 py-2 rounded-xl text-xs font-bold transition flex items-center space-x-1.5 border border-slate-700">
                    <i class="fa-solid fa-floppy-disk text-emerald-400"></i><span>데이터 백업</span>
                </button>
            </div>
        </header>

        <!-- Main Workspace -->
        <main class="flex-1 p-5 sm:p-6 space-y-6 overflow-y-auto">
            
            <!-- Dashboard -->
            <div class="grid grid-cols-1 md:grid-cols-3 gap-5">
                <section class="md:col-span-2 bg-gradient-to-br from-indigo-950/80 via-slate-900 to-slate-900 border border-indigo-500/30 rounded-3xl p-5 shadow-xl flex flex-col justify-between">
                    <div>
                        <div class="flex justify-between items-center mb-3">
                            <h2 class="text-sm font-bold text-indigo-300 flex items-center space-x-2">
                                <i class="fa-solid fa-gamepad text-indigo-400"></i><span>오늘의 학습 퀘스트 (무제한 자유 학습)</span>
                            </h2>
                            <span id="exp-text" class="text-xs font-bold text-indigo-400">EXP 0 / 100</span>
                        </div>
                        <div class="w-full bg-slate-800 h-3 rounded-full overflow-hidden mb-4">
                            <div id="exp-bar" class="bg-gradient-to-r from-indigo-500 to-purple-500 h-full transition-all duration-500" style="width: 0%"></div>
                        </div>
                    </div>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 text-xs">
                        <div class="flex justify-between items-center bg-slate-900/80 p-3 rounded-2xl border border-slate-800">
                            <span class="text-slate-300">🎯 사진 분석 및 핵심정리</span>
                            <span id="q1-status" class="px-2.5 py-1 rounded-lg bg-slate-800 text-slate-400 font-bold">진행중</span>
                        </div>
                        <div class="flex justify-between items-center bg-slate-900/80 p-3 rounded-2xl border border-slate-800">
                            <span class="text-slate-300">✍️ 맞춤 문제 풀이</span>
                            <span id="q2-status" class="px-2.5 py-1 rounded-lg bg-slate-800 text-slate-400 font-bold">진행중</span>
                        </div>
                    </div>
                </section>

                <section class="bg-slate-900 border border-slate-800 rounded-3xl p-5 shadow-xl flex flex-col justify-between">
                    <div>
                        <h3 class="text-sm font-bold text-slate-200 mb-3 flex items-center space-x-2">
                            <i class="fa-solid fa-folder-tree text-indigo-400"></i><span>내 학습 보관함</span>
                        </h3>
                        <div class="space-y-2 text-xs text-slate-400">
                            <div class="flex justify-between bg-slate-950 p-2.5 rounded-xl">
                                <span>생성된 플래시카드</span>
                                <span id="stat-cards-count" class="font-bold text-indigo-400">0개</span>
                            </div>
                            <div class="flex justify-between bg-slate-950 p-2.5 rounded-xl">
                                <span>오답 노트 보관함</span>
                                <span id="stat-incorrect-count" class="font-bold text-red-400">0개</span>
                            </div>
                        </div>
                    </div>
                    <button onclick="clearAllData()" class="mt-4 text-xs text-slate-500 hover:text-red-400 transition text-right">
                        <i class="fa-solid fa-rotate-right mr-1"></i>기록 초기화하기
                    </button>
                </section>
            </div>

            <!-- Navigation Tabs -->
            <div class="grid grid-cols-4 gap-2 bg-slate-800/80 p-1.5 rounded-2xl text-center text-xs sm:text-sm font-bold">
                <button onclick="switchTab('study')" id="tab-study" class="py-3 rounded-xl bg-indigo-600 text-white transition shadow-md">📸 사진 학습</button>
                <button onclick="switchTab('flashcard')" id="tab-flashcard" class="py-3 rounded-xl text-slate-400 hover:text-white transition">📖 플래시카드</button>
                <button onclick="switchTab('quiz')" id="tab-quiz" class="py-3 rounded-xl text-slate-400 hover:text-white transition">✍️ 맞춤 문제</button>
                <button onclick="switchTab('incorrect')" id="tab-incorrect" class="py-3 rounded-xl text-slate-400 hover:text-white transition">🚨 오답노트</button>
            </div>

            <!-- TAB 1: Study -->
            <div id="view-study" class="space-y-6">
                <div class="bg-slate-900 border border-slate-800 rounded-3xl p-5 space-y-4">
                    <h3 class="font-bold text-sm text-slate-200 flex items-center space-x-2">
                        <i class="fa-solid fa-sliders text-indigo-400"></i><span>과목 및 난이도 설정</span>
                    </h3>
                    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                        <div>
                            <label class="text-xs text-slate-400 mb-1.5 block font-medium">과목 선택</label>
                            <select id="subject-select" class="w-full bg-slate-800 border border-slate-700 text-slate-200 text-sm rounded-2xl p-3 focus:outline-none focus:border-indigo-500">
                                <option value="수학">수학</option>
                                <option value="영어">영어</option>
                                <option value="국어">국어</option>
                                <option value="과학">과학</option>
                                <option value="사회/역사">사회/역사</option>
                                <option value="기타">기타 과목</option>
                            </select>
                        </div>
                        <div>
                            <label class="text-xs text-slate-400 mb-1.5 block font-medium">문제 난이도</label>
                            <select id="difficulty-select" class="w-full bg-slate-800 border border-slate-700 text-slate-200 text-sm rounded-2xl p-3 focus:outline-none focus:border-indigo-500">
                                <option value="초급">초급 (기본 개념 확인)</option>
                                <option value="중급" selected>중급 (내신 실전형)</option>
                                <option value="고급">고급 (심화/킬러 문항)</option>
                            </select>
                        </div>
                    </div>
                    <div>
                        <label class="text-xs text-slate-400 mb-1.5 block font-medium">사진 속 핵심 키워드나 단원명 입력 (선택사항)</label>
                        <input type="text" id="topic-input" placeholder="예: 이차방정식 근의 공식, 관계대명사 what 등" class="w-full bg-slate-800 border border-slate-700 text-slate-200 text-sm rounded-2xl p-3 focus:outline-none focus:border-indigo-500 placeholder-slate-500">
                    </div>
                </div>

                <div class="bg-slate-900 border border-slate-800 rounded-3xl p-6 text-center space-y-5 shadow-xl">
                    <div id="image-preview-wrapper" class="hidden space-y-2">
                        <div class="flex justify-between items-center text-xs text-slate-400 px-1">
                            <span id="image-count-label" class="font-bold text-indigo-400">업로드된 사진 0장</span>
                            <button onclick="clearImages()" class="text-red-400 hover:underline">전체 삭제</button>
                        </div>
                        <div id="image-preview-container" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-3 max-h-96 overflow-y-auto p-3 bg-slate-950 rounded-2xl border border-slate-700"></div>
                    </div>

                    <div class="border-2 border-dashed border-slate-700 hover:border-indigo-500 rounded-3xl p-8 transition cursor-pointer flex flex-col items-center justify-center space-y-3 bg-slate-950/40" onclick="document.getElementById('file-input').click()">
                        <div class="w-16 h-16 bg-indigo-600/20 text-indigo-400 rounded-full flex items-center justify-center text-2xl shadow-inner">
                            <i class="fa-solid fa-images"></i>
                        </div>
                        <div>
                            <p class="font-bold text-base text-slate-200">교과서·노트 사진 여러 장 올리기</p>
                            <p class="text-xs text-slate-500 mt-1">여러 장을 한 번에 선택해서 올릴 수 있습니다</p>
                        </div>
                    </div>
                    <input type="file" id="file-input" accept="image/*" multiple class="hidden" onchange="handleImageUpload(event)">

                    <button onclick="analyzeUserImages()" class="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-bold py-4 px-6 rounded-2xl text-sm transition shadow-lg shadow-indigo-600/30 flex items-center justify-center space-x-2">
                        <i class="fa-solid fa-wand-magic-sparkles"></i><span>사진 내용 분석 & 맞춤 플래시카드·문제 생성하기</span>
                    </button>
                </div>

                <div id="result-section" class="hidden space-y-4">
                    <div class="bg-slate-900 border border-indigo-500/30 rounded-3xl p-6 space-y-4 shadow-xl">
                        <div class="flex justify-between items-center">
                            <h3 class="font-bold text-base text-indigo-300 flex items-center space-x-2">
                                <i class="fa-solid fa-file-lines"></i><span>사진 기반 핵심 요약 노트</span>
                            </h3>
                            <span class="bg-emerald-500/10 text-emerald-400 border border-emerald-500/30 px-3 py-1 rounded-xl text-xs font-bold">
                                <i class="fa-solid fa-check mr-1"></i>자동 저장됨
                            </span>
                        </div>
                        <div id="summary-content" class="text-sm text-slate-300 leading-relaxed bg-slate-950 p-5 rounded-2xl border border-slate-800 space-y-2.5"></div>
                        <div class="grid grid-cols-2 gap-3 pt-2">
                            <button onclick="switchTab('flashcard')" class="bg-slate-800 hover:bg-slate-700 text-indigo-300 font-bold py-3 rounded-2xl text-xs transition border border-slate-700">
                                📖 생성된 플래시카드 보기
                            </button>
                            <button onclick="switchTab('quiz')" class="bg-indigo-600 hover:bg-indigo-500 text-white font-bold py-3 rounded-2xl text-xs transition shadow">
                                ✍️ 맞춤 문제 바로 풀기
                            </button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- TAB 2: Flashcard -->
            <div id="view-flashcard" class="hidden space-y-6">
                <div class="bg-slate-900 border border-slate-800 rounded-3xl p-6 text-center space-y-5 shadow-xl">
                    <div class="flex justify-between items-center text-xs text-slate-400 font-medium">
                        <span id="card-counter">카드 0 / 0</span>
                        <span class="text-indigo-400 font-semibold bg-indigo-500/10 px-3 py-1 rounded-full border border-indigo-500/20">카드를 터치해서 정답 확인 🔄</span>
                    </div>
                    <div id="flashcard-box" onclick="flipCard()" class="w-full h-64 bg-gradient-to-br from-slate-800 to-slate-900 border border-slate-700 rounded-3xl p-8 flex flex-col items-center justify-center cursor-pointer shadow-2xl transition transform hover:scale-[1.01]">
                        <span id="card-label" class="text-xs font-bold text-indigo-400 mb-3 tracking-wider uppercase">핵심 개념</span>
                        <p id="card-text" class="text-lg font-bold text-slate-100 text-center leading-relaxed">사진을 먼저 업로드하고 분석을 진행해주세요!</p>
                    </div>
                    <div class="flex space-x-3">
                        <button onclick="prevCard()" class="flex-1 bg-slate-800 hover:bg-slate-700 text-slate-300 py-3.5 rounded-2xl text-xs font-bold transition border border-slate-700">
                            <i class="fa-solid fa-arrow-left mr-1"></i> 이전 카드
                        </button>
                        <button onclick="nextCard()" class="flex-1 bg-indigo-600 hover:bg-indigo-500 text-white py-3.5 rounded-2xl text-xs font-bold transition shadow-md">
                            다음 카드 <i class="fa-solid fa-arrow-right ml-1"></i>
                        </button>
                    </div>
                </div>
            </div>

            <!-- TAB 3: Quiz -->
            <div id="view-quiz" class="hidden space-y-6">
                <div id="quiz-container" class="bg-slate-900 border border-slate-800 rounded-3xl p-6 space-y-5 shadow-xl">
                    <div class="flex justify-between items-center text-xs text-slate-400 font-medium">
                        <span id="quiz-progress">문제 0 / 0</span>
                        <span id="quiz-score" class="text-indigo-400 font-bold">정답 0</span>
                    </div>
                    <p id="quiz-question" class="text-base font-bold text-slate-100 leading-snug">업로드된 사진을 기반으로 생성된 맞춤 문제가 여기에 표시됩니다.</p>
                    <div id="quiz-options" class="space-y-3"></div>
                    <div id="quiz-feedback" class="hidden p-4 rounded-2xl text-xs sm:text-sm font-medium leading-relaxed"></div>
                    <button id="quiz-next-btn" onclick="nextQuiz()" class="hidden w-full bg-indigo-600 hover:bg-indigo-500 text-white font-bold py-3.5 rounded-2xl text-sm transition shadow-lg">다음 문제 풀기</button>
                </div>
            </div>

            <!-- TAB 4: Incorrect Notes -->
            <div id="view-incorrect" class="hidden space-y-6">
                <div class="bg-slate-900 border border-slate-800 rounded-3xl p-6 space-y-4 shadow-xl">
                    <div class="flex justify-between items-center">
                        <h3 class="font-bold text-base text-red-400 flex items-center space-x-2">
                            <i class="fa-solid fa-triangle-exclamation"></i><span>오답 노트 보관함</span>
                        </h3>
                        <span id="incorrect-count" class="text-xs text-slate-400 font-semibold bg-red-500/10 px-3 py-1 rounded-full border border-red-500/20">0개 보관됨</span>
                    </div>
                    <div id="incorrect-list" class="space-y-3">
                        <p class="text-xs text-slate-500 text-center py-12">틀린 문제는 오답 노트에 자동 저장되어 언제든 다시 풀 수 있습니다.</p>
                    </div>
                </div>
            </div>
        </main>

        <!-- Install Guide Modal -->
        <div id="install-modal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
            <div class="bg-slate-900 border border-slate-800 rounded-3xl p-6 w-full max-w-md space-y-5 shadow-2xl">
                <div class="flex justify-between items-center">
                    <h3 class="font-bold text-base text-white flex items-center space-x-2">
                        <i class="fa-solid fa-mobile-screen-button text-indigo-400"></i><span>홈 화면에 앱으로 설치하기</span>
                    </h3>
                    <button onclick="closeInstallModal()" class="text-slate-400 hover:text-white text-lg"><i class="fa-solid fa-xmark"></i></button>
                </div>
                <div class="space-y-3 text-xs text-slate-300 leading-relaxed">
                    <div class="bg-slate-950 p-3.5 rounded-2xl border border-slate-800">
                        <p class="font-bold text-indigo-400 mb-1">📱 안드로이드 (크롬)</p>
                        <p>우측 상단 <strong>[⋮] 메뉴</strong> 터치 → <strong>[앱 설치]</strong> 또는 <strong>[홈 화면에 추가]</strong> 선택</p>
                    </div>
                    <div class="bg-slate-950 p-3.5 rounded-2xl border border-slate-800">
                        <p class="font-bold text-sky-400 mb-1">🍎 아이폰 · 아이패드 (Safari)</p>
                        <p>하단 <strong>[공유]</strong> 버튼 터치 → <strong>[홈 화면에 추가]</strong> 선택</p>
                    </div>
                </div>
                <button onclick="closeInstallModal()" class="w-full bg-indigo-600 hover:bg-indigo-500 text-white font-bold py-3 rounded-2xl text-xs transition">확인</button>
            </div>
        </div>

        <!-- Save Data Modal -->
        <div id="save-modal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-sm z-50 hidden flex items-center justify-center p-4">
            <div class="bg-slate-900 border border-slate-800 rounded-3xl p-6 w-full max-w-md space-y-5 shadow-2xl">
                <div class="flex justify-between items-center">
                    <h3 class="font-bold text-base text-white flex items-center space-x-2">
                        <i class="fa-solid fa-floppy-disk text-