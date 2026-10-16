<html lang="id" class="light">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Portir Lapas Kembangkuning - Kontrol Asimilasi</title>
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

    <!-- LOGIN SCREEN OVERLAY -->
    <div id="login-modal" class="fixed inset-0 z-50 bg-slate-900/80 backdrop-blur-md flex items-center justify-center p-4">
        <div class="bg-white dark:bg-slate-800 rounded-2xl max-w-md w-full p-8 shadow-2xl border border-slate-200 dark:border-slate-700 space-y-6">
            <div class="text-center space-y-2">
                <div class="inline-block bg-lapas-600 text-white p-3.5 rounded-2xl shadow-md">
                    <i class="fa-solid fa-shield-halved text-2xl"></i>
                </div>
                <h2 class="text-xl font-bold text-slate-900 dark:text-white">PORTIR LAPAS KEMBANGKUNING</h2>
                <p class="text-xs text-slate-500">Silakan login untuk mengakses sistem pengawasan asimilasi.</p>
            </div>

            <form onsubmit="handleLogin(event)" class="space-y-4 text-xs">
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Username / Akun *</label>
                    <input type="text" id="login-user" placeholder="Contoh: admin atau petugas" required class="w-full px-3.5 py-2.5 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                </div>
                <div>
                    <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Password *</label>
                    <input type="password" id="login-pass" placeholder="••••••••" required class="w-full px-3.5 py-2.5 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-sm focus:outline-none focus:ring-2 focus:ring-lapas-600">
                    <p class="text-[10px] text-slate-400 mt-1">Hint: admin (pass: <code>admin123</code>) atau petugas (pass: <code>petugas123</code>)</p>
                </div>
                <div class="grid grid-cols-2 gap-3 pt-2">
                    <div>
                        <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Nama Petugas *</label>
                        <input type="text" id="login-officer-name" placeholder="Bripka H. Kurniawan" required class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-xs">
                    </div>
                    <div>
                        <label class="block font-bold text-slate-700 dark:text-slate-300 mb-1">Shift Tugas *</label>
                        <select id="login-shift" class="w-full px-3.5 py-2 rounded-lg border border-slate-300 dark:border-slate-600 bg-white dark:bg-slate-700 text-slate-900 dark:text-white text-xs">
                            <option value="Shift Pagi (07:00 - 14:00)">Shift Pagi</option>
                            <option value="Shift Siang (14:00 - 21:00)">Shift Siang</option>
                            <option value="Shift Malam (21:00 - 07:00)">Shift Malam</option>
                        </select>
                    </div>
                </div>

                <button type="submit" class="w-full bg-lapas-600 hover:bg-lapas-700 text-white py-3 rounded-xl font-bold text-sm shadow-md transition">
                    Masuk ke Sistem Portir
                </button>
            </form>
        </div>
    </div>

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

                <button onclick="handleLogout()" class="p-2 rounded-lg text-red-600 hover:bg-red-50 dark:hover:bg-red-900/30 transition text-sm font-semibold flex items-center space-x-1" title="Keluar Akun">
                    <i class="fa-solid fa-power-off"></i>
                    <span class="hidden sm:inline text-xs">Logout</span>
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
                    <span id="alarm-count-pill" class
