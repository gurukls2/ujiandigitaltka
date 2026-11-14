<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Uji Coba TKA - UPT SD Negeri Mlangi 2 Tahun 2027</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome untuk ikon antarmuka CBT -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        /* Pengaturan Font Khusus Sesuai Spesifikasi */
        .font-judul-tka {
            font-family: 'Arial Nova Cond', 'Arial Narrow', 'Roboto Condensed', Arial, sans-serif;
            letter-spacing: 0.5px;
        }

        /* Tipografi Area Soal (Arial 11pt & Sumber Arial 8pt Italic) */
        .soal-typography {
            font-family: Arial, Helvetica, sans-serif !important;
            font-size: 11pt !important;
            line-height: 1.6;
            color: #1e293b;
        }

        .sumber-typography {
            font-family: Arial, Helvetica, sans-serif !important;
            font-size: 8pt !important;
            font-style: italic !important;
            color: #475569;
            margin-top: 8px;
            display: block;
        }

        .sumber-link {
            color: #0000EE !important;
            text-decoration: underline;
            word-break: break-all;
        }

        /* Animasi halus */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(8px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-fade-in {
            animation: fadeIn 0.3s ease-out forwards;
        }

        /* Custom Scrollbar untuk kenyamanan membaca stimulus panjang */
        ::-webkit-scrollbar {
            width: 7px;
            height: 7px;
        }
        ::-webkit-scrollbar-track {
            background: #f1f5f9;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #94a3b8;
        }

        /* Efek kamera pengawas */
        .mirror-video {
            transform: scaleX(-1);
        }
    </style>
</head>
<body class="bg-slate-100 text-slate-800 min-h-screen flex flex-col select-none">

    <!-- =====================================================================
         HALAMAN 1: LOGIN / IDENTITAS PESERTA & IZIN KAMERA PENGAWAS
         ===================================================================== -->
    <div id="page-login" class="flex-grow flex flex-col justify-between p-4 sm:p-6 md:p-8 relative min-h-screen bg-gradient-to-br from-blue-50 via-slate-50 to-indigo-50">
        
        <!-- Header Judul Rata Tengah dengan Font Arial Nova Cond -->
        <header class="w-full max-w-4xl mx-auto text-center pt-4 pb-6">
            <div class="inline-flex items-center justify-center w-16 h-16 rounded-2xl bg-blue-700 text-white shadow-lg mb-4">
                <i class="fas fa-graduation-cap text-3xl"></i>
            </div>
            <h1 class="font-judul-tka text-2xl sm:text-3xl md:text-4xl font-bold text-blue-950 uppercase tracking-wide leading-tight">
                UJI COBA TES KEMAMPUAN AKADEMIK (TKA)<br>
                <span class="text-blue-700">UPT SD NEGERI MLANGI 2 TAHUN 2027</span>
            </h1>
            <div class="w-32 h-1.5 bg-blue-600 mx-auto mt-3 rounded-full"></div>
        </header>

        <!-- Kontainer Utama Form & Kamera -->
        <main class="w-full max-w-4xl mx-auto my-auto">
            <div class="bg-white rounded-2xl shadow-xl border border-slate-200 overflow-hidden grid grid-cols-1 md:grid-cols-12">
                
                <!-- Kolom Kiri: Pengaturan Kamera Pengawas -->
                <div class="md:col-span-5 bg-slate-900 text-white p-6 flex flex-col justify-between items-center text-center relative">
                    <div class="w-full">
                        <span class="inline-block px-3 py-1 bg-blue-600/30 border border-blue-400/30 text-blue-200 text-xs font-semibold rounded-full mb-2">
                            <i class="fas fa-video mr-1"></i> Sistem Pengawasan Ujian
                        </span>
                        <h2 class="text-base font-semibold text-slate-100">Kamera Pengawas Peserta</h2>
                        <p class="text-xs text-slate-400 mt-1">Wajib diaktifkan sebelum memulai ujian sebagai bukti kehadiran peserta.</p>
                    </div>

                    <!-- Preview Kamera Awal -->
                    <div class="w-full aspect-video max-w-[260px] bg-slate-800 rounded-xl border-2 border-slate-700 overflow-hidden my-4 relative flex items-center justify-center shadow-inner">
                        <video id="login-video-preview" autoplay playsinline muted class="w-full h-full object-cover mirror-video hidden"></video>
                        
                        <!-- Placeholder Sebelum Kamera Menyala -->
                        <div id="login-cam-placeholder" class="flex flex-col items-center justify-center p-4 text-slate-400">
                            <i class="fas fa-user-shield text-4xl mb-2 text-slate-500"></i>
                            <span class="text-xs">Kamera Belum Aktif</span>
                        </div>

                        <!-- Mode Simulasi Kamera (Fallback jika perangkat tidak memiliki webcam) -->
                        <div id="login-cam-simulation" class="hidden flex-col items-center justify-center w-full h-full bg-gradient-to-b from-slate-700 to-slate-800 text-emerald-300 p-3">
                            <div class="w-12 h-12 rounded-full bg-emerald-500/20 border border-emerald-400 flex items-center justify-center mb-1 animate-pulse">
                                <i class="fas fa-user-check text-xl"></i>
                            </div>
                            <span class="text-[11px] font-semibold">Mode Pengawas Simulasi Aktif</span>
                            <span class="text-[9px] text-slate-300 mt-0.5">Perangkat tanpa webcam terdeteksi</span>
                        </div>

                        <!-- Indikator REC -->
                        <div id="login-rec-badge" class="hidden absolute top-2 left-2 bg-red-600 text-white text-[10px] font-bold px-2 py-0.5 rounded-md flex items-center gap-1 shadow">
                            <span class="w-2 h-2 rounded-full bg-white animate-ping"></span> AKTIF
                        </div>
                    </div>

                    <div class="w-full space-y-2">
                        <button type="button" id="btn-enable-camera" onclick="requestCameraAccess()" class="w-full py-2.5 px-4 bg-emerald-600 hover:bg-emerald-500 active:bg-emerald-700 text-white font-semibold text-sm rounded-xl shadow transition flex items-center justify-center gap-2 cursor-pointer">
                            <i class="fas fa-camera"></i>
                            <span>Nyalakan Kamera Pengawas</span>
                        </button>
                        <p id="camera-status-text" class="text-[11px] text-amber-300 min-h-[16px]">
                            *Klik tombol di atas untuk memberikan izin kamera.
                        </p>
                    </div>
                </div>

                <!-- Kolom Kanan: Form Identitas Peserta -->
                <div class="md:col-span-7 p-6 sm:p-8 flex flex-col justify-center">
                    <div class="mb-5">
                        <h3 class="text-xl font-bold text-slate-800">Data Peserta Ujian</h3>
                        <p class="text-sm text-slate-500">Silakan lengkapi identitas diri dan masukkan token ujian.</p>
                    </div>

                    <!-- Kotak Peringatan Error / Token Salah -->
                    <div id="login-error-box" class="hidden mb-4 p-3.5 rounded-xl bg-red-50 border border-red-300 text-red-700 text-sm flex items-start gap-2.5 animate-fade-in">
                        <i class="fas fa-exclamation-triangle text-red-600 mt-0.5"></i>
                        <span id="login-error-msg" class="font-medium"></span>
                    </div>

                    <form id="login-form" onsubmit="handleLoginSubmit(event)" class="space-y-4">
                        <div>
                            <label for="input-nama" class="block text-sm font-semibold text-slate-700 mb-1">
                                Nama Lengkap Peserta <span class="text-red-500">*</span>
                            </label>
                            <div class="relative">
                                <span class="absolute inset-y-0 left-0 pl-3.5 flex items-center text-slate-400">
                                    <i class="fas fa-user"></i>
                                </span>
                                <input type="text" id="input-nama" placeholder="Masukkan nama lengkap Anda" required
                                    class="w-full pl-10 pr-4 py-2.5 bg-slate-50 border border-slate-300 rounded-xl text-slate-800 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:bg-white transition">
                            </div>
                        </div>

                        <div>
                            <label for="input-nisn" class="block text-sm font-semibold text-slate-700 mb-1">
                                NISN (Nomor Induk Siswa Nasional) <span class="text-red-500">*</span>
                            </label>
                            <div class="relative">
                                <span class="absolute inset-y-0 left-0 pl-3.5 flex items-center text-slate-400">
                                    <i class="fas fa-id-card"></i>
                                </span>
                                <input type="text" id="input-nisn" inputmode="numeric" placeholder="Contoh: 0145678910" required
                                    class="w-full pl-10 pr-4 py-2.5 bg-slate-50 border border-slate-300 rounded-xl text-slate-800 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:bg-white transition">
                            </div>
                        </div>

                        <div>
                            <label for="input-token" class="block text-sm font-semibold text-slate-700 mb-1">
                                Token Ujian <span class="text-red-500">*</span>
                            </label>
                            <div class="relative">
                                <span class="absolute inset-y-0 left-0 pl-3.5 flex items-center text-slate-400">
