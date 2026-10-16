<!DOCTYPE html>
<html lang="id" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portir Lapas Kembangkuning</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        lapas: {
                            50: '#fdf8f6',
                            100: '#f2e8e5',
                            500: '#b91c1c',
                            600: '#991b1b',
                            700: '#7f1d1d',
                            800: '#691b1b',
                            900: '#450a0a',
                        }
                    }
                }
            }
        }
    </script>
    <!-- FontAwesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Google Fonts Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; }
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: transparent; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 9999px; }
        .dark ::-webkit-scrollbar-thumb { background: #475569; }
    </style>
</head>
<body class="bg-slate-100 dark:bg-slate-900 text-slate-800 dark:text-slate-100 min-h-screen flex flex-col transition-colors duration-200">

    <!-- Top Navigation Bar -->
    <header class="bg-white dark:bg-slate-800 border-b border-slate-200 dark:border-slate-700 sticky top-0 z-30 shadow-sm">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
            <div class="flex items-center space-x-3">
                <div class="bg-lapas-600 text-white p-2.5 rounded-xl shadow-md flex items-center justify-center">
                    <i class="fa-solid fa-shield-halved text-xl"></i>
                </div>
                <div>
                    <h1 class="text-lg font-bold tracking-tight text-slate-900 dark:text-white leading-tight">PORTIR LAPAS KEMBANGKUNING</h1>
                    <p class="text-xs text-slate-500 dark:text-slate-400">Pengawasan Keluar-Masuk WBP Pekerja Asimilasi Luar Lapas</p>
                </div>
            </div>
            
            <div class="flex items-center space-x-3">
                <div class="hidden md:flex items-center space-x-2 bg-slate-100 dark:bg-slate-700 px-3 py-1.5 rounded-lg text-sm font-medium">
                    <i class="fa-regular fa-clock text-lapas-600 dark:text-lapas-400"></i>
                    <span id="live-clock">--:--:--</span>
                </div>

                <button onclick="toggleDarkMode()" class="p-2 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition" title="Ubah Tema">
                    <i id="theme-icon" class="fa-solid fa-moon"></i>
                </button>

                <button onclick="switchTab('alarm')" class="relative p-2 rounded-lg text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition" title="Peringatan Waktu">
                    <i class="fa-solid fa-bell"></i>
                    <span id="notif-badge" class="absolute top-1 right-1 bg-lapas-600 text-white text-[10px] w-4 h-4 rounded-full flex items-center justify-center font-bold hidden">0</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Main Container -->
    <div class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-6 flex flex-col md:flex-row gap-6">

        <!-- Sidebar Navigation -->
        <aside class="w-full md:w-64 shrink-0">
            <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-3 space-y-1">
                <button onclick="switchTab('dashboard')" id="nav-dashboard" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium transition tab-btn active bg-lapas-600 text-white shadow-sm">
                    <i class="fa-solid fa-chart-pie w-5 text-center"></i>
                    <span>Dashboard Utama</span>
                </button>
                <button onclick="switchTab('keluar')" id="nav-keluar" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition tab-btn">
                    <i class="fa-solid fa-users-viewfinder w-5 text-center"></i>
                    <span>Keluar Rombongan</span>
                </button>
                <button onclick="switchTab('masuk')" id="nav-masuk" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition tab-btn">
                    <i class="fa-solid fa-list-check w-5 text-center"></i>
                    <span>Presensi Masuk (Kembali)</span>
                </button>
                <button onclick="switchTab('warga')" id="nav-warga" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition tab-btn">
                    <i class="fa-solid fa-users-between-lines w-5 text-center"></i>
                    <span>Data Master WBP</span>
                </button>
                <button onclick="switchTab('riwayat')" id="nav-riwayat" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition tab-btn">
                    <i class="fa-solid fa-clock-rotate-left w-5 text-center"></i>
                    <span>Sesi & Log Rombongan</span>
                </button>
                <button onclick="switchTab('alarm')" id="nav-alarm" class="w-full flex items-center space-x-3 px-4 py-3 rounded-lg text-sm font-medium text-slate-600 dark:text-slate-300 hover:bg-slate-100 dark:hover:bg-slate-700 transition tab-btn justify-between">
                    <div class="flex items-center space-x-3">
                        <i class="fa-solid fa-triangle-exclamation w-5 text-center"></i>
                        <span>Alarm / Keterlambatan</span>
                    </div>
                    <span id="alarm-count-pill" class="bg-amber-100 text-amber-800 dark:bg-amber-900/50 dark:text-amber-300 text-xs px-2 py-0.5 rounded-full font-bold">0</span>
                </button>
            </div>

            <div class="mt-4 bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-4 text-xs space-y-2">
                <div class="font-bold text-slate-900 dark:text-white uppercase tracking-wider flex items-center justify-between">
                    <span>Petugas Regu Portir</span>
                    <span class="inline-block w-2 h-2 rounded-full bg-emerald-500 animate-pulse"></span>
                </div>
                <div class="text-slate-600 dark:text-slate-400 space-y-1">
                    <p><span class="font-semibold text-slate-700 dark:text-slate-300">Komandan Portir:</span> Petugas Regu Jaga</p>
                    <p><span class="font-semibold text-slate-700 dark:text-slate-300">Pintu Utama (P2U):</span> Petugas Portir Lapas</p>
                </div>
            </div>
        </aside>

        <!-- Dynamic Content Area -->
        <main class="flex-1">

            <!-- TAB 1: DASHBOARD -->
            <section id="tab-dashboard" class="tab-content space-y-6">
                <div class="bg-gradient-to-r from-slate-900 via-slate-800 to-slate-900 text-white rounded-2xl p-6 shadow-md relative overflow-hidden">
                    <div class="absolute right-0 bottom-0 opacity-10 translate-x-4 translate-y-4">
                        <i class="fa-solid fa-building-shield text-9xl"></i>
                    </div>
                    <div class="relative z-10">
                        <span class="bg-lapas-600 text-white text-xs px-3 py-1 rounded-full font-semibold uppercase tracking-wider">Portir Lapas Kelas IIA Kembangkuning</span>
                        <h2 class="text-2xl font-bold mt-2">Pencatatan Rombongan Pekerja Asimilasi</h2>
                        <p class="text-slate-300 text-sm mt-1">Kontrol presensi pengeluaran dan pemasukan WBP Pekerja (Peternakan Kambing, Perikanan, Greenhouse, TPA, Kebersihan).</p>
                        
                        <div class="mt-6 flex flex-wrap gap-3">
                            <button onclick="switchTab('keluar')" class="bg-white text-slate-900 hover:bg-slate-100 px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                <i class="fa-solid fa-user-plus text-lapas-600"></i>
                                <span>Izin Keluar Rombongan</span>
                            </button>
                            <button onclick="switchTab('masuk')" class="bg-lapas-600 hover:bg-lapas-700 text-white px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                <i class="fa-solid fa-list-check"></i>
                                <span>Presensi Kembali (Pintu P2U)</span>
                            </button>
                        </div>
                    </div>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Total WBP Pekerja</p>
                            <h3 id="stat-total-wbp" class="text-3xl font-bold text-slate-900 dark:text-white mt-1">0</h3>
                            <span class="text-xs text-slate-500 mt-1 inline-block">Terdata di Master</span>
                        </div>
                        <div class="bg-blue-50 dark:bg-blue-900/30 text-blue-600 dark:text-blue-400 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-id-card"></i>
                        </div>
                    </div>

                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Sedang di Luar Area</p>
                            <h3 id="stat-sedang-luar" class="text-3xl font-bold text-amber-600 dark:text-amber-400 mt-1">0</h3>
                            <span class="text-xs text-amber-600 dark:text-amber-400 font-medium mt-1 inline-block"><i class="fa-solid fa-person-walking-arrow-right"></i> Bekerja Asimilasi</span>
                        </div>
                        <div class="bg-amber-50 dark:bg-amber-900/30 text-amber-600 dark:text-amber-400 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-users"></i>
                        </div>
                    </div>

                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Di Dalam Lapas</p>
                            <h3 id="stat-dalam-lapas" class="text-3xl font-bold text-emerald-600 dark:text-emerald-400 mt-1">0</h3>
                            <span class="text-xs text-emerald-600 dark:text-emerald-400 font-medium mt-1 inline-block"><i class="fa-solid fa-house-lock"></i> Ada di Dalam</span>
                        </div>
                        <div class="bg-emerald-50 dark:bg-emerald-900/30 text-emerald-600 dark:text-emerald-400 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-building-user"></i>
                        </div>
                    </div>

                    <div class="bg-white dark:bg-slate-800 p-5 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 flex items-center justify-between">
                        <div>
                            <p class="text-xs font-medium text-slate-500 dark:text-slate-400 uppercase tracking-wider">Sesi Tugas Aktif</p>
                            <h3 id="stat-sesi-aktif" class="text-3xl font-bold text-lapas-600 dark:text-lapas-500 mt-1">0</h3>
                            <span class="text-xs text-slate-500 mt-1 inline-block">Kelompok Rombongan</span>
                        </div>
                        <div class="bg-red-50 dark:bg-red-900/30 text-lapas-600 dark:text-lapas-500 p-3.5 rounded-xl text-xl">
                            <i class="fa-solid fa-layer-group"></i>
                        </div>
                    </div>
                </div>

                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="flex items-center justify-between mb-4">
                        <h3 class="font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-list-check text-lapas-600"></i>
                            <span>Daftar Sesi Rombongan Yang Sedang Bertugas Di Luar</span>
                        </h3>
                        <button onclick="switchTab('riwayat')" class="text-xs text-lapas-600 hover:underline font-semibold">Lihat Semua Log</button>
                    </div>
                    
                    <div id="dashboard-active-sessions" class="space-y-4"></div>
                </div>
            </section>

            <!-- TAB 2: FORM KELUAR ROMBONGAN -->
            <section id="tab-keluar" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-users-viewfinder text-lapas-600"></i>
                            <span>Form Izin Keluar Rombongan WBP Asimilasi</span>
                        </h2>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Pilih beberapa WBP pekerja sekaligus sesuai bidang penugasan kerja luar.</p>
                    </div>

                    <form id="form-bulk-out" onsubmit="handleBulkCheckout(event)" class="space-y-6">
                        <div class="grid grid-cols-1 md:grid-cols-3 gap-4 bg-slate-50 dark:bg-slate-700/40 p-4 rounded-xl border border-slate-200 dark:border-slate-700">
                            <div>
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Bidang Penugasan / Kerja *</label>
                                <select id="out-category" onchange="toggleCustomCategoryInput()" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                    <option value="Lahan Peternakan Kambing">Lahan Peternakan Kambing</option>
                                    <option value="Pengolah Pakan Kambing">Pengolah Pakan Kambing</option>
                                    <option value="Laundry & Greenhouse">Laundry & Greenhouse</option>
                                    <option value="Pembangunan / Operasional TPA">Pembangunan / Operasional TPA</option>
                                    <option value="Asimilasi Perikanan / Tambak">Asimilasi Perikanan / Tambak</option>
                                    <option value="Pertanian / Perkebunan">Pertanian / Perkebunan</option>
                                    <option value="Dan / Lain-lain">Dan / Lain-lain (Ketik Manual)</option>
                                </select>
                                <input type="text" id="out-custom-category" placeholder="Tuliskan nama kegiatan..." class="w-full mt-2 px-3 py-1.5 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-sm hidden">
                            </div>

                            <div>
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Jam Keluar *</label>
                                <input type="time" id="out-time" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                            </div>

                            <div>
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Batas Jam Kembali *</label>
                                <input type="time" id="out-limit-time" value="16:00" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                            </div>

                            <div class="md:col-span-2">
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Petugas Pengawal / Penanggung Jawab *</label>
                                <input type="text" id="out-officer-escort" placeholder="Contoh: Staf Seksi Kegiatan Kerja / Pengawal Asimilasi" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                            </div>

                            <div>
                                <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Lokasi Kegiatan</label>
                                <input type="text" id="out-location" placeholder="Area Peternakan Kambing & TPA Lapas Kembangkuning" class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                            </div>
                        </div>

                        <div class="space-y-3">
                            <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-2">
                                <div>
                                    <h3 class="font-bold text-sm text-slate-900 dark:text-white flex items-center space-x-2">
                                        <i class="fa-solid fa-square-check text-lapas-600"></i>
                                        <span>Pilih Warga Binaan (Tersedia: <span id="out-available-count">0</span> WBP)</span>
                                    </h3>
                                    <p class="text-xs text-slate-500">Centang nama WBP yang akan dikeluarkan pada sesi ini.</p>
                                </div>
                                <div class="flex items-center space-x-2">
                                    <button type="button" onclick="selectAllAvailableOutWbp(true)" class="px-2.5 py-1 text-xs rounded bg-blue-100 text-blue-700 dark:bg-blue-900/50 dark:text-blue-300 font-medium">Centang Semua</button>
                                    <button type="button" onclick="selectAllAvailableOutWbp(false)" class="px-2.5 py-1 text-xs rounded bg-slate-200 text-slate-700 dark:bg-slate-700 dark:text-slate-300">Kosongkan</button>
                                </div>
                            </div>

                            <input type="text" id="out-wbp-filter" onkeyup="renderOutWbpSelectionList()" placeholder="Ketik nama atau No. Registrasi WBP..." class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">

                            <div id="out-wbp-checkbox-grid" class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-3 max-h-80 overflow-y-auto p-3 bg-slate-50 dark:bg-slate-900/40 rounded-xl border border-slate-200 dark:border-slate-700"></div>
                            
                            <div class="text-xs text-slate-600 dark:text-slate-400 font-semibold flex items-center justify-between">
                                <span>Terpilih: <strong id="out-selected-count" class="text-lapas-600 dark:text-lapas-400 text-sm">0</strong> WBP</span>
                            </div>
                        </div>

                        <div class="flex justify-end space-x-3 pt-4 border-t border-slate-200 dark:border-slate-700">
                            <button type="submit" class="bg-lapas-600 hover:bg-lapas-700 text-white px-6 py-2.5 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                <i class="fa-solid fa-receipt"></i>
                                <span>Proses Keluar & Cetak Surat Jalan</span>
                            </button>
                        </div>
                    </form>
                </div>
            </section>

            <!-- TAB 3: FORM PRESENSI MASUK -->
            <section id="tab-masuk" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-list-check text-lapas-600"></i>
                            <span>Presensi Masuk & Penggeledahan Portir (P2U)</span>
                        </h2>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Lakukan pemanggilan & centang WBP yang telah kembali ke pos portir.</p>
                    </div>

                    <div class="space-y-5">
                        <div>
                            <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Pilih Sesi Rombongan Aktif *</label>
                            <select id="in-session-select" onchange="loadSessionForCheckin()" class="w-full px-3.5 py-2.5 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                <option value="">-- Pilih Sesi Rombongan Yang Sedang Bekerja --</option>
                            </select>
                        </div>

                        <div id="in-session-detail-container" class="hidden space-y-5">
                            <div class="bg-slate-50 dark:bg-slate-700/50 p-4 rounded-xl border border-slate-200 dark:border-slate-700 grid grid-cols-2 md:grid-cols-4 gap-4 text-xs">
                                <div>
                                    <span class="block text-slate-500">Penugasan Kerja</span>
                                    <span id="in-session-category" class="font-bold text-slate-900 dark:text-white text-sm">-</span>
                                </div>
                                <div>
                                    <span class="block text-slate-500">Jam Keluar / Batas</span>
                                    <span id="in-session-times" class="font-bold text-slate-900 dark:text-white text-sm">-</span>
                                </div>
                                <div>
                                    <span class="block text-slate-500">Pengawal / PIC</span>
                                    <span id="in-session-officer" class="font-bold text-slate-900 dark:text-white text-sm">-</span>
                                </div>
                                <div>
                                    <span class="block text-slate-500">Status Waktu</span>
                                    <span id="in-session-status-badge" class="inline-block mt-0.5">-</span>
                                </div>
                            </div>

                            <form id="form-bulk-in" onsubmit="handleBulkCheckin(event)" class="space-y-4">
                                <div class="flex items-center justify-between">
                                    <h3 class="font-bold text-sm text-slate-900 dark:text-white">Daftar Anggota Rombongan (Centang Yang Kembali)</h3>
                                    <div class="space-x-2">
                                        <button type="button" onclick="toggleAllCheckinWbp(true)" class="text-xs bg-emerald-100 text-emerald-800 dark:bg-emerald-900/50 dark:text-emerald-300 px-2.5 py-1 rounded font-semibold">Tandai Semua</button>
                                        <button type="button" onclick="toggleAllCheckinWbp(false)" class="text-xs bg-slate-200 text-slate-700 dark:bg-slate-700 dark:text-slate-300 px-2.5 py-1 rounded">Batal Semua</button>
                                    </div>
                                </div>

                                <div id="in-wbp-checklist-grid" class="grid grid-cols-1 md:grid-cols-2 gap-3 max-h-80 overflow-y-auto p-3 bg-slate-50 dark:bg-slate-900/40 rounded-xl border border-slate-200 dark:border-slate-700"></div>

                                <div class="grid grid-cols-1 md:grid-cols-3 gap-4 pt-2">
                                    <div>
                                        <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Jam Kembali Riil *</label>
                                        <input type="time" id="in-actual-time" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                    </div>
                                    <div>
                                        <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Hasil Penggeledahan P2U *</label>
                                        <select id="in-search-result" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                                            <option value="Aman / Nihil Temuan">Aman / Nihil Temuan Barang Terlarang</option>
                                            <option value="Temuan Barang Dilarang">Ada Temuan Dilarang (Lapor KPLP)</option>
                                            <option value="Catatan Kesehatan">Catatan Kesehatan / Pengobatan</option>
                                        </select>
                                    </div>
                                    <div>
                                        <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Petugas Verifikator Portir *</label>
                                        <input type="text" id="in-officer-name" value="Petugas Portir / P2U Lapas" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-slate-100 dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                                    </div>
                                </div>

                                <div>
                                    <label class="block text-xs font-bold text-slate-700 dark:text-slate-300 uppercase mb-1">Catatan Penggeledahan</label>
                                    <input type="text" id="in-notes" placeholder="Contoh: Badan & peralatan kerja diserahterimakan dalam keadaan aman dan lengkap." class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                                </div>

                                <div class="flex justify-end space-x-3 pt-4 border-t border-slate-200 dark:border-slate-700">
                                    <button type="submit" class="bg-emerald-600 hover:bg-emerald-700 text-white px-6 py-2.5 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                                        <i class="fa-solid fa-clipboard-check"></i>
                                        <span>Simpan Presensi Masuk & Tutup Sesi</span>
                                    </button>
                                </div>
                            </form>
                        </div>
                    </div>
                </div>
            </section>

            <!-- TAB 4: DATA MASTER WBP -->
            <section id="tab-warga" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <div>
                            <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                                <i class="fa-solid fa-users-between-lines text-lapas-600"></i>
                                <span>Master Data WBP Pekerja Asimilasi Lapas Kembangkuning</span>
                            </h2>
                            <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Daftar WBP yang ditetapkan berdasarkan Surat Perintah Kalapas Kembangkuning.</p>
                        </div>
                        <button onclick="openAddWbpModal()" class="bg-lapas-600 hover:bg-lapas-700 text-white px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                            <i class="fa-solid fa-user-plus"></i>
                            <span>Tambah WBP Pekerja</span>
                        </button>
                    </div>

                    <div class="grid grid-cols-1 sm:grid-cols-3 gap-3 mb-4">
                        <input type="text" id="wbp-search" onkeyup="renderWbpTable()" placeholder="Cari nama atau No. Reg..." class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                        <select id="wbp-filter-cat" onchange="renderWbpTable()" class="px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                            <option value="">Semua Penugasan</option>
                            <option value="Lahan Peternakan Kambing">Lahan Peternakan Kambing</option>
                            <option value="Pengolah Pakan Kambing">Pengolah Pakan Kambing</option>
                            <option value="Laundry & Greenhouse">Laundry & Greenhouse</option>
                            <option value="Pembangunan / Operasional TPA">Pembangunan / Operasional TPA</option>
                        </select>
                        <select id="wbp-filter-status" onchange="renderWbpTable()" class="px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none">
                            <option value="">Semua Lokasi Status</option>
                            <option value="Di Lapas">Di Lapas</option>
                            <option value="Di Luar">Di Luar Lapas</option>
                        </select>
                    </div>

                    <div class="overflow-x-auto">
                        <table class="w-full text-left text-sm">
                            <thead class="bg-slate-50 dark:bg-slate-700 text-slate-600 dark:text-slate-300 text-xs uppercase tracking-wider">
                                <tr>
                                    <th class="p-3 rounded-l-lg">No. Reg / ID</th>
                                    <th class="p-3">Nama Lengkap / Alias</th>
                                    <th class="p-3">Kamar / Blok</th>
                                    <th class="p-3">Penugasan Kerja Utama</th>
                                    <th class="p-3">Status Lokasi</th>
                                    <th class="p-3 text-right rounded-r-lg">Aksi</th>
                                </tr>
                            </thead>
                            <tbody id="wbp-table-tbody" class="divide-y divide-slate-100 dark:divide-slate-700"></tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- TAB 5: SESI & LOG ROMBONGAN -->
            <section id="tab-riwayat" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <div>
                            <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                                <i class="fa-solid fa-clock-rotate-left text-lapas-600"></i>
                                <span>Riwayat Sesi Keluar Masuk Rombongan</span>
                            </h2>
                            <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Daftar arsip seluruh kelompok pekerjaan asimilasi yang pernah keluar-masuk portir.</p>
                        </div>
                        <button onclick="exportLogCSV()" class="bg-slate-800 hover:bg-slate-700 text-white px-4 py-2 rounded-lg text-sm font-semibold transition shadow-sm flex items-center space-x-2">
                            <i class="fa-solid fa-file-csv"></i>
                            <span>Export Laporan CSV</span>
                        </button>
                    </div>

                    <div id="session-log-list-container" class="space-y-4"></div>
                </div>
            </section>

            <!-- TAB 6: ALARM / KETERLAMBATAN -->
            <section id="tab-alarm" class="tab-content space-y-6 hidden">
                <div class="bg-white dark:bg-slate-800 rounded-xl shadow-sm border border-slate-200 dark:border-slate-700 p-6">
                    <div class="border-b border-slate-200 dark:border-slate-700 pb-4 mb-6">
                        <h2 class="text-lg font-bold text-slate-900 dark:text-white flex items-center space-x-2">
                            <i class="fa-solid fa-triangle-exclamation text-lapas-600"></i>
                            <span>Peringatan Waktu & Keterlambatan Rombongan</span>
                        </h2>
                        <p class="text-xs text-slate-500 dark:text-slate-400 mt-1">Sesi rombongan WBP yang telah melebihi batas jam kembali.</p>
                    </div>

                    <div id="alarm-container" class="space-y-4"></div>
                </div>
            </section>

        </main>
    </div>

    <!-- MODAL: SURAT JALAN ROMBONGAN -->
    <div id="modal-receipt" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 hidden">
        <div class="bg-white dark:bg-slate-800 rounded-2xl max-w-lg w-full p-6 shadow-2xl border border-slate-200 dark:border-slate-700 space-y-4">
            <div class="text-center pb-3 border-b border-dashed border-slate-300 dark:border-slate-700">
                <div class="inline-block bg-lapas-600 text-white p-3 rounded-full mb-2">
                    <i class="fa-solid fa-stamp text-2xl"></i>
                </div>
                <h3 class="font-bold text-base text-slate-900 dark:text-white">SURAT JALAN ROMBONGAN ASIMILASI</h3>
                <p class="text-xs text-slate-500">Pos Pengamanan Pintu Utama (Portir) Lapas Kelas IIA Kembangkuning</p>
            </div>

            <div id="receipt-content" class="text-xs space-y-3 text-slate-700 dark:text-slate-300"></div>

            <div class="flex space-x-3 pt-3 border-t border-slate-200 dark:border-slate-700">
                <button onclick="closeReceiptModal()" class="flex-1 bg-slate-200 dark:bg-slate-700 text-slate-800 dark:text-white py-2 rounded-lg font-semibold text-sm">Tutup</button>
                <button onclick="window.print()" class="flex-1 bg-lapas-600 text-white py-2 rounded-lg font-semibold text-sm flex items-center justify-center space-x-2">
                    <i class="fa-solid fa-print"></i>
                    <span>Cetak Surat Jalan</span>
                </button>
            </div>
        </div>
    </div>

    <!-- MODAL: ADD WBP -->
    <div id="modal-wbp" class="fixed inset-0 z-50 bg-slate-900/60 backdrop-blur-sm flex items-center justify-center p-4 hidden">
        <div class="bg-white dark:bg-slate-800 rounded-2xl max-w-md w-full p-6 shadow-2xl border border-slate-200 dark:border-slate-700">
            <div class="flex items-center justify-between pb-3 border-b border-slate-200 dark:border-slate-700 mb-4">
                <h3 class="font-bold text-slate-900 dark:text-white">Tambah WBP Pekerja Baru</h3>
                <button onclick="closeModalWbp()" class="text-slate-400 hover:text-slate-600"><i class="fa-solid fa-xmark text-lg"></i></button>
            </div>

            <form onsubmit="saveWbpData(event)" class="space-y-4 text-xs">
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">No. Registrasi / ID *</label>
                    <input type="text" id="new-wbp-id" placeholder="BI. 200/2025" required class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                </div>
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Nama Lengkap WBP *</label>
                    <input type="text" id="new-wbp-name" placeholder="Nama WBP" required class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white">
                </div>
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Bin / Alias</label>
                    <input type="text" id="new-wbp-alias" placeholder="Bin ..." class="w-full px-3 py-2 rounded-lg border border-slate-300 dark:border-slate-
