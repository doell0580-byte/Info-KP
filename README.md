<!DOCTYPE html>
<html lang="id" class="h-full bg-slate-950 text-slate-100">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Papan Pengumuman Kuliah Pengganti - Universitas Nasional</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- FontAwesome Icons CDN -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts: Inter & JetBrains Mono -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@500;700&display=swap" rel="stylesheet">

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        mono: ['JetBrains Mono', 'monospace'],
                    },
                    colors: {
                        unas: {
                            green: '#005a2b',
                            lightgreen: '#008744',
                            darkgreen: '#00381a',
                            gold: '#fdb813',
                            accent: '#10b981'
                        }
                    },
                    animation: {
                        'marquee': 'marquee 28s linear infinite',
                        'pulse-slow': 'pulse 3s cubic-bezier(0.4, 0, 0.6, 1) infinite',
                    },
                    keyframes: {
                        marquee: {
                            '0%': { transform: 'translateX(100%)' },
                            '100%': { transform: 'translateX(-100%)' },
                        }
                    }
                }
            }
        }
    </script>
    
    <style>
        ::-webkit-scrollbar {
            width: 6px;
            height: 6px;
        }
        ::-webkit-scrollbar-track {
            background: #022c22;
        }
        ::-webkit-scrollbar-thumb {
            background: #065f46;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #047857;
        }
        .glass-panel {
            background: rgba(4, 30, 20, 0.85);
            backdrop-filter: blur(14px);
            -webkit-backdrop-filter: blur(14px);
            border: 1px solid rgba(16, 185, 129, 0.18);
        }
        .glass-panel-light {
            background: rgba(6, 44, 30, 0.6);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(253, 184, 19, 0.15);
        }
        .marquee-container:hover .marquee-content {
            animation-play-state: paused;
        }
        .unas-gold-gradient {
            background: linear-gradient(135deg, #fdb813 0%, #f59e0b 100%);
        }
    </style>
</head>
<body class="h-full flex flex-col font-sans overflow-x-hidden bg-gradient-to-br from-slate-950 via-emerald-950 to-slate-950 text-slate-100 antialiased selection:bg-emerald-500 selection:text-white">

    <header class="glass-panel sticky top-0 z-30 border-b border-emerald-900/60 px-4 py-3 lg:px-8 shadow-2xl">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
            
            <!-- Logo & Brand Header UNAS -->
            <div class="flex items-center gap-4 w-full md:w-auto justify-between md:justify-start">
                <div class="flex items-center gap-3.5">
                    <div class="relative w-14 h-14 rounded-2xl bg-white/95 border border-amber-500/40 p-1 flex items-center justify-center shadow-lg shadow-emerald-950 shrink-0 overflow-hidden">
                        <img src="https://bsdm.unas.ac.id/wp-content/uploads/2022/01/Logo-UNAS-Universitas-Nasional-Original-PNG-1.png" 
                             alt="Logo Universitas Nasional" 
                             class="w-full h-full object-contain drop-shadow"
                             onerror="this.onerror=null; this.src='https://bsdm.unas.ac.id/wp-content/uploads/2022/01/Logo-UNAS-Universitas-Nasional-Original-PNG-1.png';">
                    </div>
                    <div>
                        <div class="flex items-center gap-2">
                            <h1 class="text-xl md:text-2xl font-black tracking-tight text-white flex items-center gap-1.5">
                                SENTRA PELAYANAN AKADEMIK BAA
                            </h1>
                            <span class="text-[10px] px-2 py-0.5 rounded bg-amber-500/20 text-amber-300 font-bold border border-amber-500/40 hidden sm:inline-block">UNAS</span>
                        </div>
                        <p class="text-xs text-emerald-400 font-semibold tracking-wide flex items-center gap-2 mt-0.5">
                            <span class="inline-block w-2.5 h-2.5 rounded-full bg-emerald-400 animate-pulse"></span>
                            PENGUMUMAN KULIAH PENGGANTI AKADEMIK
                        </p>
                    </div>
                </div>

                <!-- Mobile Controls -->
                <div class="md:hidden flex items-center gap-2">
                    <button onclick="fetchSpreadsheetData()" class="p-2 rounded-xl bg-emerald-900/50 hover:bg-emerald-800 text-emerald-300 border border-emerald-700/50">
                        <i id="mobile-refresh-icon" class="fa-solid fa-rotate-right"></i>
                    </button>
                    <button onclick="openHelpModal()" class="p-2 rounded-xl bg-emerald-900/50 hover:bg-emerald-800 text-emerald-300 border border-emerald-700/50">
                        <i class="fa-solid fa-circle-question"></i>
                    </button>
                    <button onclick="openSettingsModal()" class="p-2 rounded-xl bg-emerald-900/50 hover:bg-emerald-800 text-amber-300 border border-amber-500/30">
                        <i class="fa-solid fa-gear"></i>
                    </button>
                </div>
            </div>

            <!-- Jam Digital & Quick Actions -->
            <div class="flex items-center justify-between md:justify-end gap-5 w-full md:w-auto bg-slate-900/90 px-5 py-2.5 rounded-2xl border border-emerald-900/80 shadow-inner">
                <div class="text-left md:text-right">
                    <div id="clock-date" class="text-xs font-bold text-amber-400/90 uppercase tracking-wider">
                        Memuat Tanggal...
                    </div>
                    <div id="clock-time" class="text-2xl md:text-3xl font-extrabold font-mono tracking-wider text-emerald-400 drop-shadow-[0_0_12px_rgba(16,185,129,0.35)]">
                        00:00:00 <span class="text-sm text-slate-400 font-sans font-normal">WIB</span>
                    </div>
                </div>
                
                <!-- Quick Controls -->
                <div class="hidden md:flex items-center gap-2 border-l border-emerald-900/80 pl-4">
                    <button onclick="fetchSpreadsheetData()" title="Muat Ulang Data" class="p-2.5 rounded-xl bg-emerald-950/80 hover:bg-emerald-700 text-emerald-300 hover:text-white transition duration-200 border border-emerald-800">
                        <i id="refresh-icon" class="fa-solid fa-rotate-right"></i>
                    </button>
                    <button onclick="openHelpModal()" title="Petunjuk & Solusi Connection" class="p-2.5 rounded-xl bg-emerald-950/80 hover:bg-emerald-800 text-amber-400 hover:text-white transition duration-200 border border-amber-500/30">
                        <i class="fa-solid fa-circle-question"></i>
                    </button>
                    <button onclick="toggleFullscreen()" title="Layar Penuh / TV Signage Mode" class="p-2.5 rounded-xl bg-emerald-950/80 hover:bg-emerald-700 text-emerald-300 hover:text-white transition duration-200 border border-emerald-800">
                        <i class="fa-solid fa-expand"></i>
                    </button>
                    <button onclick="openSettingsModal()" title="Pengaturan Spreadsheet" class="p-2.5 rounded-xl bg-emerald-950/80 hover:bg-emerald-700 text-amber-400 hover:text-white transition duration-200 relative border border-emerald-800">
                        <i class="fa-solid fa-gear"></i>
                        <span id="config-status-dot" class="absolute -top-1 -right-1 w-3 h-3 bg-emerald-400 border-2 border-slate-900 rounded-full"></span>
                    </button>
                </div>
            </div>

        </div>
    </header>

    <div id="connection-error-banner" class="hidden bg-rose-950/90 border-b border-rose-800/80 text-rose-200 px-4 py-2.5 text-xs md:text-sm font-medium z-20 transition-all">
        <div class="max-w-7xl mx-auto flex items-center justify-between gap-3">
            <div class="flex items-center gap-2.5">
                <i class="fa-solid fa-triangle-exclamation text-rose-400 text-base animate-bounce"></i>
                <span id="error-banner-message">Gagal terhubung. Menggunakan data cadangan.</span>
            </div>
            <div class="flex items-center gap-2">
                <button onclick="openSettingsModal()" class="px-2.5 py-1 rounded-lg bg-amber-500 hover:bg-amber-400 text-slate-950 text-xs font-bold transition">
                    <i class="fa-solid fa-gear mr-1"></i> Pengaturan Link
                </button>
                <button onclick="openHelpModal()" class="px-2.5 py-1 rounded-lg bg-rose-900 hover:bg-rose-800 text-white text-xs font-bold border border-rose-700 transition">
                    <i class="fa-solid fa-lightbulb mr-1"></i> Solusi
                </button>
                <button onclick="dismissErrorBanner()" class="text-rose-400 hover:text-white p-1">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>
        </div>
    </div>

    <main class="flex-1 max-w-7xl w-full mx-auto p-4 md:p-6 lg:p-8 flex flex-col gap-6">

        <!-- FILTER & SEARCH BAR -->
        <div class="glass-panel rounded-2xl p-4 md:p-5 flex flex-col md:flex-row items-stretch md:items-center justify-between gap-4 shadow-xl">
            
            <div class="flex flex-wrap items-center gap-3 flex-1">
                <!-- Date Filter -->
                <div class="relative min-w-[170px] flex-1 sm:flex-none">
                    <label class="block text-[10px] font-bold text-emerald-400/90 uppercase tracking-wider mb-1">
                        <i class="fa-regular fa-calendar-days mr-1"></i> Filter Tanggal
                    </label>
                    <input type="date" id="filter-date" onchange="applyFilters()" 
                        class="w-full bg-slate-900/90 border border-emerald-900 focus:border-emerald-500 rounded-xl px-3 py-2 text-sm text-slate-100 font-medium focus:outline-none focus:ring-2 focus:ring-emerald-500/20 transition">
                </div>

                <!-- Program Studi Filter -->
                <div class="relative min-w-[180px] flex-1 sm:flex-none">
                    <label class="block text-[10px] font-bold text-emerald-400/90 uppercase tracking-wider mb-1">
                        <i class="fa-solid fa-graduation-cap mr-1"></i> Program Studi
                    </label>
                    <select id="filter-prodi" onchange="applyFilters()" 
                        class="w-full bg-slate-900/90 border border-emerald-900 focus:border-emerald-500 rounded-xl px-3 py-2 text-sm text-slate-100 font-medium focus:outline-none focus:ring-2 focus:ring-emerald-500/20 transition cursor-pointer">
                        <option value="ALL">Semua Program Studi</option>
                    </select>
                </div>

                <!-- Search Input -->
                <div class="relative flex-1 min-w-[220px]">
                    <label class="block text-[10px] font-bold text-emerald-400/90 uppercase tracking-wider mb-1">
                        <i class="fa-solid fa-magnifying-glass mr-1"></i> Cari Mata Kuliah / Dosen / Ruang
                    </label>
                    <div class="relative">
                        <i class="fa-solid fa-magnifying-glass absolute left-3 top-1/2 -translate-y-1/2 text-slate-500 text-xs"></i>
                        <input type="text" id="filter-search" oninput="applyFilters()" placeholder="Ketik matakuliah, nama dosen, ruang..." 
                            class="w-full bg-slate-900/90 border border-emerald-900 focus:border-emerald-500 rounded-xl pl-9 pr-3 py-2 text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-emerald-500/20 transition">
                    </div>
                </div>
            </div>

            <!-- Quick Filter Preset Buttons -->
            <div class="flex items-center gap-2 self-end md:self-center pt-2 md:pt-0 border-t md:border-t-0 border-emerald-900/60">
                <button onclick="setFilterToday()" class="px-3.5 py-2 rounded-xl bg-emerald-700 hover:bg-emerald-600 text-white text-xs font-bold transition shadow-md shadow-emerald-950 border border-emerald-600">
                    Hari Ini
                </button>
                <button onclick="clearDateFilter()" class="px-3.5 py-2 rounded-xl bg-slate-900 hover:bg-slate-800 text-slate-300 hover:text-white text-xs font-semibold transition border border-emerald-900/80">
                    Semua Jadwal
                </button>
            </div>

        </div>

        <div class="grid grid-cols-2 sm:grid-cols-4 gap-3 md:gap-4">
            <div class="glass-panel-light p-3.5 rounded-2xl flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-emerald-500/10 border border-emerald-500/20 text-emerald-400 flex items-center justify-center text-lg">
                    <i class="fa-solid fa-calendar-check"></i>
                </div>
                <div>
                    <div id="stat-total" class="text-lg md:text-xl font-bold">0</div>
                    <div class="text-[11px] text-slate-400 font-medium">Total Kuliah Pengganti</div>
                </div>
            </div>

            <div class="glass-panel-light p-3.5 rounded-2xl flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-amber-500/10 border border-amber-500/20 text-amber-400 flex items-center justify-center text-lg">
                    <i class="fa-solid fa-circle-play animate-pulse"></i>
                </div>
                <div>
                    <div id="stat-active" class="text-lg md:text-xl font-bold text-amber-400">0</div>
                    <div class="text-[11px] text-slate-400 font-medium">Sedang Berlangsung</div>
                </div>
            </div>

            <div class="glass-panel-light p-3.5 rounded-2xl flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-teal-500/10 border border-teal-500/20 text-teal-300 flex items-center justify-center text-lg">
                    <i class="fa-solid fa-clock"></i>
                </div>
                <div>
                    <div id="stat-upcoming" class="text-lg md:text-xl font-bold text-teal-300">0</div>
                    <div class="text-[11px] text-slate-400 font-medium">Akan Datang</div>
                </div>
            </div>

            <div class="glass-panel-light p-3.5 rounded-2xl flex items-center gap-3">
                <div class="w-10 h-10 rounded-xl bg-slate-800 text-slate-400 border border-slate-700 flex items-center justify-center text-lg">
                    <i class="fa-solid fa-circle-check"></i>
                </div>
                <div>
                    <div id="stat-completed" class="text-lg md:text-xl font-bold text-slate-400">0</div>
                    <div class="text-[11px] text-slate-400 font-medium">Selesai</div>
                </div>
            </div>
        </div>

        <div class="glass-panel rounded-2xl shadow-2xl overflow-hidden border border-emerald-900/80 flex flex-col flex-1">
            
            <div class="px-6 py-4 bg-slate-900/90 border-b border-emerald-900/80 flex flex-wrap items-center justify-between gap-3">
                <div class="flex items-center gap-2.5">
                    <div class="w-3 h-3 rounded-full bg-amber-400 shadow-[0_0_8px_#fdb813]"></div>
                    <h2 class="font-bold text-sm md:text-base tracking-wide text-white">
                        DAFTAR KULIAH PENGGANTI UNIVERSITAS NASIONAL
                    </h2>
                    <span id="active-date-badge" class="px-2.5 py-0.5 rounded-full bg-emerald-950 border border-emerald-700 text-emerald-300 text-xs font-semibold">
                        Hari Ini
                    </span>
                </div>
                
                <div class="flex items-center gap-3 text-xs text-slate-400">
                    <div id="sync-status" class="flex items-center gap-1.5 px-2.5 py-1 rounded-lg bg-emerald-950/60 border border-emerald-800/80 text-emerald-300">
                        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
                        <span id="sync-status-text"> </span>
                    </div>
                </div>
            </div>

            <!-- Table Container -->
            <div class="overflow-x-auto flex-1">
                <table class="w-full text-left border-collapse">
                    <thead>
                        <tr class="bg-slate-900/80 border-b border-emerald-900/80 text-[11px] uppercase tracking-wider text-emerald-300 font-extrabold select-none">
                            <th class="py-3.5 px-4 text-center w-12 border-r border-emerald-900/40">No</th>
                            <th class="py-3.5 px-4 min-w-[200px]">Matakuliah</th>
                            <th class="py-3.5 px-4 text-center min-w-[90px]">Kelas</th>
                            <th class="py-3.5 px-4 min-w-[180px]">Nama Dosen</th>
                            <th class="py-3.5 px-4 text-center min-w-[140px]">Waktu</th>
                            <th class="py-3.5 px-4 text-center min-w-[110px]">Ruang</th>
                            <th class="py-3.5 px-4 min-w-[160px]">Prodi</th>
                            <th class="py-3.5 px-4 text-center min-w-[140px]">Status</th>
                        </tr>
                    </thead>
                    <tbody id="schedule-tbody" class="divide-y divide-emerald-900/30 text-sm font-medium">
                        <!-- Dynamic Rows Injected via JavaScript -->
                    </tbody>
                </table>

                <!-- Empty State Component -->
                <div id="empty-state" class="hidden py-16 text-center">
                    <div class="w-16 h-16 rounded-2xl bg-emerald-950/60 border border-emerald-800 flex items-center justify-center mx-auto mb-3 text-emerald-400 text-2xl shadow-lg">
                        <i class="fa-solid fa-calendar-xmark"></i>
                    </div>
                    <h3 class="text-base font-bold text-slate-200">Tidak Ada Jadwal Kuliah Pengganti</h3>
                    <p class="text-xs text-slate-400 mt-1 max-w-md mx-auto">
                        Tidak ada perkuliahan pengganti yang sesuai dengan tanggal, program studi, atau kata kunci pencarian yang dipilih.
                    </p>
                </div>
            </div>

            <!-- Table Footer Status -->
            <div class="px-6 py-3 bg-slate-900/60 border-t border-emerald-900/60 text-xs text-slate-400 flex flex-wrap items-center justify-between gap-2">
                <div>Menampilkan <span id="showing-count" class="font-bold text-emerald-400">0</span> jadwal perkuliahan</div>
                <div class="flex items-center gap-4 text-[11px] text-slate-400">
                    <span>Otomatis Sinkronisasi: <span id="refresh-interval-label" class="font-bold text-slate-200">30 detik</span></span>
                    <button onclick="openHelpModal()" class="text-amber-400 hover:underline flex items-center gap-1">
                        <i class="fa-solid fa-triangle-exclamation"></i> Bantuan Koneksi Spreadsheet
                    </button>
                </div>
            </div>
        </div>

    </main>

    <footer class="mt-auto bg-gradient-to-r from-emerald-950 via-slate-900 to-emerald-950 border-t border-emerald-800/80 relative overflow-hidden py-3 shadow-2xl z-20">
        <div class="flex items-center">
            <!-- Badge Label Pengumuman -->
            <div class="z-10 unas-gold-gradient text-slate-950 font-black text-xs uppercase px-4 py-2 shadow-lg flex items-center gap-2 shrink-0 rounded-r-xl ml-2 border border-amber-300/50 tracking-wider">
                <i class="fa-solid fa-bullhorn animate-bounce"></i>
                <span>PENGUMUMAN UNAS</span>
            </div>

            <!-- Marquee Running Text with screen size responsive speed/padding -->
            <div class="overflow-hidden whitespace-nowrap w-full relative flex items-center py-0.5 marquee-container">
                <div id="running-text-content" class="inline-block animate-marquee marquee-content pl-8 text-xs sm:text-sm md:text-base font-semibold text-emerald-100 tracking-wide">
                    📢 PENGUMUMAN KULIAH PENGGANTI UNAS: Mahasiswa diwajibkan hadir tepat waktu sesuai dengan tanggal dan ruangan yang tertera pada papan digital. Harap perhatikan perubahan jam kuliah!
                </div>
            </div>
        </div>
    </footer>

    <div id="settings-modal" class="fixed inset-0 bg-slate-950/85 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden transition-opacity duration-300">
        <div class="glass-panel w-full max-w-2xl rounded-3xl p-6 border border-emerald-800 shadow-2xl relative overflow-hidden max-h-[90vh] flex flex-col">
            
            <div class="flex items-center justify-between border-b border-emerald-900/80 pb-4 mb-4">
                <div class="flex items-center gap-3">
                    <div class="w-10 h-10 rounded-xl bg-amber-500/20 text-amber-400 border border-amber-500/40 flex items-center justify-center text-lg">
                        <i class="fa-solid fa-file-csv"></i>
                    </div>
                    <div>
                        <h3 class="text-lg font-bold text-white">Integrasi Google Sheets CSV</h3>
                        <p class="text-xs text-slate-400">Hubungkan tabel Google Sheets Universitas Nasional untuk pembaruan data real-time</p>
                    </div>
                </div>
                <button onclick="closeSettingsModal()" class="w-8 h-8 rounded-full bg-slate-800 hover:bg-slate-700 text-slate-400 hover:text-white flex items-center justify-center transition">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="space-y-5 overflow-y-auto pr-1 flex-1">
                <div>
                    <div class="flex items-center justify-between mb-2">
                        <label class="block text-xs font-bold text-emerald-400 uppercase tracking-wider">
                            URL Google Sheets (Semua Format Link Didukung)
                        </label>
                        <button type="button" onclick="testConnectionFromModal()" class="text-xs text-amber-300 hover:text-amber-200 bg-amber-500/20 hover:bg-amber-500/30 px-2.5 py-1 rounded-lg border border-amber-500/40 font-semibold transition">
                            <i id="test-icon" class="fa-solid fa-plug mr-1"></i> Uji Koneksi Link
                        </button>
                    </div>
                    <input type="text" id="input-sheet-url" 
                        placeholder="Tempelkan link Google Sheets Anda di sini..." 
                        class="w-full bg-slate-900 border border-emerald-800 focus:border-amber-400 rounded-xl px-4 py-2.5 text-sm text-slate-100 placeholder-slate-600 focus:outline-none focus:ring-2 focus:ring-amber-400/20">
                    <div id="modal-test-result" class="hidden mt-2 p-2.5 rounded-xl text-xs font-medium"></div>
                    <p class="text-[11px] text-slate-400 mt-1.5 flex items-center gap-1">
                        <i class="fa-solid fa-circle-info text-amber-400"></i>
                        Aplikasi otomatis mengonversi link biasa (<code class="text-emerald-300">/edit#gid=0</code>) menjadi format CSV interaktif.
                    </p>
                </div>

                <div>
                    <label class="block text-xs font-bold text-emerald-400 uppercase tracking-wider mb-2">
                        Teks Berjalan (Running Text)
                    </label>
                    <textarea id="input-running-text" rows="2" 
                        placeholder="Tulis pesan pengumuman berjalan..." 
                        class="w-full bg-slate-900 border border-emerald-800 focus:border-amber-400 rounded-xl px-4 py-2 text-sm text-slate-100 placeholder-slate-600 focus:outline-none focus:ring-2 focus:ring-amber-400/20"></textarea>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-xs font-bold text-emerald-400 uppercase tracking-wider mb-2">
                            Interval Pembaruan Data Otomatis
                        </label>
                        <select id="input-refresh-interval" 
                            class="w-full bg-slate-900 border border-emerald-800 focus:border-amber-400 rounded-xl px-3 py-2.5 text-sm text-slate-100 focus:outline-none cursor-pointer">
                            <option value="10000">Setiap 10 Detik</option>
                            <option value="30000" selected>Setiap 30 Detik</option>
                            <option value="60000">Setiap 1 Menit</option>
                            <option value="300000">Setiap 5 Menit</option>
                            <option value="0">Manual (Tanpa Auto-refresh)</option>
                        </select>
                    </div>

                    <div>
                        <label class="block text-xs font-bold text-emerald-400 uppercase tracking-wider mb-2">
                            Reset Data
                        </label>
                        <button type="button" onclick="loadSampleData(); closeSettingsModal();" class="w-full bg-slate-900 hover:bg-slate-800 text-amber-300 hover:text-amber-200 border border-amber-500/40 rounded-xl px-4 py-2.5 text-sm font-semibold transition flex items-center justify-center gap-2">
                            <i class="fa-solid fa-wand-magic-sparkles"></i>
                            Tampilkan Data Contoh
                        </button>
                    </div>
                </div>

                <!-- Table Format Reference Guide -->
                <div class="bg-slate-900/90 rounded-2xl p-4 border border-emerald-900">
                    <h4 class="text-xs font-bold text-amber-400 uppercase tracking-wider mb-2 flex items-center gap-2">
                        <i class="fa-solid fa-table-cells"></i> Format Header Baris Pertama di Google Sheets
                    </h4>
                    <p class="text-xs text-slate-400 mb-2">
                        Pastikan baris ke-1 spreadsheet Anda mencakup kolom berikut (Tambahkan kolom <code class="text-amber-300">Checklist</code> / <code class="text-amber-300">Status</code> diisi huruf <code class="text-emerald-300">v</code> agar status "Sedang Berlangsung" dapat aktif):
                    </p>
                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-[11px] font-mono border border-emerald-900">
                            <thead class="bg-slate-800 text-emerald-300">
                                <tr>
                                    <th class="p-1.5 border border-slate-700">Tanggal</th>
                                    <th class="p-1.5 border border-slate-700">Matakuliah</th>
                                    <th class="p-1.5 border border-slate-700">Kelas</th>
                                    <th class="p-1.5 border border-slate-700">Nama Dosen</th>
                                    <th class="p-1.5 border border-slate-700">Waktu</th>
                                    <th class="p-1.5 border border-slate-700">Ruang</th>
                                    <th class="p-1.5 border border-slate-700">Prodi</th>
                                    <th class="p-1.5 border border-slate-700 text-amber-300">Checklist</th>
                                </tr>
                            </thead>
                            <tbody class="text-slate-300">
                                <tr>
                                    <td class="p-1.5 border border-slate-800">2026-09-25</td>
                                    <td class="p-1.5 border border-slate-800">Pemrograman Web</td>
                                    <td class="p-1.5 border border-slate-800">IF-01</td>
                                    <td class="p-1.5 border border-slate-800">Dr. Septi</td>
                                    <td class="p-1.5 border border-slate-800">08:00 - 10:30</td>
                                    <td class="p-1.5 border border-slate-800">Cyber Lab 2</td>
                                    <td class="p-1.5 border border-slate-800">Informatika</td>
                                    <td class="p-1.5 border border-slate-800 text-amber-300 font-bold">v</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>

            </div>

            <div class="flex items-center justify-between border-t border-emerald-900/80 pt-4 mt-4">
                <button type="button" onclick="closeSettingsModal()" class="px-4 py-2 rounded-xl bg-slate-800 hover:bg-slate-700 text-slate-300 text-sm font-medium transition">
                    Batal
                </button>
                <button type="button" onclick="saveSettings()" class="px-6 py-2 rounded-xl bg-emerald-600 hover:bg-emerald-500 text-white text-sm font-bold transition shadow-lg shadow-emerald-950 border border-emerald-500">
                    Simpan & Terapkan
                </button>
            </div>

        </div>
    </div>

    <div id="help-modal" class="fixed inset-0 bg-slate-950/85 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden transition-opacity duration-300">
        <div class="glass-panel w-full max-w-2xl rounded-3xl p-6 border border-emerald-800 shadow-2xl relative overflow-hidden max-h-[90vh] flex flex-col">
            
            <div class="flex items-center justify-between border-b border-emerald-900/80 pb-4 mb-4">
                <div class="flex items-center gap-3">
                    <div class="w-10 h-10 rounded-xl bg-rose-500/20 text-rose-400 border border-rose-500/40 flex items-center justify-center text-lg">
                        <i class="fa-solid fa-circle-question"></i>
                    </div>
                    <div>
                        <h3 class="text-lg font-bold text-white">Panduan Menghubungkan Google Sheets</h3>
                        <p class="text-xs text-slate-400">Langkah mudah agar data perkuliahan langsung tampil di papan pengumuman</p>
                    </div>
                </div>
                <button onclick="closeHelpModal()" class="w-8 h-8 rounded-full bg-slate-800 hover:bg-slate-700 text-slate-400 hover:text-white flex items-center justify-center transition">
                    <i class="fa-solid fa-xmark"></i>
                </button>
            </div>

            <div class="space-y-4 overflow-y-auto pr-1 flex-1 text-xs md:text-sm text-slate-300">
                
                <div class="bg-slate-900/90 rounded-2xl p-4 border border-emerald-900/80 space-y-2">
                    <h4 class="font-bold text-amber-400 text-sm flex items-center gap-2">
                        <span class="w-5 h-5 rounded-full bg-amber-500 text-slate-950 flex items-center justify-center text-xs font-black">1</span>
                        Bagikan Akses Spreadsheet Menjadi Publik
                    </h4>
                    <p class="text-slate-400 leading-relaxed">
                        Buka dokumen Google Sheets Anda &gt; Klik tombol hijau <strong>Bagikan (Share)</strong> di pojok kanan atas &gt; Ubah "Akses umum" dari <em>Dibatasi</em> menjadi <strong>"Siapa saja yang memiliki link" (Anyone with the link)</strong>.
                    </p>
                </div>

                <div class="bg-slate-900/90 rounded-2xl p-4 border border-emerald-900/80 space-y-2">
                    <h4 class="font-bold text-amber-400 text-sm flex items-center gap-2">
                        <span class="w-5 h-5 rounded-full bg-amber-500 text-slate-950 flex items-center justify-center text-xs font-black">2</span>
                        Tambahkan Kolom Checklist / Validasi Masuk
                    </h4>
                    <p class="text-slate-400 leading-relaxed">
                        Tambahkan kolom dengan judul <code class="text-amber-300">Checklist</code> di kolom paling kanan. Isi dengan huruf <code class="text-emerald-300">v</code> atau tanda centang bila jadwal tersebut sudah resmi/masuk. Jika dikosongkan, status "Sedang Berlangsung" tidak akan menyala.
                    </p>
                </div>

            </div>

            <div class="flex items-center justify-between border-t border-emerald-900/80 pt-4 mt-4">
                <button type="button" onclick="loadSampleData(); closeHelpModal();" class="px-4 py-2 rounded-xl bg-amber-500 hover:bg-amber-400 text-slate-950 text-xs font-extrabold transition">
                    <i class="fa-solid fa-play mr-1"></i> Gunakan Data Contoh
                </button>
                <button type="button" onclick="closeHelpModal()" class="px-5 py-2 rounded-xl bg-emerald-700 hover:bg-emerald-600 text-white text-xs font-bold transition">
                    Tutup
                </button>
            </div>

        </div>
    </div>

    <script>
        const STORAGE_KEY_CONFIG = 'unas_papan_pengumuman_config_v1';
        
        let appState = {
            sheetUrl: 'https://docs.google.com/spreadsheets/d/1xJFzP5Ddqmfb3YzzDnnJ2Okigcyz_kkJ2vS0YB79nFQ/edit?gid=735846717#gid=735846717',
            runningText: '📢 PENGUMUMAN UNIVERSITAS NASIONAL: Mahasiswa diwajibkan memperhatikan tanggal, jam, dan ruangan kuliah pengganti. Pastikan hadir tepat waktu!',
            refreshInterval: 30000,
            schedules: [],
            filteredSchedules: [],
            selectedDate: getTodayYYYYMMDD(),
            selectedProdi: 'ALL',
            searchQuery: '',
            autoRefreshTimer: null
        };

        // Default mock sample dataset tailored for Universitas Nasional (UNAS)
        const SAMPLE_DATA_UNAS = [
            {
                no: 1,
                tanggal: getTodayYYYYMMDD(),
                matakuliah: "Pemrograman Web & Seluler",
                kelas: "IF-01",
                nama_dosen: "Dr. Septi Andryana, S.Kom., M.M.S.I.",
                waktu: "08:00 - 10:30",
                ruang: "Cyber Lab 2",
                prodi: "Informatika"
            },
            {
                no: 2,
                tanggal: getTodayYYYYMMDD(),
                matakuliah: "Sistem Informasi Manajemen",
                kelas: "SI-02",
                nama_dosen: "Drs. Augusdin, M.M.S.I.",
                waktu: "10:30 - 13:00",
                ruang: "R. Blok I.302",
                prodi: "Sistem Informasi"
            },
            {
                no: 3,
                tanggal: getTodayYYYYMMDD(),
                matakuliah: "Hukum Tata Negara",
                kelas: "HK-04",
                nama_dosen: "Prof. Dr. Basuki Rekso Wibowo, S.H., M.S.",
                waktu: "13:30 - 16:00",
                ruang: "R. Dekanat Hukum",
                prodi: "Ilmu Hukum"
            },
            {
                no: 4,
                tanggal: getTodayYYYYMMDD(),
                matakuliah: "Komunikasi Politik",
                kelas: "KP-02",
                nama_dosen: "Dr. Kumba Digdowiseiso, S.E., M.Si.",
                waktu: "16:15 - 18:00",
                ruang: "Auditorium UNAS",
                prodi: "Ilmu Komunikasi"
            },
            {
                no: 5,
                tanggal: getTodayYYYYMMDD(),
                matakuliah: "Kecerdasan Buatan (AI)",
                kelas: "IF-03",
                nama_dosen: "Fauziah, S.Kom., M.M.S.I.",
                waktu: "09:00 - 11:30",
                ruang: "Cyber Lab 1",
                prodi: "Informatika"
            },
            {
                no: 6,
                tanggal: getOffsetYYYYMMDD(1),
                matakuliah: "Manajemen Keuangan Internasional",
                kelas: "MJ-05",
                nama_dosen: "Dr. Muhani, S.E., M.Si.",
                waktu: "08:00 - 10:30",
                ruang: "R. Blok II.401",
                prodi: "Manajemen"
            }
        ];

        window.onload = function() {
            initClock();
            loadSavedConfig();
            
            document.getElementById('filter-date').value = appState.selectedDate;

            if (appState.sheetUrl && appState.sheetUrl.trim() !== '') {
                fetchSpreadsheetData();
            } else {
                loadSampleData();
            }

            setupAutoRefreshTimer();
        };

        function initClock() {
            updateClock();
            setInterval(updateClock, 1000);
        }

        function updateClock() {
            const now = new Date();
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            const dateStr = now.toLocaleDateString('id-ID', options);
            
            const hours = String(now.getHours()).padStart(2, '0');
            const minutes = String(now.getMinutes()).padStart(2, '0');
            const seconds = String(now.getSeconds()).padStart(2, '0');
            const timeStr = `${hours}:${minutes}:${seconds}`;

            const clockDateEl = document.getElementById('clock-date');
            const clockTimeEl = document.getElementById('clock-time');

            if (clockDateEl) clockDateEl.innerText = dateStr;
            if (clockTimeEl) clockTimeEl.innerHTML = `${timeStr} <span class="text-sm text-slate-400 font-sans font-normal">WIB</span>`;

            if (now.getSeconds() === 0) {
                applyFilters();
            }
        }

        async function fetchSpreadsheetData() {
            if (!appState.sheetUrl || appState.sheetUrl.trim() === '') {
                loadSampleData();
                return;
            }

            const refreshIcon = document.getElementById('refresh-icon');
            const mobileRefreshIcon = document.getElementById('mobile-refresh-icon');
            if (refreshIcon) refreshIcon.classList.add('fa-spin');
            if (mobileRefreshIcon) mobileRefreshIcon.classList.add('fa-spin');

            try {
                let formattedUrls = getFormattedCsvUrls(appState.sheetUrl);
                let csvText = null;
                let lastError = null;

                for (let url of formattedUrls) {
                    try {
                        const response = await fetch(url, { cache: "no-store" });
                        if (response.ok) {
                            const text = await response.text();
                            if (text && text.trim().length > 10) {
                                csvText = text;
                                break;
                            }
                        }
                    } catch (e) {
                        lastError = e;
                    }
                }

                if (!csvText) {
                    throw lastError || new Error("Gagal mengunduh isi dokumen.");
                }

                const parsedData = parseCsv(csvText);

                if (parsedData && parsedData.length > 0) {
                    appState.schedules = parsedData;
                    populateProdiDropdown();
                    applyFilters();
                    updateSyncBadge(true, "Live");
                    dismissErrorBanner();
                } else {
                    throw new Error("Data CSV kosong atau nama kolom header baris pertama tidak cocok.");
                }

            } catch (err) {
                console.warn("Spreadsheet Fetch Error:", err);
                updateSyncBadge(false, "Offline");
                showErrorBanner(`Gagal terhubung (${err.message || 'Error'}). Menggunakan data cadangan.`);
                if (appState.schedules.length === 0) {
                    loadSampleData();
                }
            } finally {
                if (refreshIcon) refreshIcon.classList.remove('fa-spin');
                if (mobileRefreshIcon) mobileRefreshIcon.classList.remove('fa-spin');
            }
        }

        function getFormattedCsvUrls(url) {
            let urls = [];
            const trimmed = url.trim();

            if (trimmed.includes('pub?output=csv') || trimmed.includes('/pub?')) {
                urls.push(trimmed);
            }

            const matchDoc = trimmed.match(/\/d\/([a-zA-Z0-9-_]+)/);
            if (matchDoc && matchDoc[1]) {
                const sheetId = matchDoc[1];
                const gidMatch = trimmed.match(/gid=([0-9]+)/);
                const gidParam = gidMatch ? `&gid=${gidMatch[1]}` : '';

                urls.push(`https://docs.google.com/spreadsheets/d/${sheetId}/gviz/tq?tqx=out:csv${gidParam}`);
                urls.push(`https://docs.google.com/spreadsheets/d/${sheetId}/export?format=csv${gidParam}`);
            }

            if (urls.length > 0) {
                urls.push(`https://api.allorigins.win/raw?url=${encodeURIComponent(urls[0])}`);
            } else {
                urls.push(trimmed);
            }

            return urls;
        }

        async function testConnectionFromModal() {
            const inputUrl = document.getElementById('input-sheet-url').value.trim();
            const resultEl = document.getElementById('modal-test-result');
            const testIcon = document.getElementById('test-icon');

            if (!inputUrl) {
                resultEl.className = "mt-2 p-2.5 rounded-xl text-xs font-semibold bg-rose-950/80 border border-rose-800 text-rose-300 block";
                resultEl.innerText = "Masukkan URL Google Sheets terlebih dahulu!";
                return;
            }

            if (testIcon) testIcon.className = "fa-solid fa-spinner fa-spin mr-1";
            resultEl.className = "mt-2 p-2.5 rounded-xl text-xs font-semibold bg-slate-800 border border-slate-700 text-slate-300 block";
            resultEl.innerText = "Menguji koneksi ke Google Sheets...";

            try {
                const urls = getFormattedCsvUrls(inputUrl);
                let success = false;
                let parsedRows = 0;

                for (let u of urls) {
                    try {
                        const res = await fetch(u, { cache: "no-store" });
                        if (res.ok) {
                            const txt = await res.text();
                            const parsed = parseCsv(txt);
                            if (parsed && parsed.length > 0) {
                                success = true;
                                parsedRows = parsed.length;
                                break;
                            }
                        }
                    } catch (e) {}
                }

                if (success) {
                    resultEl.className = "mt-2 p-2.5 rounded-xl text-xs font-bold bg-emerald-950/90 border border-emerald-700 text-emerald-300 block";
                    resultEl.innerHTML = `<i class="fa-solid fa-circle-check mr-1 text-emerald-400"></i> Koneksi Berhasil! Ditemukan <strong>${parsedRows}</strong> baris jadwal.`;
                } else {
                    throw new Error("Format CSV tidak terbaca atau akses link masih dibatasi.");
                }
            } catch (err) {
                resultEl.className = "mt-2 p-2.5 rounded-xl text-xs font-semibold bg-rose-950/90 border border-rose-800 text-rose-300 block";
                resultEl.innerHTML = `<i class="fa-solid fa-triangle-exclamation mr-1 text-rose-400"></i> Koneksi Gagal: ${err.message}`;
            } finally {
                if (testIcon) testIcon.className = "fa-solid fa-plug mr-1";
            }
        }

        function parseCsv(text) {
            if (!text) return [];
            const cleanText = text.replace(/^\uFEFF/, '');
            const lines = cleanText.split(/\r\n|\n/);
            if (lines.length < 2) return [];

            const headers = parseCsvRow(lines[0]).map(h => h.trim().toLowerCase());
            const results = [];

            for (let i = 1; i < lines.length; i++) {
                if (!lines[i].trim()) continue;
                const row = parseCsvRow(lines[i]);
                if (row.length === 0) continue;

                let item = {
                    no: i,
                    tanggal: getHeaderValue(headers, row, ['tanggal', 'date', 'tgl']) || getTodayYYYYMMDD(),
                    matakuliah: getHeaderValue(headers, row, ['matakuliah', 'mata kuliah', 'course', 'mk']) || '-',
                    kelas: getHeaderValue(headers, row, ['kelas', 'class', 'kls']) || '-',
                    nama_dosen: getHeaderValue(headers, row, ['nama dosen', 'dosen', 'lecturer', 'pengajar']) || '-',
                    waktu: getHeaderValue(headers, row, ['waktu', 'jam', 'time', 'jadwal']) || '-',
                    ruang: getHeaderValue(headers, row, ['ruang', 'ruangan', 'room', 'lab']) || '-',
                    prodi: getHeaderValue(headers, row, ['prodi', 'program studi', 'department', 'jurusan']) || 'Umum',
                    checklist: getHeaderValue(headers, row, ['checklist', 'status', 'cek', 'hadir', 'v']) || ''
                };
                results.push(item);
            }
            return results;
        }

        function parseCsvRow(rowText) {
            let p = '', insideQuote = false, row = [];
            for (let i = 0; i < rowText.length; i++) {
                let c = rowText[i];
                if (c === '"') {
                    insideQuote = !insideQuote;
                } else if (c === ',' && !insideQuote) {
                    row.push(p.trim().replace(/^"|"$/g, ''));
                    p = '';
                } else {
                    p += c;
                }
            }
            row.push(p.trim().replace(/^"|"$/g, ''));
            return row;
        }

        function getHeaderValue(headers, row, possibleNames) {
            for (let name of possibleNames) {
                const index = headers.findIndex(h => h.includes(name));
                if (index !== -1 && row[index] !== undefined && row[index] !== null) {
                    return row[index].trim();
                }
            }
            return '';
        }

        function applyFilters() {
            const dateVal = document.getElementById('filter-date').value;
            const prodiVal = document.getElementById('filter-prodi').value;
            const searchVal = document.getElementById('filter-search').value.toLowerCase().trim();

            appState.selectedDate = dateVal;
            appState.selectedProdi = prodiVal;
            appState.searchQuery = searchVal;

            appState.filteredSchedules = appState.schedules.filter(item => {
                let matchDate = !dateVal || normalizeDate(item.tanggal) === normalizeDate(dateVal);
                let matchProdi = !prodiVal || prodiVal === 'ALL' || item.prodi.toLowerCase() === prodiVal.toLowerCase();
                let matchSearch = !searchVal || 
                    item.matakuliah.toLowerCase().includes(searchVal) ||
                    item.nama_dosen.toLowerCase().includes(searchVal) ||
                    item.ruang.toLowerCase().includes(searchVal) ||
                    item.kelas.toLowerCase().includes(searchVal);

                return matchDate && matchProdi && matchSearch;
            });

            // CHRONOLOGICAL & STATUS SORTING ALGORITHM
            appState.filteredSchedules.sort((a, b) => {
                const statusA = calculateTimeStatus(a).code;
                const statusB = calculateTimeStatus(b).code;

                const priorityMap = { 'ACTIVE': 1, 'UNCHECKED_ACTIVE': 2, 'UPCOMING': 3, 'PENDING': 4, 'COMPLETED': 5 };
                const pA = priorityMap[statusA] || 6;
                const pB = priorityMap[statusB] || 6;

                if (pA !== pB) {
                    return pA - pB;
                }

                const startA = getStartTimeMinutes(a.waktu);
                const startB = getStartTimeMinutes(b.waktu);
                return startA - startB;
            });

            const dateBadge = document.getElementById('active-date-badge');
            if (dateBadge) {
                if (dateVal === getTodayYYYYMMDD()) {
                    dateBadge.innerText = 'Hari Ini';
                    dateBadge.className = 'px-2.5 py-0.5 rounded-full bg-emerald-950 border border-emerald-700 text-emerald-300 text-xs font-semibold';
                } else if (!dateVal) {
                    dateBadge.innerText = 'Semua Tanggal';
                    dateBadge.className = 'px-2.5 py-0.5 rounded-full bg-slate-800 border border-slate-700 text-slate-300 text-xs font-semibold';
                } else {
                    dateBadge.innerText = formatDateIndonesian(dateVal);
                    dateBadge.className = 'px-2.5 py-0.5 rounded-full bg-amber-950 border border-amber-700 text-amber-300 text-xs font-semibold';
                }
            }

            renderTable();
            updateSummaryCounters();
        }

        function getStartTimeMinutes(timeRangeStr) {
            if (!timeRangeStr) return 0;
            const times = timeRangeStr.split('-').map(t => t.trim());
            return parseTimeToMinutes(times[0]);
        }

        function setFilterToday() {
            document.getElementById('filter-date').value = getTodayYYYYMMDD();
            applyFilters();
        }

        function clearDateFilter() {
            document.getElementById('filter-date').value = '';
            applyFilters();
        }

        function renderTable() {
            const tbody = document.getElementById('schedule-tbody');
            const emptyState = document.getElementById('empty-state');
            const showingCount = document.getElementById('showing-count');

            if (!tbody) return;
            tbody.innerHTML = '';

            if (appState.filteredSchedules.length === 0) {
                tbody.classList.add('hidden');
                if (emptyState) emptyState.classList.remove('hidden');
                if (showingCount) showingCount.innerText = '0';
                return;
            }

            tbody.classList.remove('hidden');
            if (emptyState) emptyState.classList.add('hidden');
            if (showingCount) showingCount.innerText = appState.filteredSchedules.length;

            appState.filteredSchedules.forEach((item, index) => {
                const tr = document.createElement('tr');
                const statusInfo = calculateTimeStatus(item);
                
                let rowBgClass = "hover:bg-emerald-950/40 transition duration-150";
                if (statusInfo.code === 'ACTIVE') {
                    rowBgClass = "bg-amber-500/10 hover:bg-amber-500/20 border-l-4 border-l-amber-400 transition duration-150";
                } else if (statusInfo.code === 'UNCHECKED_ACTIVE') {
                    rowBgClass = "bg-rose-950/20 hover:bg-rose-950/30 border-l-4 border-l-rose-500 transition duration-150";
                }

                tr.className = `${rowBgClass}`;

                tr.innerHTML = `
                    <td class="py-4 px-4 text-center font-bold text-slate-400 border-r border-emerald-900/30">${index + 1}</td>
                    <td class="py-4 px-4">
                        <div class="font-bold text-slate-100 text-base">${escapeHtml(item.matakuliah)}</div>
                        <div class="text-xs text-emerald-400/80 mt-0.5 flex items-center gap-1.5">
                            <i class="fa-regular fa-calendar text-amber-400"></i> ${formatDateIndonesian(item.tanggal)}
                        </div>
                    </td>
                    <td class="py-4 px-4 text-center">
                        <span class="inline-block px-2.5 py-1 rounded-lg bg-slate-900 text-amber-300 text-xs font-mono font-bold border border-amber-500/30 shadow-sm">
                            ${escapeHtml(item.kelas)}
                        </span>
                    </td>
                    <td class="py-4 px-4">
                        <div class="font-semibold text-slate-200 flex items-center gap-2">
                            <i class="fa-solid fa-user-tie text-emerald-400 text-xs"></i>
                            ${escapeHtml(item.nama_dosen)}
                        </div>
                    </td>
                    <td class="py-4 px-4 text-center">
                        <span class="font-mono font-bold text-slate-200 bg-slate-900/90 px-2.5 py-1 rounded-md border border-emerald-900 inline-flex items-center gap-1.5">
                            <i class="fa-regular fa-clock text-emerald-400 text-xs"></i>
                            ${escapeHtml(item.waktu)}
                        </span>
                    </td>
                    <td class="py-4 px-4 text-center">
                        <span class="inline-block px-3 py-1 rounded-xl bg-emerald-950/90 text-emerald-300 font-bold text-xs border border-emerald-700 shadow-inner">
                            <i class="fa-solid fa-location-dot mr-1 text-amber-400"></i> ${escapeHtml(item.ruang)}
                        </span>
                    </td>
                    <td class="py-4 px-4">
                        <span class="text-xs font-semibold px-2.5 py-1 rounded-md bg-slate-800/80 text-slate-300 border border-slate-700/60 inline-block">
                            ${escapeHtml(item.prodi)}
                        </span>
                    </td>
                    <td class="py-4 px-4 text-center">
                        ${statusInfo.badgeHtml}
                    </td>
                `;
                tbody.appendChild(tr);
            });
        }

        function calculateTimeStatus(item) {
            const dateStr = item.tanggal;
            const timeRangeStr = item.waktu;
            const checklistVal = (item.checklist || '').trim().toLowerCase();
            const isChecked = checklistVal === 'v' || checklistVal === 'yes' || checklistVal === '1' || checklistVal === 'true' || checklistVal === 'hadir' || checklistVal === 'x';
            
            const todayStr = getTodayYYYYMMDD();
            const normDate = normalizeDate(dateStr);

            if (normDate > todayStr) {
                return {
                    code: 'UPCOMING',
                    badgeHtml: `<span class="px-2.5 py-1 rounded-full bg-teal-500/10 text-teal-300 border border-teal-500/30 text-xs font-bold inline-flex items-center gap-1">
                                    <i class="fa-solid fa-circle text-[8px]"></i> Akan Datang
                                </span>`
                };
            }
            if (normDate < todayStr) {
                return {
                    code: 'COMPLETED',
                    badgeHtml: `<span class="px-2.5 py-1 rounded-full bg-slate-800 text-slate-400 border border-slate-700 text-xs font-medium inline-flex items-center gap-1">
                                    <i class="fa-solid fa-check text-[10px]"></i> Selesai
                                </span>`
                };
            }

            const times = timeRangeStr.split('-').map(t => t.trim());
            if (times.length < 2) {
                return {
                    code: 'UPCOMING',
                    badgeHtml: `<span class="px-2.5 py-1 rounded-full bg-teal-500/10 text-teal-300 border border-teal-500/30 text-xs font-bold">Hari Ini</span>`
                };
            }

            const now = new Date();
            const currentMinutes = now.getHours() * 60 + now.getMinutes();

            const startMinutes = parseTimeToMinutes(times[0]);
            const endMinutes = parseTimeToMinutes(times[1]);

            if (currentMinutes >= startMinutes && currentMinutes <= endMinutes) {
                if (isChecked) {
                    return {
                        code: 'ACTIVE',
                        badgeHtml: `<span class="px-3 py-1 rounded-full bg-amber-500 text-slate-950 font-black text-xs inline-flex items-center gap-1.5 shadow-[0_0_12px_rgba(253,184,19,0.5)] animate-pulse">
                                        <i class="fa-solid fa-circle-play"></i> BERLANGSUNG
                                    </span>`
                    };
                } else {
                    return {
                        code: 'UNCHECKED_ACTIVE',
                        badgeHtml: `<span class="px-2.5 py-1 rounded-full bg-rose-950 text-rose-300 font-bold text-xs border border-rose-700 inline-flex items-center gap-1">
                                        <i class="fa-solid fa-user-xmark"></i> Belum Hadir
                                    </span>`
                    };
                }
            } else if (currentMinutes < startMinutes) {
                return {
                    code: 'UPCOMING',
                    badgeHtml: `<span class="px-2.5 py-1 rounded-full bg-teal-500/10 text-teal-300 border border-teal-500/30 text-xs font-bold inline-flex items-center gap-1">
                                    <i class="fa-solid fa-clock"></i> Akan Datang
                                </span>`
                };
            } else {
                return {
                    code: 'COMPLETED',
                    badgeHtml: `<span class="px-2.5 py-1 rounded-full bg-slate-800 text-slate-400 border border-slate-700 text-xs font-medium inline-flex items-center gap-1">
                                    <i class="fa-solid fa-check text-[10px]"></i> Selesai
                                </span>`
                };
            }
        }

        function parseTimeToMinutes(timeStr) {
            if (!timeStr) return 0;
            const parts = timeStr.split(':').map(p => parseInt(p.trim(), 10));
            if (parts.length >= 2 && !isNaN(parts[0]) && !isNaN(parts[1])) {
                return parts[0] * 60 + parts[1];
            }
            return 0;
        }

        function updateSummaryCounters() {
            let total = appState.filteredSchedules.length;
            let active = 0;
            let upcoming = 0;
            let completed = 0;

            appState.filteredSchedules.forEach(item => {
                const st = calculateTimeStatus(item).code;
                if (st === 'ACTIVE') active++;
                else if (st === 'UPCOMING' || st === 'PENDING' || st === 'UNCHECKED_ACTIVE') upcoming++;
                else if (st === 'COMPLETED') completed++;
            });

            document.getElementById('stat-total').innerText = total;
            document.getElementById('stat-active').innerText = active;
            document.getElementById('stat-upcoming').innerText = upcoming;
            document.getElementById('stat-completed').innerText = completed;
        }

        function populateProdiDropdown() {
            const select = document.getElementById('filter-prodi');
            if (!select) return;

            const currentVal = select.value;
            const prodiSet = new Set();
            
            appState.schedules.forEach(item => {
                if (item.prodi && item.prodi.trim() !== '') {
                    prodiSet.add(item.prodi.trim());
                }
            });

            select.innerHTML = '<option value="ALL">Semua Program Studi</option>';
            prodiSet.forEach(prodi => {
                const opt = document.createElement('option');
                opt.value = prodi;
                opt.innerText = prodi;
                select.appendChild(opt);
            });

            select.value = currentVal;
        }

        function openSettingsModal() {
            document.getElementById('input-sheet-url').value = appState.sheetUrl || '';
            document.getElementById('input-running-text').value = appState.runningText || '';
            document.getElementById('input-refresh-interval').value = appState.refreshInterval;

            const resultEl = document.getElementById('modal-test-result');
            if (resultEl) resultEl.className = 'hidden';

            document.getElementById('settings-modal').classList.remove('hidden');
        }

        function closeSettingsModal() {
            document.getElementById('settings-modal').classList.add('hidden');
        }

        function openHelpModal() {
            document.getElementById('help-modal').classList.remove('hidden');
        }

        function closeHelpModal() {
            document.getElementById('help-modal').classList.add('hidden');
        }

        function showErrorBanner(msg) {
            const banner = document.getElementById('connection-error-banner');
            const msgEl = document.getElementById('error-banner-message');
            if (banner && msgEl) {
                msgEl.innerText = msg;
                banner.classList.remove('hidden');
            }
        }

        function dismissErrorBanner() {
            const banner = document.getElementById('connection-error-banner');
            if (banner) banner.classList.add('hidden');
        }

        function saveSettings() {
            appState.sheetUrl = document.getElementById('input-sheet-url').value.trim();
            appState.runningText = document.getElementById('input-running-text').value.trim();
            appState.refreshInterval = parseInt(document.getElementById('input-refresh-interval').value, 10);

            localStorage.setItem(STORAGE_KEY_CONFIG, JSON.stringify({
                sheetUrl: appState.sheetUrl,
                runningText: appState.runningText,
                refreshInterval: appState.refreshInterval
            }));

            const runningEl = document.getElementById('running-text-content');
            if (runningEl) runningEl.innerText = appState.runningText || '📢 PENGUMUMAN UNIVERSITAS NASIONAL';

            setupAutoRefreshTimer();

            if (appState.sheetUrl) {
                fetchSpreadsheetData();
            } else {
                loadSampleData();
            }

            closeSettingsModal();
        }

        function loadSavedConfig() {
            try {
                const saved = localStorage.getItem(STORAGE_KEY_CONFIG);
                if (saved) {
                    const parsed = JSON.parse(saved);
                    appState.sheetUrl = parsed.sheetUrl || appState.sheetUrl;
                    appState.runningText = parsed.runningText || appState.runningText;
                    appState.refreshInterval = parsed.refreshInterval !== undefined ? parsed.refreshInterval : 30000;
                }
            } catch (e) {
                console.warn("Error loading config:", e);
            }

            const runningEl = document.getElementById('running-text-content');
            if (runningEl) runningEl.innerText = appState.runningText;

            updateIntervalLabel();
        }

        function loadSampleData() {
            appState.schedules = [...SAMPLE_DATA_UNAS];
            populateProdiDropdown();
            applyFilters();
            updateSyncBadge(true, "Demo");
            dismissErrorBanner();
        }

        function setupAutoRefreshTimer() {
            if (appState.autoRefreshTimer) clearInterval(appState.autoRefreshTimer);
            updateIntervalLabel();

            if (appState.refreshInterval > 0) {
                appState.autoRefreshTimer = setInterval(() => {
                    if (appState.sheetUrl) {
                        fetchSpreadsheetData();
                    }
                }, appState.refreshInterval);
            }
        }

        function updateIntervalLabel() {
            const label = document.getElementById('refresh-interval-label');
            if (!label) return;
            if (appState.refreshInterval === 0) {
                label.innerText = 'Matikan (Manual)';
            } else if (appState.refreshInterval < 60000) {
                label.innerText = `${appState.refreshInterval / 1000} detik`;
            } else {
                label.innerText = `${appState.refreshInterval / 60000} menit`;
            }
        }

        function updateSyncBadge(isOk, text) {
            const syncText = document.getElementById('sync-status-text');
            const syncEl = document.getElementById('sync-status');
            if (!syncEl || !syncText) return;

            syncText.innerText = text;
            if (isOk) {
                syncEl.className = 'flex items-center gap-1.5 px-2.5 py-1 rounded-lg bg-emerald-950/80 border border-emerald-700 text-emerald-300';
            } else {
                syncEl.className = 'flex items-center gap-1.5 px-2.5 py-1 rounded-lg bg-rose-950/80 border border-rose-800 text-rose-300';
            }
        }

        function toggleFullscreen() {
            if (!document.fullscreenElement) {
                document.documentElement.requestFullscreen().catch(err => {
                    console.log(`Error mode layar penuh: ${err.message}`);
                });
            } else {
                if (document.exitFullscreen) {
                    document.exitFullscreen();
                }
            }
        }

        function getTodayYYYYMMDD() {
            const today = new Date();
            const year = today.getFullYear();
            const month = String(today.getMonth() + 1).padStart(2, '0');
            const day = String(today.getDate()).padStart(2, '0');
            return `${year}-${month}-${day}`;
        }

        function getOffsetYYYYMMDD(offsetDays) {
            const d = new Date();
            d.setDate(d.getDate() + offsetDays);
            const year = d.getFullYear();
            const month = String(d.getMonth() + 1).padStart(2, '0');
            const day = String(d.getDate()).padStart(2, '0');
            return `${year}-${month}-${day}`;
        }

        function normalizeDate(str) {
            if (!str) return getTodayYYYYMMDD();
            const cleanStr = str.trim();
            if (cleanStr.includes('/')) {
                const parts = cleanStr.split('/');
                if (parts.length === 3) {
                    if (parts[0].length === 4) return `${parts[0]}-${parts[1].padStart(2, '0')}-${parts[2].padStart(2, '0')}`;
                    return `${parts[2]}-${parts[1].padStart(2, '0')}-${parts[0].padStart(2, '0')}`;
                }
            }
            return cleanStr;
        }

        function formatDateIndonesian(dateStr) {
            if (!dateStr) return '-';
            const norm = normalizeDate(dateStr);
            const parts = norm.split('-');
            if (parts.length < 3) return dateStr;

            const d = new Date(parts[0], parts[1] - 1, parts[2]);
            if (isNaN(d.getTime())) return dateStr;

            const months = ['Januari', 'Februari', 'Maret', 'April', 'Mei', 'Juni', 'Juli', 'Agustus', 'September', 'Oktober', 'November', 'Desember'];
            return `${d.getDate()} ${months[d.getMonth()]} ${d.getFullYear()}`;
        }

        function escapeHtml(text) {
            if (!text) return '';
            return String(text)
                .replace(/&/g, "&amp;")
                .replace(/</g, "&lt;")
                .replace(/>/g, "&gt;")
                .replace(/"/g, "&quot;")
                .replace(/'/g, "&#039;");
        }
    </script>
</body>
</html>