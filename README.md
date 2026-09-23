<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Quiz Game Teknologi & AI SMP</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;600;700;800&display=swap" rel="stylesheet">
    <!-- Canvas Confetti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                    }
                }
            }
        }
    </script>
    <style>
        .custom-scrollbar::-webkit-scrollbar {
            width: 6px;
        }
        .custom-scrollbar::-webkit-scrollbar-track {
            background: #1e293b;
        }
        .custom-scrollbar::-webkit-scrollbar-thumb {
            background: #475569;
            border-radius: 4px;
        }
        @keyframes pulse-ring {
            0% { transform: scale(0.98); opacity: 1; }
            50% { transform: scale(1.02); opacity: 0.8; }
            100% { transform: scale(0.98); opacity: 1; }
        }
        .timer-warning {
            animation: pulse-ring 0.8s infinite ease-in-out;
        }
    </style>
</head>
<body class="bg-slate-900 text-slate-100 font-sans min-h-screen flex flex-col justify-between relative overflow-x-hidden select-none">

    <!-- Latar Belakang Dekorasi -->
    <div class="fixed inset-0 pointer-events-none opacity-20">
        <div class="absolute -top-24 -left-24 w-96 h-96 bg-blue-500 rounded-full filter blur-3xl"></div>
        <div class="absolute top-1/2 -right-24 w-96 h-96 bg-purple-500 rounded-full filter blur-3xl"></div>
        <div class="absolute -bottom-24 left-1/3 w-96 h-96 bg-indigo-500 rounded-full filter blur-3xl"></div>
    </div>

    <!-- Header -->
    <header class="relative z-10 w-full border-b border-slate-800 bg-slate-900/80 backdrop-blur-md px-4 py-3">
        <div class="max-w-4xl mx-auto flex justify-between items-center">
            <div class="flex items-center space-x-3">
                <div class="bg-gradient-to-tr from-blue-600 to-indigo-500 p-2.5 rounded-xl text-white shadow-lg shadow-blue-500/20">
                    <i class="fa-solid fa-robot text-xl"></i>
                </div>
                <div>
                    <h1 class="font-extrabold text-lg md:text-xl bg-gradient-to-r from-blue-400 to-indigo-300 bg-clip-text text-transparent">AI & Tech Quest</h1>
                    <p class="text-xs text-slate-400 font-medium">Game Kuis Teknologi SMP</p>
                </div>
            </div>
            <button id="soundToggleBtn" class="px-3 py-2 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-300 border border-slate-700 text-sm transition flex items-center gap-2 cursor-pointer">
                <i class="fa-solid fa-volume-high text-blue-400" id="soundIcon"></i>
                <span class="hidden sm:inline font-semibold">Suara</span>
            </button>
        </div>
    </header>

    <!-- Main Content -->
    <main class="relative z-10 flex-1 max-w-4xl w-full mx-auto p-4 flex flex-col justify-center my-auto">
        
        <!-- HALAMAN 1: HALAMAN AWAL / START -->
        <div id="startScreen" class="bg-slate-800/90 border border-slate-700/60 rounded-3xl p-6 md:p-10 shadow-2xl backdrop-blur-xl text-center">
            <div class="w-20 h-20 bg-blue-500/10 text-blue-400 border border-blue-500/30 rounded-3xl flex items-center justify-center mx-auto mb-6 text-3xl shadow-inner">
                <i class="fa-solid fa-brain"></i>
            </div>
            <h2 class="text-2xl md:text-4xl font-extrabold text-white mb-3">Tantangan Teknologi & AI</h2>
            <p class="text-slate-400 max-w-md mx-auto text-sm md:text-base mb-8">
                Uji pengetahuanmu seputar AI, Komputer, Internet, dan Keamanan Siber. Jawab 35 pertanyaan dan raih skor tertinggi!
            </p>

            <div class="grid grid-cols-2 md:grid-cols-4 gap-3 max-w-lg mx-auto mb-8">
                <div class="bg-slate-900/60 p-3 rounded-2xl border border-slate-800">
                    <div class="text-blue-400 text-xs font-semibold mb-1"><i class="fa-solid fa-list-check"></i> Soal</div>
                    <div class="text-lg font-bold text-white">35 Soal</div>
                </div>
                <div class="bg-slate-900/60 p-3 rounded-2xl border border-slate-800">
                    <div class="text-amber-400 text-xs font-semibold mb-1"><i class="fa-solid fa-clock"></i> Waktu</div>
                    <div class="text-lg font-bold text-white">20 Detik/Soal</div>
                </div>
                <div class="bg-slate-900/60 p-3 rounded-2xl border border-slate-800">
                    <div class="text-emerald-400 text-xs font-semibold mb-1"><i class="fa-solid fa-bolt"></i> Bonus</div>
                    <div class="text-lg font-bold text-white">Streak Multiplier</div>
                </div>
                <div class="bg-slate-900/60 p-3 rounded-2xl border border-slate-800">
                    <div class="text-rose-400 text-xs font-semibold mb-1"><i class="fa-solid fa-heart"></i> Nyawa</div>
                    <div class="text-lg font-bold text-white">3 Kesempatan</div>
                </div>
            </div>

            <div class="flex flex-col sm:flex-row gap-3 justify-center items-center">
                <button id="startQuizBtn" class="w-full sm:w-auto px-8 py-4 rounded-2xl bg-gradient-to-r from-blue-600 to-indigo-600 hover:from-blue-500 hover:to-indigo-500 text-white font-bold text-lg shadow-xl shadow-blue-600/30 transition transform hover:-translate-y-0.5 active:translate-y-0 cursor-pointer">
                    <i class="fa-solid fa-play mr-2"></i> Mulai Bermain
                </button>
                <button id="shareStartWaBtn" class="w-full sm:w-auto px-6 py-4 rounded-2xl bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-base shadow-lg shadow-emerald-600/20 transition cursor-pointer">
                    <i class="fa-brands fa-whatsapp mr-2"></i> Bagikan Game
                </button>
            </div>
        </div>

        <!-- HALAMAN 2: GAMEPLAY KUIS -->
        <div id="quizScreen" class="hidden flex-col gap-4">
            
            <!-- Dashboard Game Status -->
            <div class="bg-slate-800/90 border border-slate-700/60 rounded-2xl p-4 flex justify-between items-center gap-3 shadow-lg">
                <div class="flex items-center gap-4">
                    <div class="flex flex-col">
                        <span class="text-xs text-slate-400 font-semibold uppercase tracking-wider">Soal Ke</span>
                        <span class="text-lg font-extrabold text-blue-400"><span id="currentQuestionNum">1</span><span class="text-slate-500 text-sm">/35</span></span>
                    </div>
                </div>

                <!-- Nyawa / Hearts -->
                <div class="flex items-center gap-1.5 bg-slate-900/80 px-3 py-1.5 rounded-xl border border-slate-800" id="livesContainer">
                    <i class="fa-solid fa-heart text-rose-500 text-base"></i>
                    <i class="fa-solid fa-heart text-rose-500 text-base"></i>
                    <i class="fa-solid fa-heart text-rose-500 text-base"></i>
                </div>

                <!-- Streak Multiplier -->
                <div class="hidden sm:flex items-center gap-2 bg-amber-500/10 border border-amber-500/20 px-3 py-1.5 rounded-xl">
                    <i class="fa-solid fa-fire text-amber-400"></i>
                    <span class="text-xs font-bold text-amber-300">Streak: <span id="streakCount">0</span>x</span>
                </div>

                <!-- Skor -->
                <div class="flex flex-col text-right">
                    <span class="text-xs text-slate-400 font-semibold uppercase tracking-wider">Skor</span>
                    <span class="text-xl font-black text-amber-400" id="scoreDisplay">0</span>
                </div>
            </div>

            <!-- Timer Progress Bar -->
            <div class="w-full bg-slate-800 h-3 rounded-full overflow-hidden p-0.5 border border-slate-700/50">
                <div id="timerBar" class="h-full bg-gradient-to-r from-blue-500 to-indigo-500 rounded-full transition-all duration-1000 ease-linear w-full"></div>
            </div>

            <!-- Kartu Pertanyaan -->
            <div class="bg-slate-800/90 border border-slate-700/60 rounded-3xl p-6 md:p-8 shadow-2xl backdrop-blur-xl relative">
                <div class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-blue-500/10 border border-blue-500/20 text-blue-400 text-xs font-semibold mb-4">
                    <i class="fa-solid fa-lightbulb"></i> Soal Teknologi SMP
                </div>

                <h3 id="questionText" class="text-lg md:text-2xl font-bold text-white mb-6 leading-relaxed">
                    Memuat pertanyaan...
                </h3>

                <!-- Pilihan Jawaban -->
                <div id="optionsContainer" class="grid grid-cols-1 md:grid-cols-2 gap-3.5">
                    <!-- Tombol Opsi dimasukkan via JS -->
                </div>
            </div>

            <div class="flex justify-between items-center text-xs text-slate-400 px-2">
                <span><i class="fa-solid fa-info-circle mr-1"></i> Pilih jawaban terbaikmu</span>
                <span id="timeLeftText" class="font-bold text-slate-300">Sisa Waktu: 20s</span>
            </div>
        </div>

        <!-- HALAMAN 3: HASIL AKHIR GAME -->
        <div id="resultScreen" class="hidden bg-slate-800/90 border border-slate-700/60 rounded-3xl p-6 md:p-10 shadow-2xl backdrop-blur-xl text-center">
            
            <div id="resultHeaderIcon" class="w-24 h-24 bg-amber-500/10 border border-amber-500/30 text-amber-400 rounded-full flex items-center justify-center mx-auto mb-4 text-4xl shadow-xl">
                <i class="fa-solid fa-trophy"></i>
            </div>

            <h2 id="resultTitle" class="text-3xl font-black text-white mb-1">Kuis Selesai!</h2>
            <p id="resultSubtitle" class="text-slate-400 text-sm mb-6">Berikut adalah rangkuman hasil kamu</p>

            <!-- Statistik Akhir -->
            <div class="grid grid-cols-2 md:grid-cols-4 gap-3 max-w-xl mx-auto mb-8">
                <div class="bg-slate-900/80 p-4 rounded-2xl border border-slate-800">
                    <div class="text-slate-400 text-xs mb-1">Total Skor</div>
                    <div class="text-2xl font-black text-amber-400" id="finalScore">0</div>
                </div>
                <div class="bg-slate-900/80 p-4 rounded-2xl border border-slate-800">
                    <div class="text-slate-400 text-xs mb-1">Akurasi</div>
                    <div class="text-2xl font-black text-emerald-400" id="finalAccuracy">0%</div>
                </div>
                <div class="bg-slate-900/80 p-4 rounded-2xl border border-slate-800">
                    <div class="text-slate-400 text-xs mb-1">Benar / Salah</div>
                    <div class="text-lg font-bold text-white"><span class="text-emerald-400" id="finalCorrect">0</span> / <span class="text-rose-400" id="finalWrong">0</span></div>
                </div>
                <div class="bg-slate-900/80 p-4 rounded-2xl border border-slate-800">
                    <div class="text-slate-400 text-xs mb-1">Max Streak</div>
                    <div class="text-2xl font-black text-amber-500" id="finalMaxStreak">0x</div>
                </div>
            </div>

            <!-- Tombol Aksi Hasil -->
            <div class="flex flex-wrap gap-3 justify-center mb-8">
                <button id="playAgainBtn" class="px-6 py-3.5 rounded-2xl bg-blue-600 hover:bg-blue-500 text-white font-bold text-sm shadow-lg shadow-blue-600/30 transition cursor-pointer">
                    <i class="fa-solid fa-rotate-right mr-2"></i> Main Lagi
                </button>
                <button id="shareWaResultBtn" class="px-6 py-3.5 rounded-2xl bg-emerald-600 hover:bg-emerald-500 text-white font-bold text-sm shadow-lg shadow-emerald-600/30 transition cursor-pointer">
                    <i class="fa-brands fa-whatsapp mr-2"></i> Bagikan Hasil ke WA
                </button>
                <button id="toggleReviewBtn" class="px-6 py-3.5 rounded-2xl bg-slate-700 hover:bg-slate-600 text-white font-bold text-sm border border-slate-600 transition cursor-pointer">
                    <i class="fa-solid fa-list-check mr-2"></i> Lihat Pembahasan
                </button>
            </div>

            <!-- Panel Pembahasan -->
            <div id="reviewContainer" class="hidden text-left bg-slate-900/90 border border-slate-800 rounded-2xl p-4 md:p-6 max-h-96 overflow-y-auto custom-scrollbar">
                <h4 class="text-base font-bold text-white mb-4 flex items-center gap-2">
                    <i class="fa-solid fa-book-open text-blue-400"></i> Review Kunci Jawaban
                </h4>
                <div id="reviewList" class="space-y-4">
                    <!-- List Pembahasan -->
                </div>
            </div>
        </div>

    </main>

    <!-- Footer -->
    <footer class="relative z-10 border-t border-slate-800 py-4 text-center text-xs text-slate-500">
        Quiz Game Teknologi & AI SMP &bull; Siap dimainkan di Browser & GitHub Pages
    </footer>

    <!-- LOGIKA GAME JAVASCRIPT -->
    <script>
        // System Sound Engine (Synthesizer Web Audio API)
        class SoundEngine {
            constructor() {
                this.ctx = null;
                this.enabled = true;
            }

            init() {
                if (!this.ctx) {
                    this.ctx = new (window.AudioContext || window.webkitAudioContext)();
                }
            }

            playCorrect() {
                if (!this.enabled) return;
                this.init();
                const now = this.ctx.currentTime;
                const osc = this.ctx.createOscillator();
                const gain = this.ctx.createGain();
                
                osc.type = 'sine';
                osc.frequency.setValueAtTime(523.25, now);
                osc.frequency.exponentialRampToValueAtTime(783.99, now + 0.2);
                
                gain.gain.setValueAtTime(0.15, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.3);
                
                osc.connect(gain);
                gain.connect(this.ctx.destination);
                
                osc.start(now);
                osc.stop(now + 0.3);
            }

            playWrong() {
                if (!this.enabled) return;
                this.init();
                const now = this.ctx.currentTime;
                const osc = this.ctx.createOscillator();
                const gain = this.ctx.createGain();
                
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(220, now);
                osc.frequency.exponentialRampToValueAtTime(130, now + 0.25);
                
                gain.gain.setValueAtTime(0.2, now);
                gain.gain.exponentialRampToValueAtTime(0.01, now + 0.3);
                
                osc.connect(gain);
                gain.connect(this.ctx.destination);
                
                osc.start(now);
                osc.stop(now + 0.3);
            }

            playComplete() {
                if (!this.enabled) return;
                this.init();
                const now = this.ctx.currentTime;
                const notes = [523.25, 659.25, 783.99, 1046.50];
                notes.forEach((freq, idx) => {
                    const osc = this.ctx.createOscillator();
                    const gain = this.ctx.createGain();
                    osc.type = 'triangle';
                    osc.frequency.value = freq;
                    gain.gain.setValueAtTime(0.15, now + (idx * 0.1));
                    gain.gain.exponentialRampToValueAtTime(0.001, now + (idx * 0.1) + 0.3);
                    osc.connect(gain);
                    gain.connect(this.ctx.destination);
                    osc.start(now + (idx * 0.1));
                    osc.stop(now + (idx * 0.1) + 0.3);
                });
            }
        }

        const audio = new SoundEngine();

        // Data 35 Soal Teknologi & AI SMP Sesuai Request
        const rawQuestions = [
            { q: "Apa kepanjangan dari AI?", options: ["Artificial Intelligence", "Automatic Internet", "Advanced Information", "Artificial Internet"], answerText: "Artificial Intelligence" },
            { q: "AI dalam bahasa Indonesia disebut...", options: ["Teknologi Digital", "Kecerdasan Buatan", "Jaringan Komputer", "Sistem Informasi"], answerText: "Kecerdasan Buatan" },
            { q: "Contoh penggunaan AI dalam kehidupan sehari-hari adalah...", options: ["Rekomendasi video", "Buku tulis", "Pensil", "Penggaris"], answerText: "Rekomendasi video" },
            { q: "Alat untuk mengetik pada komputer adalah...", options: ["Monitor", "Keyboard", "Speaker", "Printer"], answerText: "Keyboard" },
            { q: "Otak utama komputer disebut...", options: ["RAM", "CPU", "USB", "Mouse"], answerText: "CPU" },
            { q: "Fungsi RAM adalah...", options: ["Menyimpan data sementara", "Mencetak dokumen", "Menampilkan suara", "Menghubungkan internet"], answerText: "Menyimpan data sementara" },
            { q: "Internet adalah...", options: ["Jaringan komputer yang saling terhubung", "Jenis keyboard", "Aplikasi menggambar", "Alat mencetak"], answerText: "Jaringan komputer yang saling terhubung" },
            { q: "Contoh mesin pencari adalah...", options: ["Google", "Paint", "Word", "Calculator"], answerText: "Google" },
            { q: "Fungsi browser adalah...", options: ["Membuka dan menjelajahi internet", "Mengisi baterai", "Mencetak kertas", "Memperbaiki komputer"], answerText: "Membuka dan menjelajahi internet" },
            { q: "Contoh sistem operasi adalah...", options: ["Windows", "YouTube", "Google", "WhatsApp"], answerText: "Windows" },
            { q: "Bluetooth digunakan untuk...", options: ["Menghubungkan perangkat secara nirkabel", "Mencetak buku", "Mengisi baterai", "Menghapus virus"], answerText: "Menghubungkan perangkat secara nirkabel" },
            { q: "AI dapat mempelajari pola berdasarkan...", options: ["Data", "Kertas", "Meja", "Kabel"], answerText: "Data" },
            { q: "Program AI yang dapat melakukan percakapan disebut...", options: ["Chatbot", "Printer", "Scanner", "Router"], answerText: "Chatbot" },
            { q: "Contoh perangkat keras adalah...", options: ["Monitor", "Windows", "Google Chrome", "Microsoft Word"], answerText: "Monitor" },
            { q: "Contoh perangkat lunak adalah...", options: ["Keyboard", "Mouse", "Microsoft Word", "Monitor"], answerText: "Microsoft Word" },
            { q: "Password yang aman sebaiknya...", options: ["Menggunakan kombinasi huruf, angka, dan simbol", "Menggunakan nama sendiri", "Menggunakan tanggal lahir", "Menggunakan 123456"], answerText: "Menggunakan kombinasi huruf, angka, dan simbol" },
            { q: "Phishing bertujuan untuk...", options: ["Mencuri informasi pribadi", "Mempercepat komputer", "Menghemat baterai", "Membuat komputer lebih besar"], answerText: "Mencuri informasi pribadi" },
            { q: "Data pribadi yang harus dijaga adalah...", options: ["Password", "Warna favorit", "Makanan kesukaan", "Hobi"], answerText: "Password" },
            { q: "Jejak digital adalah...", options: ["Rekaman aktivitas seseorang di dunia digital", "Bekas kaki di tanah",# quiz-game-
