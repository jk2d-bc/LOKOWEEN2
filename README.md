<!DOCTYPE html>
<html lang="es" class="dark scroll-smooth">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>🎃 LOKOWEEN 2da Edición | La Peda de Disfraces</title>

  <!-- Open Graph Meta Tags (Para vista previa en WhatsApp, Messenger, IG) -->
  <meta property="og:title" content="🎃 LOKOWEEN (2da Edición) — ¡La Peda de Disfraces del Año!">
  <meta property="og:description" content="🗓️ 31 Octubre | ⏰ 8:00 PM | 🎭 Putidisfraz Obligatorio | 🍾 TTP (Trae Tu Pomo). ¡Haz clic para ver detalles!">
  <meta property="og:type" content="website">
  <meta property="og:image" content="https://images.unsplash.com/photo-1508361001413-7a9dca21d08a?auto=format&fit=crop&w=1200&q=80">
  <meta property="og:image:width" content="1200">
  <meta property="og:image:height" content="630">
  <meta name="theme-color" content="#0d0514">

  <!-- Fonts & Icons -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Creepster&family=Plus+Jakarta+Sans:wght@400;600;700;800&family=Orbitron:wght@600;800;900&display=swap" rel="stylesheet">
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Lucide Icons CDN -->
  <script src="https://unpkg.com/lucide@latest"></script>

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            brand: {
              orange: '#ff6600',
              orangeGlow: '#ff4500',
              green: '#00ff66',
              purple: '#8b5cf6',
              darkBg: '#09040e',
              cardBg: 'rgba(18, 9, 28, 0.75)',
            }
          },
          fontFamily: {
            spooky: ['Creepster', 'cursive'],
            tech: ['Orbitron', 'sans-serif'],
            sans: ['Plus Jakarta Sans', 'sans-serif']
          },
          animation: {
            'pulse-glow': 'pulseGlow 2s infinite alternate',
            'float': 'float 4s ease-in-out infinite',
          },
          keyframes: {
            pulseGlow: {
              '0%': { boxShadow: '0 0 15px rgba(255,102,0,0.4), 0 0 30px rgba(255,102,0,0.2)' },
              '100%': { boxShadow: '0 0 25px rgba(0,255,102,0.6), 0 0 50px rgba(0,255,102,0.3)' }
            },
            float: {
              '0%, 100%': { transform: 'translateY(0px)' },
              '50%': { transform: 'translateY(-10px)' }
            }
          }
        }
      }
    }
  </script>

  <style>
    /* Estilos Neón y Vidrio Oscuro */
    .text-glow-orange {
      text-shadow: 0 0 14px rgba(255, 102, 0, 0.9), 0 0 30px rgba(255, 102, 0, 0.6);
    }
    .text-glow-green {
      text-shadow: 0 0 14px rgba(0, 255, 102, 0.9), 0 0 30px rgba(0, 255, 102, 0.6);
    }
    .glass-card {
      background: rgba(14, 7, 24, 0.78);
      backdrop-filter: blur(20px);
      -webkit-backdrop-filter: blur(20px);
      border: 1px solid rgba(255, 102, 0, 0.3);
      box-shadow: 0 8px 32px 0 rgba(0, 0, 0, 0.5);
    }
    .glass-card:hover {
      border-color: rgba(0, 255, 102, 0.6);
    }
    canvas#spookyCanvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      pointer-events: none;
      z-index: 2;
    }
    ::-webkit-scrollbar {
      width: 8px;
    }
    ::-webkit-scrollbar-track {
      background: #09040e;
    }
    ::-webkit-scrollbar-thumb {
      background: #ff6600;
      border-radius: 4px;
    }
  </style>
</head>
<body class="bg-brand-darkBg text-slate-100 font-sans selection:bg-brand-orange selection:text-black min-h-screen relative overflow-x-hidden">

  <!-- VIDEO DE FONDO ESTILO ANTRO / DISCO BALLS -->
  <video autoplay loop muted playsinline id="bgVideo" class="fixed top-0 left-0 w-full h-full object-cover z-0 opacity-45 pointer-events-none scale-105">
    <!-- REEMPLAZA "video.mp4" CON EL NOMBRE DE TU VIDEO EN GITHUB -->
    <source src="video.mp4" type="video/mp4">
    <!-- Video de respaldo mientras subes tu propio archivo -->
    <source src="https://assets.mixkit.co/videos/preview/mixkit-party-lights-and-people-dancing-40348-large.mp4" type="video/mp4">
  </video>

  <!-- OVERLAY OSCURO CON DEGRADADO PARA ASEGURAR LECTURA DE TEXTO -->
  <div class="fixed inset-0 bg-gradient-to-b from-brand-darkBg/80 via-brand-darkBg/65 to-brand-darkBg/90 z-[1] pointer-events-none backdrop-blur-[1px]"></div>

  <!-- PARTICULAS CHISPAS Y NEBLINA CREADAS EN CANVAS -->
  <canvas id="spookyCanvas"></canvas>

  <!-- CONTROLES DE AUDIO SINTETIZADO -->
  <div class="fixed top-4 right-4 z-50">
    <button id="soundToggle" onclick="toggleSpookySound()" class="glass-card text-brand-orange hover:text-brand-green p-3 rounded-full shadow-2xl transition duration-300 flex items-center justify-center space-x-2">
      <i data-lucide="volume-x" id="soundIcon" class="w-5 h-5"></i>
      <span class="text-xs font-bold tracking-wider hidden sm:inline" id="soundText">AUDIO OFF</span>
    </button>
  </div>

  <!-- SISTEMA DE NOTIFICACIONES TOAST -->
  <div id="toastContainer" class="fixed bottom-6 right-6 z-50 flex flex-col space-y-3 pointer-events-none"></div>

  <!-- CONTENEDOR PRINCIPAL -->
  <div class="relative z-10 max-w-4xl mx-auto px-4 py-8 sm:py-12 space-y-12">

    <!-- HERO SECTION -->
    <header class="text-center space-y-6 pt-4">
      
      <!-- Insignia de Edición -->
      <div class="inline-flex items-center space-x-2 px-4 py-1.5 rounded-full bg-brand-orange/15 border border-brand-orange/50 text-brand-orange font-tech text-xs sm:text-sm tracking-widest uppercase animate-pulse">
        <span>🔥 2DA EDICIÓN RECARGADA 🔥</span>
      </div>

      <!-- Título Principal -->
      <div class="space-y-2">
        <h1 class="font-spooky text-6xl sm:text-8xl md:text-9xl text-brand-orange text-glow-orange tracking-wider leading-none select-none animate-float">
          LOKOWEEN
        </h1>
        <p class="font-tech text-lg sm:text-2xl text-brand-green text-glow-green tracking-widest uppercase font-extrabold">
          Peda de Disfraces Vol. II
        </p>
      </div>

      <p class="text-slate-200 max-w-lg mx-auto text-sm sm:text-base leading-relaxed font-medium drop-shadow-md">
        Hace un año sobrevivimos al primer Lokoween... ¡Este 31 de octubre subimos el nivel! Prepárate para la mejor noche del año. 🎃💀✨
      </p>

      <!-- CONTADOR REGRESIVO -->
      <div class="pt-4">
        <div class="glass-card p-6 sm:p-8 rounded-3xl max-w-2xl mx-auto shadow-2xl relative overflow-hidden group">
          <div class="absolute -top-12 -left-12 w-24 h-24 bg-brand-orange/30 rounded-full blur-2xl group-hover:bg-brand-green/30 transition duration-700"></div>
          
          <h2 class="text-xs font-tech text-slate-300 uppercase tracking-widest mb-4 flex items-center justify-center space-x-2">
            <i data-lucide="clock" class="w-4 h-4 text-brand-orange"></i>
            <span>Tiempo Restante para el Desmadre</span>
          </h2>

          <div class="grid grid-cols-4 gap-2 sm:gap-4 font-tech">
            <div class="bg-black/70 p-3 sm:p-4 rounded-2xl border border-white/10 text-center shadow-inner">
              <span id="cdDays" class="block text-2xl sm:text-4xl font-black text-brand-orange">00</span>
              <span class="text-[10px] sm:text-xs text-slate-400 uppercase">Días</span>
            </div>
            <div class="bg-black/70 p-3 sm:p-4 rounded-2xl border border-white/10 text-center shadow-inner">
              <span id="cdHours" class="block text-2xl sm:text-4xl font-black text-brand-orange">00</span>
              <span class="text-[10px] sm:text-xs text-slate-400 uppercase">Horas</span>
            </div>
            <div class="bg-black/70 p-3 sm:p-4 rounded-2xl border border-white/10 text-center shadow-inner">
              <span id="cdMinutes" class="block text-2xl sm:text-4xl font-black text-brand-orange">00</span>
              <span class="text-[10px] sm:text-xs text-slate-400 uppercase">Mins</span>
            </div>
            <div class="bg-black/70 p-3 sm:p-4 rounded-2xl border border-white/10 text-center shadow-inner">
              <span id="cdSeconds" class="block text-2xl sm:text-4xl font-black text-brand-green text-glow-green">00</span>
              <span class="text-[10px] sm:text-xs text-slate-400 uppercase">Segs</span>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- DETALLES DEL EVENTO -->
    <section class="grid grid-cols-1 md:grid-cols-2 gap-6">

      <!-- TARJETA 1: DRESS CODE -->
      <div class="glass-card p-6 sm:p-8 rounded-3xl transition duration-300 hover:-translate-y-1 relative overflow-hidden">
        <div class="flex items-start justify-between">
          <div class="p-3 bg-brand-orange/20 rounded-2xl border border-brand-orange/40 text-brand-orange">
            <i data-lucide="sparkles" class="w-7 h-7"></i>
          </div>
          <span class="px-3 py-1 bg-brand-orange/20 text-brand-orange text-xs font-bold rounded-full uppercase tracking-wider">
            Mandatorio 🎭
          </span>
        </div>
        <div class="mt-6 space-y-2">
          <h3 class="text-xl font-bold font-tech text-white">Dress Code: Putidisfraz</h3>
          <p class="text-sm text-slate-300 leading-relaxed">
            Ponte creativo/a, sensual o terrorífico/a. Obligatorio venir disfrazado.
          </p>
          <div class="mt-4 p-3 bg-black/50 rounded-xl border border-brand-orange/30 flex items-center space-x-3">
            <i data-lucide="trophy" class="w-6 h-6 text-yellow-400 shrink-0"></i>
            <p class="text-xs text-slate-200">
              <strong class="text-yellow-400 font-semibold">¡Concurso & Premio!</strong> Habrá premio sorpresa al mejor disfraz de la noche.
            </p>
          </div>
        </div>
      </div>

      <!-- TARJETA 2: TTP (SIMPLIFICADO AL MÁXIMO) -->
      <div class="glass-card p-6 sm:p-8 rounded-3xl transition duration-300 hover:-translate-y-1 relative overflow-hidden flex flex-col justify-between">
        <div class="flex items-start justify-between">
          <div class="p-3 bg-brand-green/20 rounded-2xl border border-brand-green/40 text-brand-green">
            <i data-lucide="wine" class="w-7 h-7"></i>
          </div>
          <span class="px-3 py-1 bg-brand-green/20 text-brand-green text-xs font-bold rounded-full uppercase tracking-wider">
            TTP 🍾
          </span>
        </div>
        <div class="mt-6 space-y-2">
          <h3 class="text-xl font-bold font-tech text-white">TTP (Trae Tu Pomo)</h3>
          <p class="text-sm sm:text-base text-slate-200 font-medium leading-relaxed">
            Cada quien trae lo que vaya a tomar. 🥂
          </p>
        </div>
        <div class="mt-6 pt-3 border-t border-white/10 text-xs text-brand-green font-tech">
          <span>#Lokoween2daEdición</span>
        </div>
      </div>

      <!-- TARJETA 3: FECHA Y HORARIO -->
      <div class="glass-card p-6 sm:p-8 rounded-3xl transition duration-300 hover:-translate-y-1">
        <div class="flex items-center space-x-4">
          <div class="p-3 bg-purple-500/20 rounded-2xl border border-purple-500/40 text-purple-400">
            <i data-lucide="calendar" class="w-7 h-7"></i>
          </div>
          <div>
            <h3 class="text-lg font-bold font-tech text-white">Fecha y Hora</h3>
            <p class="text-sm text-slate-300">Jueves 31 de Octubre, 2026</p>
          </div>
        </div>
        <div class="mt-6 pt-4 border-t border-white/10 flex items-center justify-between text-sm">
          <span class="text-slate-300 flex items-center space-x-2">
            <i data-lucide="clock" class="w-4 h-4 text-brand-orange"></i>
            <span>Acceso: <strong>8:00 PM</strong></span>
          </span>
          <span class="text-slate-300 flex items-center space-x-2">
            <i data-lucide="moon" class="w-4 h-4 text-brand-green"></i>
            <span>Cierre: <strong>Hasta que el cuerpo aguante</strong></span>
          </span>
        </div>
      </div>

      <!-- TARJETA 4: UBICACIÓN Y BOTONES DE ENLACE -->
      <div class="glass-card p-6 sm:p-8 rounded-3xl transition duration-300 hover:-translate-y-1 flex flex-col justify-between">
        <div class="flex items-center space-x-4 mb-4">
          <div class="p-3 bg-red-500/20 rounded-2xl border border-red-500/40 text-red-400">
            <i data-lucide="map-pin" class="w-7 h-7"></i>
          </div>
          <div>
            <h3 class="text-lg font-bold font-tech text-white">Ubicación del Evento</h3>
            <p class="text-xs text-slate-300">¡Activa el mapa o abre la ruta en tu app!</p>
          </div>
        </div>

        <div class="grid grid-cols-1 sm:grid-cols-2 gap-3 mt-2">
          <button onclick="copyAddress()" class="w-full py-2.5 px-4 rounded-xl bg-white/10 hover:bg-white/20 border border-white/15 text-xs font-semibold text-slate-100 flex items-center justify-center space-x-2 transition">
            <i data-lucide="copy" class="w-4 h-4 text-brand-orange"></i>
            <span>Copiar Enlace Mapa</span>
          </button>
          
          <a href="https://maps.app.goo.gl/emMSVnp81T2YVWb28" target="_blank" rel="noopener noreferrer" class="w-full py-2.5 px-4 rounded-xl bg-brand-green/20 hover:bg-brand-green/35 border border-brand-green/50 text-xs font-bold text-brand-green flex items-center justify-center space-x-2 transition text-center">
            <i data-lucide="external-link" class="w-4 h-4 text-brand-green"></i>
            <span>Abrir en Google Maps</span>
          </a>
        </div>
      </div>

    </section>

    <!-- SECCIÓN COMPLETA DE MAPA INTEGRADO -->
    <section class="glass-card p-4 sm:p-6 rounded-3xl overflow-hidden space-y-4">
      <div class="flex items-center justify-between px-2">
        <h3 class="text-sm font-bold font-tech text-white flex items-center space-x-2">
          <i data-lucide="navigation" class="w-4 h-4 text-brand-orange"></i>
          <span>Mapa Interactivo</span>
        </h3>
        <span class="text-[10px] text-slate-400 font-tech">GOOGLE MAPS</span>
      </div>
      
      <div class="w-full h-64 sm:h-80 rounded-2xl overflow-hidden border border-white/15 shadow-2xl">
        <iframe 
          src="https://www.google.com/maps/embed?pb=!1m16!1m11!1m3!1d633.0317042666064!2d-99.65825499183204!3d19.349213441261625!2m2!1f0!2f0!3m2!1i1024!2i768!4f13.1!3m2!1m1!2s!5e1!3m2!1ses-419!2smx!4v1793036161034!5m2!1ses-419!2smx" 
          width="100%" 
          height="100%" 
          style="border:0; filter: invert(90%) hue-rotate(180deg) contrast(1.2);" 
          allowfullscreen="" 
          loading="lazy" 
          referrerpolicy="strict-origin-when-cross-origin">
        </iframe>
      </div>
    </section>

    <!-- RECOMENDACIÓN DE MÚSICA -->
    <section class="glass-card p-6 sm:p-8 rounded-3xl relative overflow-hidden">
      <div class="flex flex-col sm:flex-row items-start sm:items-center justify-between gap-4">
        <div class="space-y-1">
          <h3 class="text-xl font-bold font-tech text-white flex items-center space-x-2">
            <i data-lucide="disc" class="w-6 h-6 text-brand-green animate-spin" style="animation-duration: 6s;"></i>
            <span>¿Qué rola no puede faltar? 🎧</span>
          </h3>
          <p class="text-xs sm:text-sm text-slate-300">
            Recomienda tu canción para la lista de reproducción de la noche.
          </p>
        </div>
        <div class="flex w-full sm:w-auto items-center space-x-2">
          <input type="text" id="songInput" placeholder="Ej: Safaera - Bad Bunny" class="w-full sm:w-64 px-4 py-2.5 rounded-xl bg-black/70 border border-white/15 text-xs text-white focus:outline-none focus:border-brand-green transition">
          <button onclick="submitSong()" class="px-4 py-2.5 bg-brand-green text-black font-bold text-xs rounded-xl hover:bg-emerald-400 transition shrink-0">
            Enviar
          </button>
        </div>
      </div>
    </section>

    <!-- CALL TO ACTION FINAL -->
    <section class="text-center space-y-6 pt-4">
      <div class="glass-card p-8 sm:p-12 rounded-3xl border-2 border-brand-orange/40 shadow-2xl space-y-6 bg-gradient-to-b from-brand-orange/15 via-transparent to-transparent">
        
        <h2 class="font-spooky text-5xl sm:text-7xl text-brand-orange text-glow-orange">
          ¡Nos vemos el 31! 🎃
        </h2>
        <p class="text-sm sm:text-base text-slate-200 max-w-md mx-auto">
          Prepara tu disfraz y tu pomo. ¡La 2da edición de Lokoween se va a poner legendaria!
        </p>

        <div class="max-w-md mx-auto flex flex-col sm:flex-row gap-4 pt-2">
          <button onclick="addToCalendar()" class="flex-1 py-4 px-6 rounded-2xl bg-gradient-to-r from-brand-orange to-red-600 text-white font-tech font-bold text-sm uppercase tracking-wider shadow-xl hover:brightness-110 active:scale-95 transition flex items-center justify-center space-x-2">
            <i data-lucide="calendar-plus" class="w-5 h-5"></i>
            <span>Agendar en Google Calendar</span>
          </button>
        </div>

      </div>
    </section>

    <!-- FOOTER -->
    <footer class="text-center text-xs text-slate-400 space-y-2 py-6 border-t border-white/10">
      <p>LOKOWEEN 2026 🎃 • Nos reservamos el derecho de acceso a quien no traiga disfraz.</p>
    </footer>

  </div>

  <!-- JAVASCRIPT -->
  <script>
    // Inicializar Iconos Lucide
    lucide.createIcons();

    const MAP_URL = "https://maps.app.goo.gl/emMSVnp81T2YVWb28";

    function copyAddress() {
      if (navigator.clipboard && navigator.clipboard.writeText) {
        navigator.clipboard.writeText(MAP_URL);
        showToast("📍 ¡Enlace de Google Maps copiado!");
      } else {
        const textarea = document.createElement('textarea');
        textarea.value = MAP_URL;
        document.body.appendChild(textarea);
        textarea.select();
        document.execCommand('copy');
        document.body.removeChild(textarea);
        showToast("📍 ¡Enlace de Google Maps copiado!");
      }
    }

    // TOAST NOTIFICATION SYSTEM
    function showToast(message) {
      const container = document.getElementById('toastContainer');
      const toast = document.createElement('div');
      toast.className = 'glass-card px-4 py-3 rounded-2xl text-xs font-bold text-brand-green border border-brand-green/40 shadow-2xl flex items-center space-x-2 transition-all duration-300 transform translate-y-4 opacity-0 pointer-events-auto';
      toast.innerHTML = `<i data-lucide="check-circle" class="w-4 h-4 text-brand-green"></i><span>${message}</span>`;
      
      container.appendChild(toast);
      lucide.createIcons();

      setTimeout(() => {
        toast.classList.remove('translate-y-4', 'opacity-0');
      }, 50);

      setTimeout(() => {
        toast.classList.add('opacity-0', 'translate-y-2');
        setTimeout(() => toast.remove(), 300);
      }, 3500);
    }

    // COUNTDOWN TIMER TO OCT 31 8:00 PM
    const targetDate = new Date('October 31, 2026 20:00:00').getTime();

    function updateCountdown() {
      const now = new Date().getTime();
      const difference = targetDate - now;

      if (difference < 0) {
        document.getElementById('cdDays').innerText = "00";
        document.getElementById('cdHours').innerText = "00";
        document.getElementById('cdMinutes').innerText = "00";
        document.getElementById('cdSeconds').innerText = "00";
        return;
      }

      const days = Math.floor(difference / (1000 * 60 * 60 * 24));
      const hours = Math.floor((difference % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      const minutes = Math.floor((difference % (1000 * 60 * 60)) / (1000 * 60));
      const seconds = Math.floor((difference % (1000 * 60)) / 1000);

      document.getElementById('cdDays').innerText = days < 10 ? '0' + days : days;
      document.getElementById('cdHours').innerText = hours < 10 ? '0' + hours : hours;
      document.getElementById('cdMinutes').innerText = minutes < 10 ? '0' + minutes : minutes;
      document.getElementById('cdSeconds').innerText = seconds < 10 ? '0' + seconds : seconds;
    }

    setInterval(updateCountdown, 1000);
    updateCountdown();

    // ENVÍO DE SUGERENCIA DE CANCIÓN
    function submitSong() {
      const input = document.getElementById('songInput');
      const song = input.value.trim();
      if (!song) {
        showToast("⚠️ Escribe el nombre de la canción primero");
        return;
      }
      showToast(`🎶 ¡"${song}" anotada!`);
      input.value = '';
    }

    // AGENDAR EN GOOGLE CALENDAR
    function addToCalendar() {
      const title = encodeURIComponent("🎃 LOKOWEEN (2da Edición) - Peda de Disfraces");
      const details = encodeURIComponent("Peda de disfraces (Putidisfraz), TTP (Trae tu pomo).");
      const location = encodeURIComponent("https://maps.app.goo.gl/emMSVnp81T2YVWb28");
      const startDate = "20261031T200000";
      const endDate = "20261101T060000";

      const googleCalUrl = `https://calendar.google.com/calendar/render?action=TEMPLATE&text=${title}&dates=${startDate}/${endDate}&details=${details}&location=${location}`;
      window.open(googleCalUrl, '_blank');
    }

    // CANVAS DE CHISPAS Y NEBLINA CREADO A 60FPS
    const canvas = document.getElementById('spookyCanvas');
    const ctx = canvas.getContext('2d');

    let particles = [];
    let width = (canvas.width = window.innerWidth);
    let height = (canvas.height = window.innerHeight);

    window.addEventListener('resize', () => {
      width = canvas.width = window.innerWidth;
      height = canvas.height = window.innerHeight;
      initParticles();
    });

    class EmberParticle {
      constructor() {
        this.reset();
      }

      reset() {
        this.x = Math.random() * width;
        this.y = height + Math.random() * 50;
        this.size = Math.random() * 3 + 1;
        this.speedY = Math.random() * 1.5 + 0.5;
        this.speedX = (Math.random() - 0.5) * 0.8;
        this.opacity = Math.random() * 0.8 + 0.2;
        this.color = Math.random() > 0.3 ? '#ff6600' : '#00ff66';
      }

      update() {
        this.y -= this.speedY;
        this.x += this.speedX + Math.sin(this.y * 0.01) * 0.3;
        this.opacity -= 0.003;

        if (this.y < -10 || this.opacity <= 0) {
          this.reset();
        }
      }

      draw() {
        ctx.save();
        ctx.globalAlpha = this.opacity;
        ctx.fillStyle = this.color;
        ctx.shadowBlur = 10;
        ctx.shadowColor = this.color;
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
        ctx.fill();
        ctx.restore();
      }
    }

    function initParticles() {
      particles = [];
      const particleCount = Math.min(Math.floor(width / 15), 60);
      for (let i = 0; i < particleCount; i++) {
        const p = new EmberParticle();
        p.y = Math.random() * height;
        particles.push(p);
      }
    }

    function animateParticles() {
      ctx.clearRect(0, 0, width, height);
      particles.forEach(p => {
        p.update();
        p.draw();
      });
      requestAnimationFrame(animateParticles);
    }

    initParticles();
    animateParticles();

    // SINTETIZADOR AUDIO SPOOKY
    let audioCtx = null;
    let isPlayingSound = false;
    let mainGain = null;
    let synthOsc = null;

    function toggleSpookySound() {
      const soundIcon = document.getElementById('soundIcon');
      const soundText = document.getElementById('soundText');

      if (!isPlayingSound) {
        if (!audioCtx) {
          audioCtx = new (window.AudioContext || window.webkitAudioContext)();
        }
        
        synthOsc = audioCtx.createOscillator();
        const lfo = audioCtx.createOscillator();
        mainGain = audioCtx.createGain();
        const filter = audioCtx.createBiquadFilter();

        synthOsc.type = 'sawtooth';
        synthOsc.frequency.setValueAtTime(55, audioCtx.currentTime);

        lfo.frequency.setValueAtTime(0.2, audioCtx.currentTime);
        const lfoGain = audioCtx.createGain();
        lfoGain.gain.setValueAtTime(15, audioCtx.currentTime);

        lfo.connect(lfoGain);
        lfoGain.connect(synthOsc.frequency);

        filter.type = 'lowpass';
        filter.frequency.setValueAtTime(180, audioCtx.currentTime);

        mainGain.gain.setValueAtTime(0.05, audioCtx.currentTime);

        synthOsc.connect(filter);
        filter.connect(mainGain);
        mainGain.connect(audioCtx.destination);

        synthOsc.start();
        lfo.start();

        isPlayingSound = true;
        soundIcon.setAttribute('data-lucide', 'volume-2');
        soundText.innerText = "AUDIO ON";
        showToast("👻 Ambiente Spooky Activado");
      } else {
        if (mainGain) {
          mainGain.gain.exponentialRampToValueAtTime(0.0001, audioCtx.currentTime + 0.5);
          setTimeout(() => {
            if (synthOsc) synthOsc.stop();
          }, 500);
        }
        isPlayingSound = false;
        soundIcon.setAttribute('data-lucide', 'volume-x');
        soundText.innerText = "AUDIO OFF";
      }
      lucide.createIcons();
    }
  </script>
</body>
</html>
