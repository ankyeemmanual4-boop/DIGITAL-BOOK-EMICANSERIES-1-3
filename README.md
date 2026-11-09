<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Emican English Series: Digital Book Reader (Basic 1 - 3)</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;500;600;700&family=Quicksand:wght@500;600;700&family=Lexend:wght@400;600;700&display=swap" rel="stylesheet">
    
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        ghanaRed: '#CE1126',
                        ghanaYellow: '#FCD116',
                        ghanaGreen: '#006B3F',
                        ghanaGold: '#D4AF37',
                        kenteOrange: '#E65100',
                        kenteBlue: '#0D47A1',
                        paperLight: '#FFFDF9',
                        paperDark: '#1E2022',
                    },
                    fontFamily: {
                        fredoka: ['Fredoka', 'sans-serif'],
                        quicksand: ['Quicksand', 'sans-serif'],
                        lexend: ['Lexend', 'sans-serif'],
                    }
                }
            }
        }
    </script>

    <style>
        body {
            font-family: 'Quicksand', sans-serif;
            transition: background-color 0.3s, color 0.3s;
        }

        /* Ghanaian Kente Top Ribbon Pattern */
        .kente-border-top {
            background: repeating-linear-gradient(
                90deg,
                #CE1126 0px, #CE1126 15px,
                #FCD116 15px, #FCD116 30px,
                #006B3F 30px, #006B3F 45px,
                #000000 45px, #000000 50px,
                #E65100 50px, #E65100 65px
            );
            height: 10px;
        }

        .book-shadow {
            box-shadow: 0 25px 35px -5px rgba(0, 0, 0, 0.18), 0 10px 10px -5px rgba(0, 0, 0, 0.05);
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 7px;
        }
        ::-webkit-scrollbar-track {
            background: rgba(0,0,0,0.05);
        }
        ::-webkit-scrollbar-thumb {
            background: #006B3F;
            border-radius: 4px;
        }

        /* Audio Wave Pulse */
        @keyframes pulse-ring {
            0% { transform: scale(0.95); opacity: 0.8; }
            50% { transform: scale(1.08); opacity: 1; }
            100% { transform: scale(0.95); opacity: 0.8; }
        }
        .speaking-animation {
            animation: pulse-ring 1.5s infinite ease-in-out;
        }
    </style>
</head>
<body class="bg-[#F3EFE6] dark:bg-gray-950 text-gray-800 dark:text-gray-100 min-h-screen flex flex-col">

    <!-- Top Kente Ribbon -->
    <div class="kente-border-top"></div>

    <!-- Header -->
    <header class="bg-white dark:bg-gray-900 border-b border-amber-200 dark:border-gray-800 shadow-sm sticky top-0 z-40">
        <div class="max-w-7xl mx-auto px-4 py-2.5 flex flex-wrap items-center justify-between gap-3">
            
            <!-- Brand & Series Title -->
            <div class="flex items-center gap-3">
                <div class="w-11 h-11 bg-ghanaGreen rounded-2xl flex items-center justify-center text-white text-2xl shadow-md border-2 border-ghanaYellow">
                    <i class="fa-solid fa-graduation-cap"></i>
                </div>
                <div>
                    <h1 class="font-fredoka text-xl sm:text-2xl font-bold text-gray-900 dark:text-white tracking-wide flex items-center gap-2">
                        EMICAN ENGLISH SERIES
                        <span class="text-[10px] bg-ghanaGold/20 text-yellow-900 dark:text-ghanaYellow border border-ghanaGold/50 px-2 py-0.5 rounded-full font-sans font-bold">
                            NaCCA Primary Standards
                        </span>
                    </h1>
                    <p class="text-xs text-gray-500 dark:text-gray-400 font-medium">Digital Pupil's Reader (Basic 1, 2 & 3 • 200+ Pages)</p>
                </div>
            </div>

            <!-- Global Actions & Book Switcher -->
            <div class="flex items-center gap-3">
                
                <!-- Book Volume Selector -->
                <select id="bookVolumeSelect" onchange="changeBookVolume(this.value)" class="bg-amber-50 dark:bg-gray-800 border-2 border-ghanaGold dark:border-amber-600 text-gray-900 dark:text-white text-xs sm:text-sm rounded-xl font-bold p-2 focus:ring-2 focus:ring-ghanaGreen outline-none cursor-pointer">
                    <option value="b1">Pupil's Book 1 (Pages 1 - 70)</option>
                    <option value="b2">Pupil's Book 2 (Pages 71 - 140)</option>
                    <option value="b3">Pupil's Book 3 (Pages 141 - 210)</option>
                </select>

                <!-- Dark Mode Toggle -->
                <button onclick="toggleDarkMode()" class="w-9 h-9 bg-gray-100 dark:bg-gray-800 hover:bg-gray-200 dark:hover:bg-gray-700 rounded-xl flex items-center justify-center text-gray-700 dark:text-ghanaYellow transition">
                    <i class="fa-solid fa-moon dark:hidden"></i>
                    <i class="fa-solid fa-sun hidden dark:block"></i>
                </button>

                <!-- Bookmarks Panel Trigger -->
                <button onclick="toggleBookmarksModal()" class="w-9 h-9 bg-amber-100 dark:bg-amber-900/40 text-amber-900 dark:text-amber-300 rounded-xl flex items-center justify-center text-sm font-bold relative hover:bg-amber-200 transition">
                    <i class="fa-solid fa-bookmark"></i>
                    <span id="bookmarkBadge" class="absolute -top-1 -right-1 bg-ghanaRed text-white text-[9px] w-4 h-4 rounded-full flex items-center justify-center font-bold">0</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main App Container -->
    <main class="flex-1 max-w-7xl w-full mx-auto p-3 sm:p-5 grid grid-cols-1 lg:grid-cols-12 gap-5">

        <!-- Left Navigation Sidebar (Index & Jumper) -->
        <aside class="lg:col-span-3 bg-white dark:bg-gray-900 rounded-3xl p-4 border border-amber-200/80 dark:border-gray-800 shadow-sm flex flex-col h-[520px] lg:h-[820px]">
            
            <!-- Index Header -->
            <div class="flex items-center justify-between mb-2 pb-2 border-b border-gray-100 dark:border-gray-800">
                <h2 class="font-fredoka font-bold text-base text-ghanaGreen dark:text-emerald-400 flex items-center gap-2">
                    <i class="fa-solid fa-book-open text-xs"></i> Curriculum Index
                </h2>
                <span id="currentPageBadge" class="text-xs font-bold bg-ghanaYellow/30 text-amber-900 dark:text-yellow-300 px-2.5 py-0.5 rounded-full">
                    Page 1 / 210
                </span>
            </div>

            <!-- Page Jumper Box -->
            <div class="bg-amber-50 dark:bg-gray-800/80 border border-amber-200 dark:border-gray-700 rounded-2xl p-3 mb-3">
                <div class="flex items-center justify-between text-xs font-bold text-gray-700 dark:text-gray-300 mb-1.5">
                    <span>Direct Page Jumper</span>
                    <span id="jumperLabel" class="text-ghanaGreen dark:text-emerald-400">Page 1</span>
                </div>
                <div class="flex items-center gap-2">
                    <input type="range" id="pageSlider" min="1" max="210" value="1" oninput="onSliderChange(this.value)" class="w-full accent-ghanaGreen cursor-pointer">
                    <input type="number" id="pageInput" min="1" max="210" value="1" onchange="onNumberInput(this.value)" class="w-14 bg-white dark:bg-gray-900 border border-amber-300 dark:border-gray-600 rounded-lg text-center text-xs font-bold py-1">
                </div>
            </div>

            <!-- TOC Search -->
            <div class="relative mb-3">
                <i class="fa-solid fa-magnifying-glass absolute left-3 top-2.5 text-gray-400 text-xs"></i>
                <input type="text" id="tocSearch" placeholder="Search page title or topic..." class="w-full bg-gray-50 dark:bg-gray-800 border border-gray-200 dark:border-gray-700 rounded-xl pl-8 pr-3 py-1.5 text-xs focus:ring-2 focus:ring-ghanaGreen outline-none">
            </div>

            <!-- Scrollable Page List -->
            <div id="tocList" class="flex-1 overflow-y-auto space-y-1 pr-1">
                <!-- Dynamically populated 200+ page items -->
            </div>

            <!-- Learning Progress Tracker -->
            <div class="mt-3 pt-3 border-t border-gray-100 dark:border-gray-800">
                <div class="flex justify-between text-xs text-gray-500 dark:text-gray-400 font-bold mb-1">
                    <span>Mastery Progress</span>
                    <span id="progressPercent">0%</span>
                </div>
                <div class="w-full bg-gray-100 dark:bg-gray-800 h-2.5 rounded-full overflow-hidden">
                    <div id="progressBar" class="bg-ghanaGreen h-full w-0 transition-all duration-300"></div>
                </div>
            </div>
        </aside>

        <!-- Main Digital Page Reader Section -->
        <section class="lg:col-span-9 flex flex-col gap-4">

            <!-- Control Bar (Voice & Navigation Buttons) -->
            <div class="bg-white dark:bg-gray-900 rounded-2xl p-3 px-4 border border-amber-200/80 dark:border-gray-800 shadow-sm flex flex-wrap items-center justify-between gap-3">
                
                <!-- Dual Voice Audio Engines -->
                <div class="flex flex-wrap items-center gap-2">
                    <button id="btnReadPage" onclick="speakPageText()" class="bg-ghanaGreen hover:bg-emerald-800 text-white font-bold px-3.5 py-2 rounded-xl text-xs sm:text-sm flex items-center gap-2 shadow-sm transition transform active:scale-95">
                        <i class="fa-solid fa-volume-high"></i> <span>🔊 Read Page</span>
                    </button>

                    <button id="btnExplainLesson" onclick="speakExplanation()" class="bg-ghanaGold hover:bg-yellow-500 text-amber-950 font-bold px-3.5 py-2 rounded-xl text-xs sm:text-sm flex items-center gap-2 shadow-sm transition transform active:scale-95">
                        <i class="fa-solid fa-wand-magic-sparkles"></i> <span>💡 Voice Guide</span>
                    </button>

                    <button id="btnStopAudio" onclick="stopSpeech()" class="bg-rose-100 dark:bg-rose-950/50 hover:bg-rose-200 text-rose-700 dark:text-rose-300 font-bold px-3 py-2 rounded-xl text-xs flex items-center gap-1.5 hidden">
                        <i class="fa-solid fa-circle-stop"></i> Stop Speech
                    </button>

                    <span id="audioStatus" class="text-xs text-emerald-700 dark:text-emerald-400 font-bold hidden flex items-center gap-1.5 speaking-animation">
                        <i class="fa-solid fa-waveform"></i> Audio Active...
                    </span>
                </div>

                <!-- Page Jump Nav Controls -->
                <div class="flex items-center gap-2">
                    <button onclick="toggleBookmarkCurrentPage()" title="Bookmark Page" class="w-9 h-9 bg-amber-50 dark:bg-gray-800 text-amber-700 dark:text-amber-400 rounded-xl flex items-center justify-center font-bold hover:bg-amber-100 transition">
                        <i id="bookmarkIconBtn" class="fa-regular fa-bookmark"></i>
                    </button>

                    <button onclick="prevPage()" class="w-9 h-9 bg-gray-100 dark:bg-gray-800 hover:bg-ghanaGreen hover:text-white rounded-xl flex items-center justify-center font-bold text-gray-700 dark:text-gray-200 transition">
                        <i class="fa-solid fa-chevron-left"></i>
                    </button>

                    <span id="pageIndicator" class="text-xs font-bold text-gray-800 dark:text-gray-200 px-2 min-w-[75px] text-center">
                        Page 1 / 210
                    </span>

                    <button onclick="nextPage()" class="w-9 h-9 bg-gray-100 dark:bg-gray-800 hover:bg-ghanaGreen hover:text-white rounded-xl flex items-center justify-center font-bold text-gray-700 dark:text-gray-200 transition">
                        <i class="fa-solid fa-chevron-right"></i>
                    </button>
                </div>
            </div>

            <!-- Interactive Digital Page Book Viewer -->
            <div id="bookContainer" class="bg-paperLight dark:bg-paperDark rounded-3xl border-2 border-amber-200/90 dark:border-gray-800 book-shadow min-h-[660px] p-4 sm:p-8 flex flex-col justify-between relative overflow-hidden">

                <div id="pageMainContent" class="flex-1 flex flex-col justify-between">
                    <div>
                        <!-- Header Strand & Sub-strand Badges -->
                        <div class="flex flex-wrap items-center justify-between gap-2 border-b border-amber-200 dark:border-gray-800 pb-3 mb-4">
                            <div class="flex flex-wrap items-center gap-2">
                                <span id="strandTag" class="bg-ghanaGreen text-white text-[11px] font-bold px-3 py-1 rounded-full uppercase tracking-wide">
                                    STRAND 1: ORAL LANGUAGE
                                </span>
                                <span id="subStrandTag" class="bg-amber-100 dark:bg-amber-950/60 text-amber-900 dark:text-amber-300 border border-amber-300 dark:border-amber-700 text-[11px] font-bold px-3 py-1 rounded-full">
                                    Sub-Strand 6: Greetings
                                </span>
                            </div>
                            <span id="codeStandardTag" class="text-xs font-mono font-bold text-gray-500 dark:text-gray-400 bg-gray-100 dark:bg-gray-800 px-2.5 py-1 rounded-lg">
                                Standard: B1.1.6.1
                            </span>
                        </div>

                        <!-- Page Title -->
                        <h2 id="lessonTitle" class="font-fredoka text-2xl sm:text-3xl font-bold text-gray-900 dark:text-white mb-2">
                            Page Title Loading...
                        </h2>

                        <!-- Ghanaian Heritage Focus Banner -->
                        <div id="culturalContextBanner" class="bg-amber-50 dark:bg-amber-950/30 border-l-4 border-ghanaGold p-3 rounded-r-xl mb-4 text-xs sm:text-sm text-amber-900 dark:text-amber-200 flex items-start gap-3">
                            <i class="fa-solid fa-kaaba text-ghanaGold text-base mt-0.5"></i>
                            <div>
                                <strong class="font-bold">Ghana Heritage & Civic Values:</strong>
                                <span id="culturalContextText">Cultural Heritage Context</span>
                            </div>
                        </div>

                        <!-- TOPIC MULTIMEDIA CANVAS WIDGET (SVG Scene + Animated Canvas Illustration) -->
                        <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-6">
                            
                            <!-- Static SVG Cultural Graphic Frame -->
                            <div class="bg-white dark:bg-gray-900 border border-amber-200 dark:border-gray-800 rounded-2xl p-4 flex flex-col items-center justify-center min-h-[200px] text-center relative overflow-hidden shadow-sm">
                                <div id="svgIllustrationContainer" class="w-full flex items-center justify-center">
                                    <!-- Dynamic SVG Illustration rendered here -->
                                </div>
                                <p id="svgCaption" class="text-[11px] font-bold text-gray-500 dark:text-gray-400 mt-2">Ghanaian Cultural Scene</p>
                            </div>

                            <!-- Animated Interactive Canvas Motion Graphic Widget -->
                            <div class="bg-gray-900 border border-gray-800 rounded-2xl p-4 flex flex-col items-center justify-center min-h-[200px] text-center relative overflow-hidden shadow-sm">
                                <canvas id="topicMotionCanvas" width="300" height="170" class="rounded-xl w-full max-w-[300px] h-[170px] bg-gray-950"></canvas>
                                <div class="flex items-center justify-between w-full mt-2 text-[10px] font-bold text-amber-400">
                                    <span><i class="fa-solid fa-clapperboard"></i> Animated Lesson Graphic</span>
                                    <button onclick="restartMotionWidget()" class="text-white hover:text-ghanaYellow underline">Replay Motion</button>
                                </div>
                            </div>

                        </div>

                        <!-- Lesson Main Text Content Box -->
                        <div id="storyBox" class="prose max-w-none text-gray-800 dark:text-gray-200 text-sm sm:text-base leading-relaxed bg-white/70 dark:bg-gray-900/60 p-4 sm:p-5 rounded-2xl border border-amber-100 dark:border-gray-800 mb-5 shadow-sm">
                            <!-- Story Paragraphs -->
                        </div>

                        <!-- Interactive Tap-to-Pronounce Vocabulary Keywords -->
                        <div class="mb-5 bg-amber-50/50 dark:bg-gray-800/40 border border-amber-200 dark:border-gray-700 p-3.5 rounded-2xl">
                            <p class="text-xs font-bold text-gray-600 dark:text-gray-400 mb-2 flex items-center gap-1.5">
                                <i class="fa-solid fa-spell-check text-ghanaGreen"></i> Key Vocabulary (Tap word to listen):
                            </p>
                            <div id="vocabChipsContainer" class="flex flex-wrap gap-2">
                                <!-- Dynamic Vocab Words -->
                            </div>
                        </div>

                        <!-- Teacher Emican's Explanation Box -->
                        <div id="explanationBox" class="bg-emerald-50 dark:bg-emerald-950/30 border border-emerald-200 dark:border-emerald-800 p-4 rounded-2xl mb-6">
                            <div class="flex items-center gap-2 text-emerald-900 dark:text-emerald-300 font-bold text-sm mb-1">
                                <i class="fa-solid fa-chalkboard-user text-ghanaGreen"></i>
                                <span>Teacher Emican's Lesson Voice Explanation:</span>
                            </div>
                            <p id="explanationText" class="text-xs sm:text-sm text-emerald-950 dark:text-emerald-200 leading-normal">
                                Lesson explanation text.
                            </p>
                        </div>

                        <!-- Interactive Page Exercise & Quiz Box -->
                        <div id="exerciseSection" class="bg-gradient-to-r from-orange-50 to-amber-50 dark:from-gray-800 dark:to-gray-900 border-2 border-dashed border-amber-300 dark:border-gray-700 p-4 sm:p-6 rounded-2xl">
                            <div class="flex items-center justify-between mb-3">
                                <h3 class="font-fredoka font-bold text-base sm:text-lg text-amber-950 dark:text-amber-300 flex items-center gap-2">
                                    <i class="fa-solid fa-pen-ruler text-kenteOrange"></i> Page Exercise & Quick Assessment
                                </h3>
                                <span id="starScoreBadge" class="text-xs font-bold bg-ghanaYellow text-amber-950 px-3 py-1 rounded-full shadow-sm flex items-center gap-1">
                                    <i class="fa-solid fa-star"></i> Stars: <span id="totalStarsCount">0</span>
                                </span>
                            </div>

                            <p id="quizQuestion" class="text-xs sm:text-sm font-bold text-gray-800 dark:text-gray-100 mb-3">
                                Question text...
                            </p>

                            <!-- Options Container -->
                            <div id="quizOptions" class="grid grid-cols-1 sm:grid-cols-2 gap-2.5 mb-3">
                                <!-- Option buttons dynamic -->
                            </div>

                            <!-- Feedback Alert -->
                            <div id="quizFeedback" class="hidden p-3 rounded-xl text-xs font-bold flex items-center justify-between">
                                <span id="feedbackMessage">Correct! Well done child.</span>
                                <span class="text-yellow-500 text-sm flex gap-1">
                                    <i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i><i class="fa-solid fa-star"></i>
                                </span>
                            </div>
                        </div>

                    </div>

                    <!-- Footer Page Info -->
                    <div class="mt-6 pt-4 border-t border-amber-200 dark:border-gray-800 flex items-center justify-between text-xs text-gray-500 dark:text-gray-400 font-bold">
                        <span>Emican Series • Pupil's Book</span>
                        <span id="footerPageNum">Page 1 of 210</span>
                        <span>Ministry of Education, NaCCA</span>
                    </div>
                </div>

            </div>
        </section>
    </main>

    <!-- Bookmarks Modal -->
    <div id="bookmarksModal" class="fixed inset-0 bg-black/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white dark:bg-gray-900 border border-amber-200 dark:border-gray-800 rounded-3xl max-w-md w-full p-5 shadow-2xl flex flex-col max-h-[80vh]">
            <div class="flex items-center justify-between pb-3 border-b border-gray-100 dark:border-gray-800 mb-3">
                <h3 class="font-fredoka font-bold text-lg text-ghanaGreen dark:text-emerald-400 flex items-center gap-2">
                    <i class="fa-solid fa-bookmark text-amber-500"></i> Bookmarked Pages
                </h3>
                <button onclick="toggleBookmarksModal()" class="text-gray-400 hover:text-gray-600 text-lg">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
            <div id="bookmarksList" class="flex-1 overflow-y-auto space-y-2 pr-1">
                <p class="text-xs text-gray-500 text-center py-6">No pages bookmarked yet. Click the bookmark icon on any page to save it here!</p>
            </div>
        </div>
    </div>

    <!-- Application Engine Script -->
    <script>
        // -------------------------------------------------------------
        // CURRICULUM DATABASE: PAGES 1 THROUGH 210 (BASIC 1, 2, AND 3)
        // Includes preliminary pages (Cover, Acknowledgments, Inspiration)
        // -------------------------------------------------------------
        
        const rawPagesData = [
            // PRELIMINARY PAGES
            {
                pageNum: 1,
                volume: "b1",
                strand: "FRONT MATTER",
                subStrand: "Title & Cover",
                standard: "NaCCA-B1",
                title: "Cover & Title Page: Pupil's Book 1",
                culturalContext: "Classroom Scene in Ghana with Teacher and Future Leaders.",
                svgType: "classroom",
                motionType: "welcomeWave",
                story: "EMICAN ENGLISH SERIES • BASIC ONE (PUPIL'S BOOK 1). Aligned with Ministry of Education & NaCCA Standards for Primary Schools in Ghana. Cultivating leadership, reading literacy, and strong community values.",
                vocab: ["English", "Leaders", "Community", "Ghana"],
                explanation: "Welcome to Pupil's Book 1 of the Emican English Series! This book will guide you through listening, speaking, reading, writing, and leadership.",
                quiz: {
                    question: "What is the title of this English textbook series?",
                    options: ["Emican English Series", "Accra Reader", "Primary Reader", "Golden Series"],
                    correct: 0
                }
            },
            {
                pageNum: 2,
                volume: "b1",
                strand: "FRONT MATTER",
                subStrand: "Acknowledgments",
                standard: "NaCCA-B1",
                title: "Acknowledgments",
                culturalContext: "Honoring Parents, Educators, and Educational Supporters in Ghana.",
                svgType: "cultureSymbol",
                motionType: "heartBeat",
                story: "Writing this textbook series has been a journey of dedication to the future of education. I express my deepest gratitude to my parents who ensured I received a strong educational foundation. Special thanks to Author Alice M.C. Bamukunde for her unwavering support and professional guidance, Mr. Alex Yaw Werekuu for believing in this vision, and all Ghanaian educators and NaCCA curriculum specialists.",
                vocab: ["Gratitude", "Foundation", "Guidance", "Education"],
                explanation: "Acknowledging those who support our education teaches us the core value of gratitude and respect.",
                quiz: {
                    question: "What value do we show when thanking people who help us?",
                    options: ["Gratitude and Respect", "Greed", "Anger", "Pride"],
                    correct: 0
                }
            },
            {
                pageNum: 3,
                volume: "b1",
                strand: "FRONT MATTER",
                subStrand: "Inspiration & Philosophy",
                standard: "NaCCA-B1",
                title: "Inspiration: Leadership & Entrepreneurship",
                culturalContext: "Developing CEOs, Entrepreneurs, and Moral Leaders for Ghana.",
                svgType: "leadership",
                motionType: "starBurst",
                story: "Every child deserves a leadership-ready foundation. This series is designed to break the traditional mold. We aim to cultivate CEOs and entrepreneurs who are deeply rooted in the knowledge of their community, guided by strong morals, and literate in the laws that govern a just society.",
                vocab: ["Leadership", "Entrepreneur", "Morals", "Innovate"],
                explanation: "Education is not just about getting a job; it is about becoming a creative leader and solving problems for your country.",
                quiz: {
                    question: "According to the inspiration page, what kind of foundation should children receive?",
                    options: ["Leadership-ready foundation", "Lazy foundation", "Fearful foundation", "No foundation"],
                    correct: 0
                }
            },
            {
                pageNum: 4,
                volume: "b1",
                strand: "FRONT MATTER",
                subStrand: "Table of Contents",
                standard: "NaCCA-B1",
                title: "Table of Contents (Basic 1)",
                culturalContext: "Overview of Basic 1 English Curriculum Strands.",
                svgType: "tocIcon",
                motionType: "listScroll",
                story: "Strand 1: Oral Language (Songs, Greetings, Manners, Ananse Stories) • Strand 2: Reading & Phonics (-at, -an word families) • Strand 4: Writing & Labelling • Strand 5: Grammar & Prepositions • Strand 6: Extensive Reading.",
                vocab: ["Strand", "Phonics", "Grammar", "Listening"],
                explanation: "The table of contents lists all topics so you can easily jump to any lesson in your book.",
                quiz: {
                    question: "How many main language skills are developed in the English curriculum?",
                    options: ["4 Skills (Listening, Speaking, Reading, Writing)", "1 Skill", "8 Skills", "No skills"],
                    correct: 0
                }
            }
        ];

        // DYNAMICALLY GENERATE PAGES 5 THROUGH 210 SYSTEMATICALLY
        // Covering Basic 1 (5-70), Basic 2 (71-140), Basic 3 (141-210)
        
        const strandTopics = [
            { strand: "STRAND 1: ORAL LANGUAGE", sub: "Greetings & Manners", std: "B1.1.6.1", type: "greetings" },
            { strand: "STRAND 1: ORAL LANGUAGE", sub: "Songs & Rhymes", std: "B1.1.2.1", type: "rhyme" },
            { strand: "STRAND 1: ORAL LANGUAGE", sub: "Ananse Folklore", std: "B1.1.4.1", type: "ananse" },
            { strand: "STRAND 2: READING", sub: "Phonics & Letter Sounds", std: "B1.2.2.1", type: "phonics" },
            { strand: "STRAND 2: READING", sub: "Digraphs & Blends", std: "B2.2.3.1", type: "digraph" },
            { strand: "STRAND 4: WRITING", sub: "Penmanship & Labelling", std: "B1.4.4.1", type: "writing" },
            { strand: "STRAND 4: WRITING", sub: "Road Safety & Traffic Lights", std: "B2.4.5.1", type: "traffic" },
            { strand: "STRAND 5: GRAMMAR", sub: "Action Verbs & Tenses", std: "B2.5.4.1", type: "verbs" },
            { strand: "STRAND 5: GRAMMAR", sub: "Prepositions of Position", std: "B1.5.7.1", type: "preposition" },
            { strand: "STRAND 5: GRAMMAR", sub: "Civic Infrastructure & Government", std: "B3.4.10.1", type: "civics" }
        ];

        const ghanaPlaces = ["Cape Coast", "Kumasi", "Accra", "Tamale", "Sunyani", "Ho", "Bolgatanga", "Koforidua", "Wa", "Takoradi"];

        for (let p = 5; p <= 210; p++) {
            let vol = p <= 70 ? "b1" : (p <= 140 ? "b2" : "b3");
            let gradeLabel = p <= 70 ? "Basic 1" : (p <= 140 ? "Basic 2" : "Basic 3");
            let topicObj = strandTopics[(p - 5) % strandTopics.length];
            let place = ghanaPlaces[(p - 5) % ghanaPlaces.length];

            let title = "";
            let storyText = "";
            let explanation = "";
            let question = "";
            let options = [];
            let correct = 0;
            let vocab = [];

            if (topicObj.type === "greetings") {
                title = `Morning Greetings in ${place} (${gradeLabel})`;
                storyText = `Kofi and Aba walked through the morning market in ${place}. Kofi greeted the elders politely: 'Good morning, Elders!' The elders smiled and blessed the children. Respectful greetings build peace in our Ghanaian community.`;
                explanation = "Always greet elders and friends warmly in the morning before starting your conversation.";
                question = "What should you say when greeting someone in the morning?";
                options = ["Good morning", "Good night", "Go away", "Quiet"];
                correct = 0;
                vocab = ["Greeting", "Respect", "Community", "Peace"];
            } else if (topicObj.type === "traffic") {
                title = `Traffic Lights & Road Safety in ${place}`;
                storyText = `Yaw reached the busy road in ${place}. He watched the traffic light carefully. RED means STOP. YELLOW means GET READY. GREEN means GO. Yaw looked left, right, and left again before stepping onto the zebra crossing safely.`;
                explanation = "Obey traffic lights and always use zebra crossings when crossing streets with cars.";
                question = "What does the RED traffic light tell drivers and pedestrians?";
                options = ["Stop immediately!", "Drive fast", "Dance", "Turn off light"];
                correct = 0;
                vocab = ["Traffic Light", "Red Light", "Safety", "Zebra Crossing"];
            } else if (topicObj.type === "ananse") {
                title = `Kwaku Ananse & The Wisdom Pot (${gradeLabel})`;
                storyText = `Kwaku Ananse tried to collect all the world's wisdom into a clay pot in ${place}. He tied the pot to his stomach and tried to climb a tall Baobab tree. But his son Ntikuma said: 'Father, tie the pot to your back instead!' Ananse realized that wisdom belongs to everyone!`;
                explanation = "Nobody knows everything. Wisdom is shared among all members of the community.";
                question = "What lesson did Kwaku Ananse learn from his son Ntikuma?";
                options = ["Wisdom belongs to everyone", "Hide all food", "Climb trees fast", "Don't talk"];
                correct = 0;
                vocab = ["Wisdom", "Ananse", "Baobab", "Sharing"];
            } else if (topicObj.type === "phonics") {
                title = `Phonics Sound Blends & Words (Page ${p})`;
                storyText = `Listen carefully to the initial letter sounds: /b/ as in Bag, /c/ as in Cat, /m/ as in Mango in ${place}. Let us blend /a/ and /t/ to form 'AT'. B + AT = BAT. M + AT = MAT.`;
                explanation = "Blending sounds together helps us decode unknown words when reading books.";
                question = "Which sound is heard at the start of 'Mango'?";
                options = ["/m/", "/b/", "/t/", "/s/"];
                correct = 0;
                vocab = ["Phonics", "Blend", "Sound", "Letters"];
            } else if (topicObj.type === "civics") {
                title = `Government Roads & Public Property in ${place}`;
                storyText = `The Government of Ghana builds tarred roads, public hospitals, solar streetlights, and schools in ${place}. As patriotic pupils, we must protect public property, avoid littering, and obey government laws.`;
                explanation = "Government services belong to all citizens. Taking care of public property shows patriotism.";
                question = "Who builds public roads and schools for the country?";
                options = ["The Government", "Foreign tourists", "Ananse", "Nobody"];
                correct = 0;
                vocab = ["Government", "Patriotism", "Infrastructure", "Roads"];
            } else {
                title = `English Mastery Lesson - Page ${p} (${gradeLabel})`;
                storyText = `In this lesson at ${place}, pupils practice speaking clearly, spelling key vocabulary words accurately, and using correct action verbs in sentences. Practice makes perfect in English literacy!`;
                explanation = "Read your text aloud every day to build reading speed and confidence.";
                question = "Why do we read aloud every day?";
                options = ["To build reading speed and fluency", "To make noise", "To sleep", "To forget words"];
                correct = 0;
                vocab = ["Literacy", "Fluency", "Practice", "Vocabulary"];
            }

            rawPagesData.push({
                pageNum: p,
                volume: vol,
                strand: topicObj.strand,
                subStrand: topicObj.sub,
                standard: `${topicObj.std}.${p % 4 + 1}`,
                title: title,
                culturalContext: `Ghanaian Heritage Context in ${place}.`,
                svgType: topicObj.type,
                motionType: topicObj.type,
                story: storyText,
                vocab: vocab,
                explanation: explanation,
                quiz: {
                    question: question,
                    options: options,
                    correct: correct
                }
            });
        }

        // APPLICATION STATE
        let currentBookVolume = 'b1';
        let currentPageIndex = 0; // index in rawPagesData
        let isDarkMode = false;
        let bookmarks = [];
        let totalStars = 0;
        let isSpeaking = false;
        let currentUtterance = null;
        let motionAnimId = null;

        // DOM ELEMENTS
        const bookVolumeSelect = document.getElementById('bookVolumeSelect');
        const tocList = document.getElementById('tocList');
        const tocSearch = document.getElementById('tocSearch');
        const pageSlider = document.getElementById('pageSlider');
        const pageInput = document.getElementById('pageInput');
        const jumperLabel = document.getElementById('jumperLabel');
        const currentPageBadge = document.getElementById('currentPageBadge');

        const strandTag = document.getElementById('strandTag');
        const subStrandTag = document.getElementById('subStrandTag');
        const codeStandardTag = document.getElementById('codeStandardTag');
        const lessonTitle = document.getElementById('lessonTitle');
        const culturalContextText = document.getElementById('culturalContextText');
        const svgIllustrationContainer = document.getElementById('svgIllustrationContainer');
        const svgCaption = document.getElementById('svgCaption');
        const storyBox = document.getElementById('storyBox');
        const vocabChipsContainer = document.getElementById('vocabChipsContainer');
        const explanationText = document.getElementById('explanationText');

        const quizQuestion = document.getElementById('quizQuestion');
        const quizOptions = document.getElementById('quizOptions');
        const quizFeedback = document.getElementById('quizFeedback');
        const feedbackMessage = document.getElementById('feedbackMessage');
        const totalStarsCount = document.getElementById('totalStarsCount');

        const pageIndicator = document.getElementById('pageIndicator');
        const footerPageNum = document.getElementById('footerPageNum');
        const progressBar = document.getElementById('progressBar');
        const progressPercent = document.getElementById('progressPercent');
        const bookmarkIconBtn = document.getElementById('bookmarkIconBtn');
        const audioStatus = document.getElementById('audioStatus');
        const btnStopAudio = document.getElementById('btnStopAudio');

        // INITIALIZATION
        window.onload = function() {
            renderTOC();
            loadPageData(0);
            setupSearch();
        };

        // RENDER TOC INDEX (200+ PAGES)
        function renderTOC() {
            tocList.innerHTML = '';
            rawPagesData.forEach((page, idx) => {
                // Filter TOC based on selected Volume or show all
                const isSelected = currentPageIndex === idx;
                const btn = document.createElement('button');
                btn.className = `w-full text-left p-2 rounded-xl text-xs transition flex flex-col gap-0.5 ${isSelected ? 'bg-amber-200/90 dark:bg-amber-900/60 text-amber-950 dark:text-amber-200 font-bold border-l-4 border-ghanaGreen shadow-sm' : 'hover:bg-amber-50 dark:hover:bg-gray-800 text-gray-700 dark:text-gray-300'}`;
                btn.innerHTML = `
                    <div class="flex items-center justify-between w-full">
                        <span class="font-bold text-gray-900 dark:text-gray-100 truncate max-w-[170px]">${page.pageNum}. ${page.title}</span>
                        <span class="text-[9px] font-bold text-emerald-800 dark:text-emerald-300 bg-emerald-100 dark:bg-emerald-950 px-1.5 py-0.5 rounded">P. ${page.pageNum}</span>
                    </div>
                    <span class="text-[10px] text-gray-500 dark:text-gray-400 truncate">${page.subStrand}</span>
                `;
                btn.onclick = () => {
                    stopSpeech();
                    loadPageData(idx);
                };
                tocList.appendChild(btn);
            });
        }

        function setupSearch() {
            tocSearch.addEventListener('input', (e) => {
                const query = e.target.value.toLowerCase();
                const buttons = tocList.querySelectorAll('button');
                buttons.forEach((btn) => {
                    const text = btn.innerText.toLowerCase();
                    btn.style.display = text.includes(query) ? 'flex' : 'none';
                });
            });
        }

        // PAGE JUMPER CONTROLS
        function onSliderChange(val) {
            let targetPage = parseInt(val);
            jumpToPageNumber(targetPage);
        }

        function onNumberInput(val) {
            let targetPage = parseInt(val);
            if (isNaN(targetPage)) targetPage = 1;
            if (targetPage < 1) targetPage = 1;
            if (targetPage > 210) targetPage = 210;
            jumpToPageNumber(targetPage);
        }

        function jumpToPageNumber(pageNum) {
            const idx = rawPagesData.findIndex(p => p.pageNum === pageNum);
            if (idx !== -1) {
                stopSpeech();
                loadPageData(idx);
            }
        }

        function changeBookVolume(volKey) {
            currentBookVolume = volKey;
            let targetPage = 1;
            if (volKey === 'b2') targetPage = 71;
            if (volKey === 'b3') targetPage = 141;
            jumpToPageNumber(targetPage);
        }

        // LOAD PAGE CONTENT DATA
        function loadPageData(idx) {
            currentPageIndex = idx;
            const page = rawPagesData[idx];

            // Update Volume Selector if needed
            if (page.pageNum <= 70) bookVolumeSelect.value = 'b1';
            else if (page.pageNum <= 140) bookVolumeSelect.value = 'b2';
            else bookVolumeSelect.value = 'b3';

            // Sync Jumper
            pageSlider.value = page.pageNum;
            pageInput.value = page.pageNum;
            jumperLabel.innerText = `Page ${page.pageNum}`;
            currentPageBadge.innerText = `Page ${page.pageNum} / 210`;

            // Tags & Titles
            strandTag.innerText = page.strand;
            subStrandTag.innerText = page.subStrand;
            codeStandardTag.innerText = `Standard: ${page.standard}`;
            lessonTitle.innerText = page.title;
            culturalContextText.innerText = page.culturalContext;

            // Render SVG Illustration
            renderSVGIllustration(page.svgType);
            svgCaption.innerText = `Ghanaian Illustration: ${page.title}`;

            // Render Animated Motion Widget Canvas
            startMotionWidget(page.motionType);

            // Render Story
            storyBox.innerHTML = `<p class="leading-relaxed font-medium">${page.story}</p>`;

            // Render Vocabulary Chips
            vocabChipsContainer.innerHTML = '';
            page.vocab.forEach(word => {
                const chip = document.createElement('button');
                chip.className = "bg-white dark:bg-gray-800 border border-amber-300 dark:border-gray-600 hover:border-ghanaGreen text-gray-800 dark:text-gray-200 text-xs font-bold px-3 py-1 rounded-full shadow-sm flex items-center gap-1.5 transition active:scale-95";
                chip.innerHTML = `<i class="fa-solid fa-volume-low text-ghanaGreen"></i> ${word}`;
                chip.onclick = () => speakWord(word);
                vocabChipsContainer.appendChild(chip);
            });

            // Teacher Explanation
            explanationText.innerText = page.explanation;

            // Quiz Section
            quizQuestion.innerText = `Page Question: ${page.quiz.question}`;
            quizOptions.innerHTML = '';
            quizFeedback.classList.add('hidden');

            page.quiz.options.forEach((opt, oIdx) => {
                const optBtn = document.createElement('button');
                optBtn.className = "w-full text-left bg-white dark:bg-gray-800 border border-amber-200 dark:border-gray-700 hover:border-ghanaGreen hover:bg-emerald-50 dark:hover:bg-emerald-950 text-gray-800 dark:text-gray-100 text-xs sm:text-sm font-semibold p-3 rounded-xl transition shadow-sm flex items-center justify-between";
                optBtn.innerHTML = `<span>${opt}</span> <i class="fa-regular fa-circle text-gray-300"></i>`;
                optBtn.onclick = () => checkQuizAnswer(oIdx, page.quiz.correct, optBtn);
                quizOptions.appendChild(optBtn);
            });

            // Page Indicators
            pageIndicator.innerText = `Page ${page.pageNum} / 210`;
            footerPageNum.innerText = `Page ${page.pageNum} of 210`;

            // Bookmark Button State
            updateBookmarkBtn();

            // Progress Bar
            const percent = Math.round(((currentPageIndex + 1) / rawPagesData.length) * 100);
            progressBar.style.width = `${percent}%`;
            progressPercent.innerText = `${percent}%`;

            renderTOC();
        }

        // SVG ILLUSTRATION GENERATOR
        function renderSVGIllustration(type) {
            let svgHtml = '';
            if (type === 'traffic') {
                svgHtml = `
                <svg width="180" height="150" viewBox="0 0 200 160" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <rect x="75" y="10" width="50" height="130" rx="10" fill="#1E293B" stroke="#FCD116" stroke-width="3"/>
                    <circle cx="100" cy="35" r="16" fill="#CE1126"/>
                    <circle cx="100" cy="75" r="16" fill="#FCD116"/>
                    <circle cx="100" cy="115" r="16" fill="#006B3F"/>
                </svg>`;
            } else if (type === 'ananse') {
                svgHtml = `
                <svg width="180" height="150" viewBox="0 0 200 160" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M100 20 L150 140 L50 140 Z" fill="#D4AF37" opacity="0.3"/>
                    <circle cx="100" cy="70" r="25" fill="#E65100"/>
                    <circle cx="100" cy="50" r="15" fill="#334155"/>
                    <path d="M70 50 Q40 30 30 60 M130 50 Q160 30 170 60" stroke="#334155" stroke-width="4" fill="none"/>
                    <path d="M70 70 Q40 70 30 100 M130 70 Q160 70 170 100" stroke="#334155" stroke-width="4" fill="none"/>
                </svg>`;
            } else if (type === 'greetings') {
                svgHtml = `
                <svg width="180" height="150" viewBox="0 0 200 160" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <circle cx="100" cy="50" r="35" fill="#FCD116"/>
                    <path d="M20 140 Q100 80 180 140" fill="#006B3F"/>
                    <circle cx="70" cy="100" r="12" fill="#E65100"/>
                    <circle cx="130" cy="100" r="12" fill="#0D47A1"/>
                </svg>`;
            } else {
                svgHtml = `
                <svg width="180" height="150" viewBox="0 0 200 160" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <rect x="20" y="20" width="160" height="120" rx="12" fill="#006B3F" stroke="#FCD116" stroke-width="4"/>
                    <path d="M40 60 L160 60 M40 100 L160 100" stroke="#FFFFFF" stroke-width="3" stroke-dasharray="8 8"/>
                    <text x="100" y="45" fill="#FCD116" font-size="14" font-weight="bold" text-anchor="middle">EMICAN GHANA</text>
                </svg>`;
            }
            svgIllustrationContainer.innerHTML = svgHtml;
        }

        // CANVAS ANIMATED MOTION GRAPHIC WIDGET
        function startMotionWidget(type) {
            if (motionAnimId) cancelAnimationFrame(motionAnimId);
            const canvas = document.getElementById('topicMotionCanvas');
            const ctx = canvas.getContext('2d');
            let frame = 0;

            function animate() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                frame++;

                if (type === 'traffic') {
                    // Traffic light cycle
                    ctx.fillStyle = '#1E293B';
                    ctx.fillRect(125, 20, 50, 130);

                    // Red light blink
                    ctx.fillStyle = (frame % 90 < 30) ? '#CE1126' : '#450a0a';
                    ctx.beginPath(); ctx.arc(150, 45, 12, 0, Math.PI * 2); ctx.fill();

                    // Yellow light blink
                    ctx.fillStyle = (frame % 90 >= 30 && frame % 90 < 60) ? '#FCD116' : '#422006';
                    ctx.beginPath(); ctx.arc(150, 85, 12, 0, Math.PI * 2); ctx.fill();

                    // Green light blink
                    ctx.fillStyle = (frame % 90 >= 60) ? '#006B3F' : '#064e3b';
                    ctx.beginPath(); ctx.arc(150, 125, 12, 0, Math.PI * 2); ctx.fill();

                    // Moving car
                    let carX = (frame * 2) % 220 - 40;
                    ctx.fillStyle = '#E65100';
                    ctx.fillRect(carX, 120, 40, 20);
                    ctx.fillStyle = '#FFFFFF';
                    ctx.beginPath(); ctx.arc(carX + 10, 140, 5, 0, Math.PI*2); ctx.fill();
                    ctx.beginPath(); ctx.arc(carX + 30, 140, 5, 0, Math.PI*2); ctx.fill();
                } else if (type === 'phonics') {
                    // Phonics wave effect
                    ctx.fillStyle = '#006B3F';
                    ctx.font = '22px Fredoka';
                    ctx.fillText('/a/  /b/  /c/  /m/', 40, 50);

                    for (let i = 0; i < 5; i++) {
                        let h = Math.sin((frame + i * 15) * 0.1) * 30 + 40;
                        ctx.fillStyle = '#FCD116';
                        ctx.fillRect(40 + i * 45, 130 - h, 20, h);
                    }
                } else {
                    // Default Ghanaian Star & Wave animation
                    let scale = 1 + Math.sin(frame * 0.05) * 0.15;
                    ctx.save();
                    ctx.translate(150, 85);
                    ctx.scale(scale, scale);
                    ctx.fillStyle = '#FCD116';
                    ctx.font = '40px FontAwesome';
                    ctx.textAlign = 'center';
                    ctx.textBaseline = 'middle';
                    ctx.fillText('★', 0, 0);
                    ctx.restore();

                    ctx.fillStyle = '#006B3F';
                    ctx.font = '12px Quicksand';
                    ctx.fillText('Emican Interactive Motion', 80, 155);
                }

                motionAnimId = requestAnimationFrame(animate);
            }
            animate();
        }

        function restartMotionWidget() {
            const page = rawPagesData[currentPageIndex];
            startMotionWidget(page.motionType);
        }

        // QUIZ GRADING & STARS
        function checkQuizAnswer(selectedIdx, correctIdx, btnEl) {
            const allBtns = quizOptions.querySelectorAll('button');
            allBtns.forEach(b => b.disabled = true);

            quizFeedback.classList.remove('hidden');

            if (selectedIdx === correctIdx) {
                btnEl.className = "w-full text-left bg-emerald-100 dark:bg-emerald-950 border-2 border-ghanaGreen text-emerald-950 dark:text-emerald-200 font-bold p-3 rounded-xl shadow-sm flex items-center justify-between";
                btnEl.querySelector('i').className = "fa-solid fa-circle-check text-ghanaGreen text-lg";

                quizFeedback.className = "p-3 rounded-xl text-xs font-bold bg-emerald-100 dark:bg-emerald-950/80 text-emerald-900 dark:text-emerald-200 border border-emerald-300 flex items-center justify-between";
                feedbackMessage.innerHTML = `<i class="fa-solid fa-face-smile text-ghanaGreen"></i> Correct answer! You earned +3 Star Points. Ayekoo!`;

                totalStars += 3;
                totalStarsCount.innerText = totalStars;
                playSimpleTone(600, 900);
            } else {
                btnEl.className = "w-full text-left bg-rose-100 dark:bg-rose-950/80 border-2 border-ghanaRed text-rose-950 dark:text-rose-200 font-bold p-3 rounded-xl shadow-sm flex items-center justify-between";
                btnEl.querySelector('i').className = "fa-solid fa-circle-xmark text-ghanaRed text-lg";

                allBtns[correctIdx].className = "w-full text-left bg-emerald-50 dark:bg-emerald-950/40 border-2 border-emerald-400 text-emerald-900 dark:text-emerald-300 font-bold p-3 rounded-xl flex items-center justify-between";

                quizFeedback.className = "p-3 rounded-xl text-xs font-bold bg-rose-50 dark:bg-rose-950/60 text-rose-900 dark:text-rose-200 border border-rose-200 flex items-center justify-between";
                feedbackMessage.innerHTML = `<i class="fa-solid fa-circle-info text-ghanaRed"></i> Incorrect option. Review the page text and try again!`;
                playSimpleTone(300, 200);
            }
        }

        // NAVIGATION BUTTONS
        function nextPage() {
            if (currentPageIndex < rawPagesData.length - 1) {
                stopSpeech();
                loadPageData(currentPageIndex + 1);
            }
        }

        function prevPage() {
            if (currentPageIndex > 0) {
                stopSpeech();
                loadPageData(currentPageIndex - 1);
            }
        }

        // BOOKMARKS
        function toggleBookmarkCurrentPage() {
            const pageNum = rawPagesData[currentPageIndex].pageNum;
            const bIdx = bookmarks.indexOf(pageNum);
            if (bIdx === -1) {
                bookmarks.push(pageNum);
            } else {
                bookmarks.splice(bIdx, 1);
            }
            updateBookmarkBtn();
            renderBookmarksList();
        }

        function updateBookmarkBtn() {
            const pageNum = rawPagesData[currentPageIndex].pageNum;
            const isBookmarked = bookmarks.includes(pageNum);
            if (isBookmarked) {
                bookmarkIconBtn.className = "fa-solid fa-bookmark text-amber-500";
            } else {
                bookmarkIconBtn.className = "fa-regular fa-bookmark";
            }
            document.getElementById('bookmarkBadge').innerText = bookmarks.length;
        }

        function renderBookmarksList() {
            const container = document.getElementById('bookmarksList');
            if (bookmarks.length === 0) {
                container.innerHTML = `<p class="text-xs text-gray-500 text-center py-6">No pages bookmarked yet.</p>`;
                return;
            }
            container.innerHTML = '';
            bookmarks.forEach(pNum => {
                const pObj = rawPagesData.find(p => p.pageNum === pNum);
                const item = document.createElement('div');
                item.className = "bg-amber-50 dark:bg-gray-800 p-2.5 rounded-xl border border-amber-200 dark:border-gray-700 flex items-center justify-between text-xs";
                item.innerHTML = `
                    <div>
                        <strong class="text-gray-900 dark:text-gray-100">Page ${pNum}: ${pObj ? pObj.title : ''}</strong>
                    </div>
                    <button onclick="jumpToPageNumber(${pNum}); toggleBookmarksModal();" class="bg-ghanaGreen text-white px-2.5 py-1 rounded-lg font-bold">Jump</button>
                `;
                container.appendChild(item);
            });
        }

        function toggleBookmarksModal() {
            const modal = document.getElementById('bookmarksModal');
            modal.classList.toggle('hidden');
        }

        function toggleDarkMode() {
            isDarkMode = !isDarkMode;
            document.documentElement.classList.toggle('dark', isDarkMode);
        }

        // AUDIO SPEECH SYNTHESIS
        function speakPageText() {
            const page = rawPagesData[currentPageIndex];
            speakText(`Page ${page.pageNum}. ${page.title}. ${page.story}`);
        }

        function speakExplanation() {
            const page = rawPagesData[currentPageIndex];
            speakText(`Teacher Emican Explanation: ${page.explanation}`, 0.95);
        }

        function speakWord(word) {
            speakText(word, 1.0);
        }

        function speakText(text, rate = 1.0) {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
                currentUtterance = new SpeechSynthesisUtterance(text);
                currentUtterance.rate = rate;

                currentUtterance.onstart = () => {
                    isSpeaking = true;
                    audioStatus.classList.remove('hidden');
                    btnStopAudio.classList.remove('hidden');
                };

                currentUtterance.onend = () => {
                    isSpeaking = false;
                    audioStatus.classList.add('hidden');
                    btnStopAudio.classList.add('hidden');
                };

                currentUtterance.onerror = () => {
                    isSpeaking = false;
                    audioStatus.classList.add('hidden');
                    btnStopAudio.classList.add('hidden');
                };

                window.speechSynthesis.speak(currentUtterance);
            }
        }

        function stopSpeech() {
            if ('speechSynthesis' in window) {
                window.speechSynthesis.cancel();
                isSpeaking = false;
                audioStatus.classList.add('hidden');
                btnStopAudio.classList.add('hidden');
            }
        }

        function playSimpleTone(freq1, freq2) {
            try {
                const ctx = new (window.AudioContext || window.webkitAudioContext)();
                const osc = ctx.createOscillator();
                const gain = ctx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(freq1, ctx.currentTime);
                osc.frequency.exponentialRampToValueAtTime(freq2, ctx.currentTime + 0.2);
                gain.gain.setValueAtTime(0.1, ctx.currentTime);
                gain.gain.exponentialRampToValueAtTime(0.01, ctx.currentTime + 0.3);
                osc.connect(gain);
                gain.connect(ctx.destination);
                osc.start();
                osc.stop(ctx.currentTime + 0.3);
            } catch(e) {}
        }
    </script>
</body>
</html>
