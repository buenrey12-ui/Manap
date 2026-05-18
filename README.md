<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Amanah — Toko Sayuran Segar</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="https://code.iconify.design/3/3.1.0/iconify.min.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&family=Playfair+Display:ital,wght@0,400;0,500;0,600;1,400&display=swap" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            cream: '#FDFCF8',
            savor: '#F3EFE0',
            green: {
              50: '#f0fdf4',
              100: '#dcfce7',
              200: '#bbf7d0',
              300: '#86efac',
              400: '#4ade80',
              500: '#22c55e',
              600: '#16a34a',
              700: '#15803d',
              800: '#166534',
              900: '#14532d',
            }
          },
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            serif: ['Playfair Display', 'serif'],
          },
          borderRadius: {
            '4xl': '2rem',
          }
        }
      }
    }
  </script>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    html { scroll-behavior: smooth; }

    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(30px); }
      to { opacity: 1; transform: translateY(0); }
    }

    .animate-fade-in-up {
      animation: fadeInUp 1s cubic-bezier(0.16, 1, 0.3, 1) forwards;
    }

    .delay-100 { animation-delay: 100ms; }
    .delay-200 { animation-delay: 200ms; }
    .delay-300 { animation-delay: 300ms; }
    .delay-400 { animation-delay: 400ms; }
    .delay-500 { animation-delay: 500ms; }

    .reveal {
      opacity: 0;
      filter: blur(8px);
      transform: translateY(24px);
      transition: all 1.2s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .reveal.active {
      opacity: 1;
      filter: blur(0);
      transform: translateY(0);
    }

    .glass-card {
      background: rgba(28, 25, 23, 0.4);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.1);
      transition: all 500ms ease;
    }
    .glass-card:hover {
      background: rgba(28, 25, 23, 0.6);
      border-color: rgba(255, 255, 255, 0.2);
      transform: translateY(-8px);
    }

    .shine-effect {
      position: relative;
      overflow: hidden;
    }
    .shine-effect::after {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0; bottom: 0;
      background: linear-gradient(to right, transparent, rgba(255,255,255,0.15), transparent);
      transform: translateX(-100%) skewX(-12deg);
      transition: transform 1000ms ease-in-out;
    }
    .shine-effect:hover::after {
      transform: translateX(100%) skewX(-12deg);
    }

    @keyframes pulse-bg {
      0%, 100% { transform: scale(1.05); }
      50% { transform: scale(1.1); }
    }
    .animate-pulse-bg {
      animation: pulse-bg 15s ease-in-out infinite;
    }

    @keyframes float {
      0%, 100% { transform: translateY(0px); }
      50% { transform: translateY(-10px); }
    }
    .animate-float {
      animation: float 4s ease-in-out infinite;
    }

    .product-img {
      transition: transform 700ms ease;
    }
    .glass-card:hover .product-img {
      transform: scale(1.08);
    }

    .nav-scrolled {
      background: rgba(10, 10, 10, 0.85) !important;
      backdrop-filter: blur(24px) !important;
    }

    /* Toast */
    .toast {
      position: fixed;
      bottom: 2rem;
      right: 2rem;
      background: #166534;
      color: #fff;
      padding: 1rem 1.5rem;
      border-radius: 1rem;
      font-size: 0.95rem;
      z-index: 9999;
      opacity: 0;
      transform: translateY(20px);
      transition: all 0.4s ease;
      pointer-events: none;
    }
    .toast.show {
      opacity: 1;
      transform: translateY(0);
      pointer-events: auto;
    }

    /* Mobile menu */
    .mobile-menu {
      max-height: 0;
      overflow: hidden;
      transition: max-height 0.5s cubic-bezier(0.16, 1, 0.3, 1);
    }
    .mobile-menu.open {
      max-height: 400px;
    }
  </style>
</head>
<body class="bg-stone-950 text-cream font-sans">

  <!-- Toast Notification -->
  <div id="toast" class="toast">
    <span id="toast-msg">Pesan berhasil dikirim!</span>
  </div>

  <!-- ===== NAVBAR ===== -->
  <nav id="navbar" class="fixed top-0 left-0 right-0 z-50 h-20 flex items-center px-6 transition-all duration-500" style="background: rgba(10,10,10,0.3); backdrop-filter: blur(24px);">
    <div class="max-w-screen-2xl mx-auto w-full flex items-center justify-between">
      <!-- Logo -->
      <a href="#" class="flex items-center gap-3 group">
        <div class="w-10 h-10 rounded-xl bg-green-600 flex items-center justify-center transition-transform duration-300 group-hover:rotate-12">
          <span class="iconify text-white text-xl" data-icon="mdi:leaf"></span>
        </div>
        <span class="font-serif text-2xl font-medium tracking-tight">Amanah</span>
      </a>

      <!-- Desktop Links -->
      <div class="hidden md:flex items-center gap-8">
        <a href="#beranda" class="text-sm font-medium text-stone-400 hover:text-cream transition-colors duration-300">Beranda</a>
        <a href="#produk" class="text-sm font-medium text-stone-400 hover:text-cream transition-colors duration-300">Produk</a>
        <a href="#tentang" class="text-sm font-medium text-stone-400 hover:text-cream transition-colors duration-300">Tentang</a>
        <a href="#keunggulan" class="text-sm font-medium text-stone-400 hover:text-cream transition-colors duration-300">Keunggulan</a>
        <a href="#kontak" class="text-sm font-medium text-stone-400 hover:text-cream transition-colors duration-300">Kontak</a>
        <a href="https://wa.me/62083182339790" target="_blank" class="bg-green-600 hover:bg-green-700 text-white text-sm font-bold uppercase tracking-wide px-6 py-3 rounded-full transition-all duration-150 hover:scale-105 shine-effect">
          <span class="iconify inline-block mr-1 -mt-0.5" data-icon="mdi:whatsapp"></span>
          Pesan Sekarang
        </a>
      </div>

      <!-- Mobile Toggle -->
      <button id="menu-toggle" class="md:hidden text-cream text-2xl">
        <span class="iconify" data-icon="mdi:menu" id="menu-icon"></span>
      </button>
    </div>

    <!-- Mobile Menu -->
    <div id="mobile-menu" class="mobile-menu absolute top-20 left-0 right-0 bg-stone-950/95 backdrop-blur-xl border-b border-white/10 md:hidden">
      <div class="flex flex-col px-6 py-4 gap-4">
        <a href="#beranda" class="text-sm font-medium text-stone-400 hover:text-cream transition-colors py-2" onclick="closeMobileMenu()">Beranda</a>
        <a href="#produk" class="text-sm font-medium text-stone-400 hover:text-cream transition-colors py-2" onclick="closeMobileMenu()">Produk</a>
        <a href="#tentang" class="text-sm font-medium text-stone-400 hover:text-cream transition-colors py-2" onclick="closeMobileMenu()">Tentang</a>
        <a href="#keunggulan" class="text-sm font-medium text-stone-400 hover:text-cream transition-colors py-2" onclick="closeMobileMenu()">Keunggulan</a>
        <a href="#kontak" class="text-sm font-medium text-stone-400 hover:text-cream transition-colors py-2" onclick="closeMobileMenu()">Kontak</a>
        <a href="https://wa.me/62083182339790" target="_blank" class="bg-green-600 text-white text-sm font-bold uppercase tracking-wide px-6 py-3 rounded-full text-center mt-2">Pesan Sekarang</a>
      </div>
    </div>
  </nav>

  <!-- ===== HERO ===== -->
  <section id="beranda" class="relative h-[90vh] flex items-center justify-center overflow-hidden rounded-b-[3rem]">
    <!-- BG Image -->
    <div class="absolute inset-0">
      <img src="https://picsum.photos/seed/vegetable-market-fresh/1920/1080.jpg" alt="Sayuran Segar" class="w-full h-full object-cover animate-pulse-bg" />
      <div class="absolute inset-0 bg-gradient-to-b from-stone-950/70 via-stone-950/50 to-stone-950"></div>
    </div>

    <!-- Content -->
    <div class="relative z-10 text-center px-6 max-w-4xl">
      <div class="opacity-0 animate-fade-in-up">
        <span class="inline-flex items-center gap-2 bg-green-600/20 border border-green-500/30 text-green-300 text-xs font-bold uppercase tracking-[0.3em] px-5 py-2 rounded-full mb-8">
          <span class="iconify" data-icon="mdi:leaf-circle-outline"></span>
          Segar & Alami
        </span>
      </div>
      <h1 class="font-serif text-5xl md:text-8xl font-normal leading-[0.85] tracking-tighter mb-8 opacity-0 animate-fade-in-up delay-100">
        Sayuran Segar<br><span class="italic text-green-400">Pilihan Amanah</span>
      </h1>
      <p class="text-lg md:text-xl font-light text-stone-400 max-w-2xl mx-auto mb-10 opacity-0 animate-fade-in-up delay-200 leading-relaxed">
        Dari kebun langsung ke dapur Anda. Sayuran pilihan berkualitas tinggi dengan harga terjangkau. Karena kejujuran adalah pegangan kami.
      </p>
      <div class="flex flex-col sm:flex-row items-center justify-center gap-4 opacity-0 animate-fade-in-up delay-300">
        <a href="#produk" class="bg-green-600 hover:bg-green-700 text-white text-sm font-bold uppercase tracking-wide px-8 py-4 rounded-full transition-all duration-150 hover:scale-105 shine-effect">
          Lihat Produk
        </a>
        <a href="#kontak" class="bg-white/10 hover:bg-white/20 text-cream text-sm font-bold uppercase tracking-wide px-8 py-4 rounded-full border border-white/20 transition-all duration-150 hover:scale-105">
          Hubungi Kami
        </a>
      </div>
    </div>

    <!-- Scroll Indicator -->
    <div class="absolute bottom-8 left-1/2 -translate-x-1/2 animate-float">
      <span class="iconify text-stone-500 text-2xl" data-icon="mdi:chevron-double-down"></span>
    </div>
  </section>

  <!-- ===== STATS BAR ===== -->
  <section class="py-16 px-6">
    <div class="max-w-screen-xl mx-auto">
      <div class="grid grid-cols-2 md:grid-cols-4 gap-8 reveal">
        <div class="text-center">
          <div class="text-3xl md:text-5xl font-serif font-medium text-green-400 mb-2">50+</div>
          <div class="text-sm text-stone-500 uppercase tracking-widest font-bold">Jenis Sayuran</div>
        </div>
        <div class="text-center">
          <div class="text-3xl md:text-5xl font-serif font-medium text-green-400 mb-2">5K+</div>
          <div class="text-sm text-stone-500 uppercase tracking-widest font-bold">Pelanggan</div>
        </div>
        <div class="text-center">
          <div class="text-3xl md:text-5xl font-serif font-medium text-green-400 mb-2">10</div>
          <div class="text-sm text-stone-500 uppercase tracking-widest font-bold">Tahun Pengalaman</div>
        </div>
        <div class="text-center">
          <div class="text-3xl md:text-5xl font-serif font-medium text-green-400 mb-2">100%</div>
          <div class="text-sm text-stone-500 uppercase tracking-widest font-bold">Alami & Segar</div>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== PRODUK ===== -->
  <section id="produk" class="py-32 px-6 bg-stone-900 rounded-t-[3rem]" style="box-shadow: 0 -10px 40px rgba(0,0,0,0.03);">
    <div class="max-w-screen-xl mx-auto">
      <!-- Header -->
      <div class="text-center mb-20 reveal">
        <span class="inline-block text-xs font-bold uppercase tracking-[0.3em] text-green-400 mb-4">Produk Kami</span>
        <h2 class="font-serif text-4xl md:text-6xl font-normal leading-[0.85] tracking-tighter mb-6">
          Sayuran Pilihan<br><span class="italic text-green-400">Terbaik</span>
        </h2>
        <p class="text-lg font-light text-stone-500 max-w-xl mx-auto leading-relaxed">
          Berbagai macam sayuran segar yang dipilih langsung dari petani terpercaya setiap harinya.
        </p>
      </div>

      <!-- Product Grid -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-x-6 gap-y-10">

        <!-- Product 1 -->
        <div class="glass-card rounded-3xl p-3 reveal group">
          <div class="overflow-hidden rounded-2xl aspect-[4/3]">
            <img src="https://picsum.photos/seed/bayam-spinach-green/600/450.jpg" alt="Bayam" class="w-full h-full object-cover product-img" />
          </div>
          <div class="p-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="font-serif text-xl font-medium">Bayam Segar</h3>
              <span class="bg-green-600/20 text-green-400 text-xs font-bold px-3 py-1 rounded-full">Organik</span>
            </div>
            <p class="text-stone-500 text-sm mb-4">Bayam hijau segar kaya zat besi dan vitamin, cocok untuk berbagai masakan.</p>
            <div class="flex items-center justify-between">
              <span class="text-green-400 font-serif text-xl font-medium">Rp 8.000<span class="text-stone-500 text-xs font-sans">/ikat</span></span>
              <button onclick="orderProduct('Bayam Segar')" class="bg-green-600 hover:bg-green-700 text-white text-xs font-bold uppercase tracking-wider px-4 py-2 rounded-full transition-all hover:scale-105">
                <span class="iconify inline-block mr-1" data-icon="mdi:cart-plus"></span>Pesan
              </button>
            </div>
          </div>
        </div>

        <!-- Product 2 -->
        <div class="glass-card rounded-3xl p-3 reveal delay-100 group md:translate-y-8">
          <div class="overflow-hidden rounded-2xl aspect-[4/3]">
            <img src="https://picsum.photos/seed/tomato-red-fresh/600/450.jpg" alt="Tomat" class="w-full h-full object-cover product-img" />
          </div>
          <div class="p-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="font-serif text-xl font-medium">Tomat Merah</h3>
              <span class="bg-red-600/20 text-red-400 text-xs font-bold px-3 py-1 rounded-full">Best Seller</span>
            </div>
            <p class="text-stone-500 text-sm mb-4">Tomat merah segar dan berair, sempurna untuk sambal atau salad.</p>
            <div class="flex items-center justify-between">
              <span class="text-green-400 font-serif text-xl font-medium">Rp 12.000<span class="text-stone-500 text-xs font-sans">/kg</span></span>
              <button onclick="orderProduct('Tomat Merah')" class="bg-green-600 hover:bg-green-700 text-white text-xs font-bold uppercase tracking-wider px-4 py-2 rounded-full transition-all hover:scale-105">
                <span class="iconify inline-block mr-1" data-icon="mdi:cart-plus"></span>Pesan
              </button>
            </div>
          </div>
        </div>

        <!-- Product 3 -->
        <div class="glass-card rounded-3xl p-3 reveal delay-200 group">
          <div class="overflow-hidden rounded-2xl aspect-[4/3]">
            <img src="https://picsum.photos/seed/carrot-orange-veggie/600/450.jpg" alt="Wortel" class="w-full h-full object-cover product-img" />
          </div>
          <div class="p-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="font-serif text-xl font-medium">Wortel Premium</h3>
              <span class="bg-orange-600/20 text-orange-400 text-xs font-bold px-3 py-1 rounded-full">Lokal</span>
            </div>
            <p class="text-stone-500 text-sm mb-4">Wortel manis dan renyah kaya vitamin A, pilihan terbaik untuk keluarga.</p>
            <div class="flex items-center justify-between">
              <span class="text-green-400 font-serif text-xl font-medium">Rp 15.000<span class="text-stone-500 text-xs font-sans">/kg</span></span>
              <button onclick="orderProduct('Wortel Premium')" class="bg-green-600 hover:bg-green-700 text-white text-xs font-bold uppercase tracking-wider px-4 py-2 rounded-full transition-all hover:scale-105">
                <span class="iconify inline-block mr-1" data-icon="mdi:cart-plus"></span>Pesan
              </button>
            </div>
          </div>
        </div>

        <!-- Product 4 -->
        <div class="glass-card rounded-3xl p-3 reveal group">
          <div class="overflow-hidden rounded-2xl aspect-[4/3]">
            <img src="https://picsum.photos/seed/broccoli-green-fresh/600/450.jpg" alt="Brokoli" class="w-full h-full object-cover product-img" />
          </div>
          <div class="p-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="font-serif text-xl font-medium">Brokoli Hijau</h3>
              <span class="bg-green-600/20 text-green-400 text-xs font-bold px-3 py-1 rounded-full">Organik</span>
            </div>
            <p class="text-stone-500 text-sm mb-4">Brokoli segar berukuran besar, kaya antioksidan dan nutrisi penting.</p>
            <div class="flex items-center justify-between">
              <span class="text-green-400 font-serif text-xl font-medium">Rp 18.000<span class="text-stone-500 text-xs font-sans">/bungkus</span></span>
              <button onclick="orderProduct('Brokoli Hijau')" class="bg-green-600 hover:bg-green-700 text-white text-xs font-bold uppercase tracking-wider px-4 py-2 rounded-full transition-all hover:scale-105">
                <span class="iconify inline-block mr-1" data-icon="mdi:cart-plus"></span>Pesan
              </button>
            </div>
          </div>
        </div>

        <!-- Product 5 -->
        <div class="glass-card rounded-3xl p-3 reveal delay-100 group md:translate-y-8">
          <div class="overflow-hidden rounded-2xl aspect-[4/3]">
            <img src="https://picsum.photos/seed/cabbage-vegetable/600/450.jpg" alt="Kubis" class="w-full h-full object-cover product-img" />
          </div>
          <div class="p-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="font-serif text-xl font-medium">Kubis / Kol</h3>
              <span class="bg-green-600/20 text-green-400 text-xs font-bold px-3 py-1 rounded-full">Segar</span>
            </div>
            <p class="text-stone-500 text-sm mb-4">Kubis segar dan padat, ideal untuk tumisan, sup, atau salad segar.</p>
            <div class="flex items-center justify-between">
              <span class="text-green-400 font-serif text-xl font-medium">Rp 10.000<span class="text-stone-500 text-xs font-sans">/kg</span></span>
              <button onclick="orderProduct('Kubis / Kol')" class="bg-green-600 hover:bg-green-700 text-white text-xs font-bold uppercase tracking-wider px-4 py-2 rounded-full transition-all hover:scale-105">
                <span class="iconify inline-block mr-1" data-icon="mdi:cart-plus"></span>Pesan
              </button>
            </div>
          </div>
        </div>

        <!-- Product 6 -->
        <div class="glass-card rounded-3xl p-3 reveal delay-200 group">
          <div class="overflow-hidden rounded-2xl aspect-[4/3]">
            <img src="https://picsum.photos/seed/chili-pepper-red/600/450.jpg" alt="Cabai" class="w-full h-full object-cover product-img" />
          </div>
          <div class="p-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="font-serif text-xl font-medium">Cabai Merah</h3>
              <span class="bg-red-600/20 text-red-400 text-xs font-bold px-3 py-1 rounded-full">Populer</span>
            </div>
            <p class="text-stone-500 text-sm mb-4">Cabai merah keriting segar dan pedas, kondisi prima langsung dari petani.</p>
            <div class="flex items-center justify-between">
              <span class="text-green-400 font-serif text-xl font-medium">Rp 35.000<span class="text-stone-500 text-xs font-sans">/kg</span></span>
              <button onclick="orderProduct('Cabai Merah')" class="bg-green-600 hover:bg-green-700 text-white text-xs font-bold uppercase tracking-wider px-4 py-2 rounded-full transition-all hover:scale-105">
                <span class="iconify inline-block mr-1" data-icon="mdi:cart-plus"></span>Pesan
              </button>
            </div>
          </div>
        </div>

      </div>

      <!-- More Products Row -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-x-6 gap-y-10 mt-10">

        <!-- Product 7 -->
        <div class="glass-card rounded-3xl p-3 reveal group">
          <div class="overflow-hidden rounded-2xl aspect-[4/3]">
            <img src="https://picsum.photos/seed/potato-tuber-fresh/600/450.jpg" alt="Kentang" class="w-full h-full object-cover product-img" />
          </div>
          <div class="p-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="font-serif text-xl font-medium">Kentang</h3>
              <span class="bg-yellow-600/20 text-yellow-400 text-xs font-bold px-3 py-1 rounded-full">Import</span>
            </div>
            <p class="text-stone-500 text-sm mb-4">Kentang berkualitas tinggi, bertekstur padat dan cocok untuk digoreng atau direbus.</p>
            <div class="flex items-center justify-between">
              <span class="text-green-400 font-serif text-xl font-medium">Rp 14.000<span class="text-stone-500 text-xs font-sans">/kg</span></span>
              <button onclick="orderProduct('Kentang')" class="bg-green-600 hover:bg-green-700 text-white text-xs font-bold uppercase tracking-wider px-4 py-2 rounded-full transition-all hover:scale-105">
                <span class="iconify inline-block mr-1" data-icon="mdi:cart-plus"></span>Pesan
              </button>
            </div>
          </div>
        </div>

        <!-- Product 8 -->
        <div class="glass-card rounded-3xl p-3 reveal delay-100 group md:translate-y-8">
          <div class="overflow-hidden rounded-2xl aspect-[4/3]">
            <img src="https://picsum.photos/seed/green-beans-vegetable/600/450.jpg" alt="Kacang Panjang" class="w-full h-full object-cover product-img" />
          </div>
          <div class="p-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="font-serif text-xl font-medium">Kacang Panjang</h3>
              <span class="bg-green-600/20 text-green-400 text-xs font-bold px-3 py-1 rounded-full">Organik</span>
            </div>
            <p class="text-stone-500 text-sm mb-4">Kacang panjang segar dan renyah, pelengkap sempurna untuk sayur lodeh.</p>
            <div class="flex items-center justify-between">
              <span class="text-green-400 font-serif text-xl font-medium">Rp 10.000<span class="text-stone-500 text-xs font-sans">/ikat</span></span>
              <button onclick="orderProduct('Kacang Panjang')" class="bg-green-600 hover:bg-green-700 text-white text-xs font-bold uppercase tracking-wider px-4 py-2 rounded-full transition-all hover:scale-105">
                <span class="iconify inline-block mr-1" data-icon="mdi:cart-plus"></span>Pesan
              </button>
            </div>
          </div>
        </div>

        <!-- Product 9 -->
        <div class="glass-card rounded-3xl p-3 reveal delay-200 group">
          <div class="overflow-hidden rounded-2xl aspect-[4/3]">
            <img src="https://picsum.photos/seed/cucumber-salad-green/600/450.jpg" alt="Timun" class="w-full h-full object-cover product-img" />
          </div>
          <div class="p-5">
            <div class="flex items-center justify-between mb-2">
              <h3 class="font-serif text-xl font-medium">Timun Segar</h3>
              <span class="bg-green-600/20 text-green-400 text-xs font-bold px-3 py-1 rounded-full">Segar</span>
            </div>
            <p class="text-stone-500 text-sm mb-4">Timun hijau segar dan berair, menyegarkan untuk salad atau lalapan.</p>
            <div class="flex items-center justify-between">
              <span class="text-green-400 font-serif text-xl font-medium">Rp 7.000<span class="text-stone-500 text-xs font-sans">/kg</span></span>
              <button onclick="orderProduct('Timun Segar')" class="bg-green-600 hover:bg-green-700 text-white text-xs font-bold uppercase tracking-wider px-4 py-2 rounded-full transition-all hover:scale-105">
                <span class="iconify inline-block mr-1" data-icon="mdi:cart-plus"></span>Pesan
              </button>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- ===== TENTANG ===== -->
  <section id="tentang" class="relative py-32 px-6 overflow-hidden">
    <!-- BG Image -->
    <div class="absolute inset-0">
      <img src="https://picsum.photos/seed/farm-field-landscape/1920/1080.jpg" alt="Kebun" class="w-full h-full object-cover opacity-20" />
      <div class="absolute inset-0 bg-gradient-to-b from-stone-900 via-stone-950/90 to-stone-950"></div>
    </div>

    <div class="relative z-10 max-w-screen-xl mx-auto flex flex-col lg:flex-row items-center gap-16 lg:gap-20">
      <!-- Image Side -->
      <div class="lg:w-2/5 reveal">
        <div class="relative">
          <img src="https://picsum.photos/seed/vegetable-basket-harvest/600/800.jpg" alt="Keranjang Sayuran" class="w-full aspect-[3/4] object-cover rounded-2xl" style="box-shadow: 0 25px 50px -12px rgba(0,0,0,0.25);" />
          <div class="absolute -bottom-6 -right-6 bg-green-600 text-white p-6 rounded-2xl" style="box-shadow: 0 25px 50px -12px rgba(0,0,0,0.5);">
            <div class="text-4xl font-serif font-medium">10+</div>
            <div class="text-xs uppercase tracking-widest font-bold mt-1">Tahun Melayani</div>
          </div>
        </div>
      </div>

      <!-- Text Side -->
      <div class="lg:w-3/5 reveal delay-200">
        <span class="inline-block text-xs font-bold uppercase tracking-[0.3em] text-green-400 mb-4">Tentang Kami</span>
        <h2 class="font-serif text-4xl md:text-6xl font-normal leading-[0.85] tracking-tighter mb-8">
          Amanah,<br><span class="italic text-green-400">Berkah dari Bumi</span>
        </h2>
        <p class="text-lg font-light text-stone-400 leading-relaxed mb-6">
          Toko Sayuran Amanah hadir sejak lebih dari 10 tahun lalu dengan satu komitmen: menyediakan sayuran segar berkualitas tinggi dengan harga yang jujur dan terjangkau. Nama "Amanah" bukan sekadar nama — itu adalah janji kami kepada setiap pelanggan.
        </p>
        <p class="text-lg font-light text-stone-400 leading-relaxed mb-10">
          Kami bekerja sama langsung dengan petani lokal untuk memastikan setiap sayuran yang sampai ke tangan Anda dalam kondisi terbaik. Tanpa pestisida berlebihan, tanpa bahan pengawet — hanya kesegaran alami dari alam.
        </p>

        <div class="grid grid-cols-2 gap-6">
          <div class="flex items-start gap-3">
            <div class="w-10 h-10 rounded-xl bg-green-600/20 flex items-center justify-center flex-shrink-0 mt-1">
              <span class="iconify text-green-400 text-xl" data-icon="mdi:shield-check"></span>
            </div>
            <div>
              <h4 class="font-medium text-cream mb-1">Garansi Segar</h4>
              <p class="text-sm text-stone-500">Uang kembali jika tidak segar</p>
            </div>
          </div>
          <div class="flex items-start gap-3">
            <div class="w-10 h-10 rounded-xl bg-green-600/20 flex items-center justify-center flex-shrink-0 mt-1">
              <span class="iconify text-green-400 text-xl" data-icon="mdi:truck-delivery"></span>
            </div>
            <div>
              <h4 class="font-medium text-cream mb-1">Antar Gratis</h4>
              <p class="text-sm text-stone-500">Minimal pembelian Rp 50.000</p>
            </div>
          </div>
          <div class="flex items-start gap-3">
            <div class="w-10 h-10 rounded-xl bg-green-600/20 flex items-center justify-center flex-shrink-0 mt-1">
              <span class="iconify text-green-400 text-xl" data-icon="mdi:heart-outline"></span>
            </div>
            <div>
              <h4 class="font-medium text-cream mb-1">Dipilih Tangan</h4>
              <p class="text-sm text-stone-500">Sortir manual satu per satu</p>
            </div>
          </div>
          <div class="flex items-start gap-3">
            <div class="w-10 h-10 rounded-xl bg-green-600/20 flex items-center justify-center flex-shrink-0 mt-1">
              <span class="iconify text-green-400 text-xl" data-icon="mdi:leaf"></span>
            </div>
            <div>
              <h4 class="font-medium text-cream mb-1">100% Alami</h4>
              <p class="text-sm text-stone-500">Tanpa bahan pengawet</p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== KEUNGGULAN ===== -->
  <section id="keunggulan" class="py-32 px-6 bg-green-900 rounded-t-[3rem] relative overflow-hidden">
    <div class="absolute inset-0 bg-gradient-to-b from-green-900 to-stone-950"></div>

    <div class="relative z-10 max-w-screen-xl mx-auto">
      <!-- Header -->
      <div class="text-center mb-20 reveal">
        <span class="inline-block text-xs font-bold uppercase tracking-[0.3em] text-green-400 mb-4">Mengapa Amanah?</span>
        <h2 class="font-serif text-4xl md:text-6xl font-normal leading-[0.85] tracking-tighter text-cream">
          Keunggulan<br><span class="italic text-green-400">Kami</span>
        </h2>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <!-- Card 1 -->
        <div class="bg-white/5 border border-white/10 rounded-3xl p-8 text-center reveal hover:bg-white/10 hover:border-white/20 transition-all duration-500 hover:-translate-y-2 group">
          <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-green-600/20 flex items-center justify-center group-hover:scale-110 transition-transform duration-300">
            <span class="iconify text-green-400 text-3xl" data-icon="mdi:sprout"></span>
          </div>
          <h3 class="font-serif text-xl font-medium text-cream mb-3">Langsung dari Petani</h3>
          <p class="text-stone-400 font-light leading-relaxed">Kami membeli langsung dari petani lokal tanpa perantara, sehingga kesegaran terjaga dan harga lebih terjangkau.</p>
        </div>

        <!-- Card 2 -->
        <div class="bg-white/5 border border-white/10 rounded-3xl p-8 text-center reveal delay-100 hover:bg-white/10 hover:border-white/20 transition-all duration-500 hover:-translate-y-2 group">
          <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-green-600/20 flex items-center justify-center group-hover:scale-110 transition-transform duration-300">
            <span class="iconify text-green-400 text-3xl" data-icon="mdi:clock-check-outline"></span>
          </div>
          <h3 class="font-serif text-xl font-medium text-cream mb-3">Panen Pagi, Sampai Pagi</h3>
          <p class="text-stone-400 font-light leading-relaxed">Sayuran dipanen di pagi hari dan langsung dikirim, memastikan Anda mendapatkan kesegaran maksimal.</p>
        </div>

        <!-- Card 3 -->
        <div class="bg-white/5 border border-white/10 rounded-3xl p-8 text-center reveal delay-200 hover:bg-white/10 hover:border-white/20 transition-all duration-500 hover:-translate-y-2 group">
          <div class="w-16 h-16 mx-auto mb-6 rounded-2xl bg-green-600/20 flex items-center justify-center group-hover:scale-110 transition-transform duration-300">
            <span class="iconify text-green-400 text-3xl" data-icon="mdi:handshake-outline"></span>
          </div>
          <h3 class="font-serif text-xl font-medium text-cream mb-3">Amanah & Terpercaya</h3>
          <p class="text-stone-400 font-light leading-relaxed">Timbangan jujur, kualitas terjamin, dan pelayanan ramah. Lebih dari 5.000 pelanggan mempercayai kami.</p>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== TESTIMONIAL ===== -->
  <section class="py-32 px-6 bg-stone-950">
    <div class="max-w-screen-xl mx-auto">
      <div class="text-center mb-16 reveal">
        <span class="inline-block text-xs font-bold uppercase tracking-[0.3em] text-green-400 mb-4">Testimoni</span>
        <h2 class="font-serif text-4xl md:text-6xl font-normal leading-[0.85] tracking-tighter">
          Kata <span class="italic text-green-400">Pelanggan</span>
        </h2>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <div class="glass-card rounded-3xl p-8 reveal">
          <div class="flex items-center gap-1 mb-4">
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
          </div>
          <p class="text-stone-400 font-light leading-relaxed mb-6">"Sayurannya selalu segar dan harganya sangat bersaing. Sudah langganan lebih dari 3 tahun dan tidak pernah kecewa!"</p>
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-full bg-green-600/30 flex items-center justify-center">
              <span class="text-green-400 font-serif font-medium">B</span>
            </div>
            <div>
              <div class="font-medium text-cream text-sm">Bu Sari</div>
              <div class="text-stone-500 text-xs">Pelanggan Setia</div>
            </div>
          </div>
        </div>

        <div class="glass-card rounded-3xl p-8 reveal delay-100">
          <div class="flex items-center gap-1 mb-4">
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
          </div>
          <p class="text-stone-400 font-light leading-relaxed mb-6">"Pelayanannya ramah, antarannya cepat, dan yang paling penting timbangannya jujur. Sesuai namanya, Amanah!"</p>
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-full bg-green-600/30 flex items-center justify-center">
              <span class="text-green-400 font-serif font-medium">P</span>
            </div>
            <div>
              <div class="font-medium text-cream text-sm">Pak Ahmad</div>
              <div class="text-stone-500 text-xs">Pemilik Warung</div>
            </div>
          </div>
        </div>

        <div class="glass-card rounded-3xl p-8 reveal delay-200">
          <div class="flex items-center gap-1 mb-4">
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star"></span>
            <span class="iconify text-yellow-400" data-icon="mdi:star-half-full"></span>
          </div>
          <p class="text-stone-400 font-light leading-relaxed mb-6">"Saya pesan via WhatsApp dan within 1 jam sudah sampai. Sayuran organiknya benar-benar berkualitas, anak-anak suka!"</p>
          <div class="flex items-center gap-3">
            <div class="w-10 h-10 rounded-full bg-green-600/30 flex items-center justify-center">
              <span class="text-green-400 font-serif font-medium">M</span>
            </div>
            <div>
              <div class="font-medium text-cream text-sm">Mbak Dewi</div>
              <div class="text-stone-500 text-xs">Ibu Rumah Tangga</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- ===== KONTAK ===== -->
  <section id="kontak" class="py-32 px-6 bg-stone-900 rounded-t-[3rem]" style="box-shadow: 0 -10px 40px rgba(0,0,0,0.03);">
    <div class="max-w-screen-xl mx-auto">
      <div class="flex flex-col lg:flex-row gap-16 lg:gap-20">

        <!-- Left: Info -->
        <div class="lg:w-2/5 reveal">
          <span class="inline-block text-xs font-bold uppercase tracking-[0.3em] text-green-400 mb-4">Hubungi Kami</span>
          <h2 class="font-serif text-4xl md:text-6xl font-normal leading-[0.85] tracking-tighter mb-8">
            Mari<br><span class="italic text-green-400">Terhubung</span>
          </h2>
          <p class="text-lg font-light text-stone-400 leading-relaxed mb-10">
            Punya pertanyaan atau ingin pesan sayuran? Jangan ragu untuk menghubungi kami melalui salah satu kanal berikut.
          </p>

          <div class="space-y-6">
            <!-- Phone -->
            <a href="tel:+62083182339790" class="flex items-center gap-4 group">
              <div class="w-14 h-14 rounded-2xl bg-green-600/20 flex items-center justify-center group-hover:bg-green-600/30 transition-colors duration-300">
                <span class="iconify text-green-400 text-2xl" data-icon="mdi:phone"></span>
              </div>
              <div>
                <div class="text-xs text-stone-500 uppercase tracking-widest font-bold mb-1">Telepon / WhatsApp</div>
                <div class="text-cream font-medium group-hover:text-green-400 transition-colors duration-300">0831-8233-9790</div>
              </div>
            </a>

            <!-- Instagram -->
            <a href="https://instagram.com/amanahjaya" target="_blank" class="flex items-center gap-4 group">
              <div class="w-14 h-14 rounded-2xl bg-green-600/20 flex items-center justify-center group-hover:bg-green-600/30 transition-colors duration-300">
                <span class="iconify text-green-400 text-2xl" data-icon="mdi:instagram"></span>
              </div>
              <div>
                <div class="text-xs text-stone-500 uppercase tracking-widest font-bold mb-1">Instagram</div>
                <div class="text-cream font-medium group-hover:text-green-400 transition-colors duration-300">@amanahjaya</div>
              </div>
            </a>

            <!-- Location -->
            <div class="flex items-center gap-4">
              <div class="w-14 h-14 rounded-2xl bg-green-600/20 flex items-center justify-center">
                <span class="iconify text-green-400 text-2xl" data-icon="mdi:map-marker"></span>
              </div>
              <div>
                <div class="text-xs text-stone-500 uppercase tracking-widest font-bold mb-1">Lokasi</div>
                <div class="text-cream font-medium">Pasar Sayur Tradisional</div>
              </div>
            </div>

            <!-- Hours -->
            <div class="flex items-center gap-4">
              <div class="w-14 h-14 rounded-2xl bg-green-600/20 flex items-center justify-center">
                <span class="iconify text-green-400 text-2xl" data-icon="mdi:clock-outline"></span>
              </div>
              <div>
                <div class="text-xs text-stone-500 uppercase tracking-widest font-bold mb-1">Jam Buka</div>
                <div class="text-cream font-medium">05.00 — 17.00 WIB</div>
              </div>
            </div>
          </div>
        </div>

        <!-- Right: Form -->
        <div class="lg:w-3/5 reveal delay-200">
          <form id="contact-form" class="glass-card rounded-3xl p-8 md:p-10">
            <h3 class="font-serif text-2xl font-medium mb-6">Kirim Pesan</h3>
            <div class="grid grid-cols-1 md:grid-cols-2 gap-6 mb-6">
              <div>
                <label class="block text-xs uppercase tracking-widest font-bold text-stone-500 mb-2">Nama</label>
                <input type="text" required placeholder="Nama Anda" class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-cream placeholder-stone-600 focus:outline-none focus:border-green-500/50 focus:bg-white/10 transition-all duration-300" />
              </div>
              <div>
                <label class="block text-xs uppercase tracking-widest font-bold text-stone-500 mb-2">No. HP</label>
                <input type="tel" required placeholder="08xxxxxxxxxx" class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-cream placeholder-stone-600 focus:outline-none focus:border-green-500/50 focus:bg-white/10 transition-all duration-300" />
              </div>
            </div>
            <div class="mb-6">
              <label class="block text-xs uppercase tracking-widest font-bold text-stone-500 mb-2">Subjek</label>
              <select class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-cream focus:outline-none focus:border-green-500/50 focus:bg-white/10 transition-all duration-300">
                <option value="" class="bg-stone-900">Pilih Subjek</option>
                <option value="order" class="bg-stone-900">Pemesanan Sayuran</option>
                <option value="info" class="bg-stone-900">Informasi Produk</option>
                <option value="complaint" class="bg-stone-900">Saran & Masukan</option>
                <option value="other" class="bg-stone-900">Lainnya</option>
              </select>
            </div>
            <div class="mb-8">
              <label class="block text-xs uppercase tracking-widest font-bold text-stone-500 mb-2">Pesan</label>
              <textarea rows="4" required placeholder="Tulis pesan Anda..." class="w-full bg-white/5 border border-white/10 rounded-xl px-4 py-3 text-cream placeholder-stone-600 focus:outline-none focus:border-green-500/50 focus:bg-white/10 transition-all duration-300 resize-none"></textarea>
            </div>
            <button type="submit" class="w-full bg-green-600 hover:bg-green-700 text-white font-bold uppercase tracking-wide text-sm py-4 rounded-xl transition-all duration-150 hover:scale-[1.02] shine-effect">
              <span class="iconify inline-block mr-2 -mt-0.5" data-icon="mdi:send"></span>
              Kirim Pesan
            </button>
          </form>
        </div>

      </div>
    </div>
  </section>

  <!-- ===== CTA ===== -->
  <section class="py-24 px-6 bg-green-600 relative overflow-hidden">
    <div class="absolute inset-0 opacity-10">
      <div class="absolute top-10 left-10 text-[200px] font-serif leading-none text-white/10 rotate-12">🌿</div>
      <div class="absolute bottom-10 right-10 text-[150px] font-serif leading-none text-white/10 -rotate-12">🥬</div>
    </div>
    <div class="relative z-10 max-w-screen-md mx-auto text-center reveal">
      <h2 class="font-serif text-4xl md:text-5xl font-normal leading-[0.85] tracking-tighter text-white mb-6">
        Siap Pesan Sayuran <span class="italic">Segar?</span>
      </h2>
      <p class="text-green-100 text-lg font-light mb-10 leading-relaxed">
        Hubungi kami sekarang melalui WhatsApp dan dapatkan sayuran segar langsung ke pintu rumah Anda.
      </p>
      <div class="flex flex-col sm:flex-row items-center justify-center gap-4">
        <a href="https://wa.me/62083182339790" target="_blank" class="bg-white text-green-700 font-bold uppercase tracking-wide text-sm px-8 py-4 rounded-full hover:scale-105 transition-all duration-150 shine-effect inline-flex items-center gap-2">
          <span class="iconify text-xl" data-icon="mdi:whatsapp"></span>
          Chat WhatsApp
        </a>
        <a href="https://instagram.com/amanahjaya" target="_blank" class="bg-white/20 text-white border border-white/30 font-bold uppercase tracking-wide text-sm px-8 py-4 rounded-full hover:bg-white/30 hover:scale-105 transition-all duration-150 inline-flex items-center gap-2">
          <span class="iconify text-xl" data-icon="mdi:instagram"></span>
          @amanahjaya
        </a>
      </div>
    </div>
  </section>

  <!-- ===== FOOTER ===== -->
  <footer class="py-16 px-6 bg-stone-950 border-t border-white/5">
    <div class="max-w-screen-xl mx-auto">
      <div class="grid grid-cols-1 md:grid-cols-4 gap-12 mb-16">
        <!-- Brand -->
        <div class="md:col-span-2">
          <div class="flex items-center gap-3 mb-6">
            <div class="w-10 h-10 rounded-xl bg-green-600 flex items-center justify-center">
              <span class="iconify text-white text-xl" data-icon="mdi:leaf"></span>
            </div>
            <span class="font-serif text-2xl font-medium tracking-tight">Amanah</span>
          </div>
          <p class="text-stone-500 font-light leading-relaxed max-w-md mb-6">
            Toko sayuran segar terpercaya sejak lebih dari 10 tahun. Menyediakan berbagai sayuran pilihan langsung dari petani lokal dengan harga jujur dan terjangkau.
          </p>
          <div class="flex items-center gap-3">
            <a href="https://wa.me/62083182339790" target="_blank" class="w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center hover:bg-green-600/20 hover:border-green-500/30 transition-all duration-300">
              <span class="iconify text-stone-400 hover:text-green-400" data-icon="mdi:whatsapp"></span>
            </a>
            <a href="https://instagram.com/amanahjaya" target="_blank" class="w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center hover:bg-green-600/20 hover:border-green-500/30 transition-all duration-300">
              <span class="iconify text-stone-400 hover:text-green-400" data-icon="mdi:instagram"></span>
            </a>
            <a href="tel:+62083182339790" class="w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center hover:bg-green-600/20 hover:border-green-500/30 transition-all duration-300">
              <span class="iconify text-stone-400 hover:text-green-400" data-icon="mdi:phone"></span>
            </a>
          </div>
        </div>

        <!-- Quick Links -->
        <div>
          <h4 class="text-xs uppercase tracking-widest font-bold text-stone-500 mb-6">Menu</h4>
          <ul class="space-y-3">
            <li><a href="#beranda" class="text-stone-400 hover:text-cream transition-colors duration-300">Beranda</a></li>
            <li><a href="#produk" class="text-stone-400 hover:text-cream transition-colors duration-300">Produk</a></li>
            <li><a href="#tentang" class="text-stone-400 hover:text-cream transition-colors duration-300">Tentang Kami</a></li>
            <li><a href="#keunggulan" class="text-stone-400 hover:text-cream transition-colors duration-300">Keunggulan</a></li>
            <li><a href="#kontak" class="text-stone-400 hover:text-cream transition-colors duration-300">Kontak</a></li>
          </ul>
        </div>

        <!-- Contact -->
        <div>
          <h4 class="text-xs uppercase tracking-widest font-bold text-stone-500 mb-6">Kontak</h4>
          <ul class="space-y-3">
            <li class="flex items-center gap-2 text-stone-400">
              <span class="iconify text-green-400" data-icon="mdi:phone"></span>
              0831-8233-9790
            </li>
            <li class="flex items-center gap-2 text-stone-400">
              <span class="iconify text-green-400" data-icon="mdi:instagram"></span>
              @amanahjaya
            </li>
            <li class="flex items-center gap-2 text-stone-400">
              <span class="iconify text-green-400" data-icon="mdi:clock-outline"></span>
              05.00 — 17.00 WIB
            </li>
          </ul>
        </div>
      </div>

      <!-- Bottom -->
      <div class="border-t border-white/5 pt-8 flex flex-col md:flex-row items-center justify-between gap-4">
        <p class="text-stone-600 text-sm">&copy; 2025 Toko Sayuran Amanah. Segar, Jujur, Terpercaya.</p>
        <p class="text-stone-700 text-xs">Dibuat dengan <span class="text-green-400">♥</span> untuk pelanggan setia</p>
      </div>
    </div>
  </footer>

  <!-- ===== FLOATING WHATSAPP ===== -->
  <a href="https://wa.me/62083182339790" target="_blank" class="fixed bottom-6 right-6 z-50 w-14 h-14 bg-green-600 hover:bg-green-700 rounded-full flex items-center justify-center shadow-2xl hover:scale-110 transition-all duration-300 animate-float" title="Chat WhatsApp">
    <span class="iconify text-white text-3xl" data-icon="mdi:whatsapp"></span>
  </a>

  <script>
    // ===== NAVBAR SCROLL =====
    const navbar = document.getElementById('navbar');
    window.addEventListener('scroll', () => {
      if (window.scrollY > 50) {
        navbar.classList.add('nav-scrolled');
      } else {
        navbar.classList.remove('nav-scrolled');
      }
    });

    // ===== MOBILE MENU =====
    const menuToggle = document.getElementById('menu-toggle');
    const mobileMenu = document.getElementById('mobile-menu');
    const menuIcon = document.getElementById('menu-icon');
    let menuOpen = false;

    menuToggle.addEventListener('click', () => {
      menuOpen = !menuOpen;
      mobileMenu.classList.toggle('open');
      menuIcon.setAttribute('data-icon', menuOpen ? 'mdi:close' : 'mdi:menu');
    });

    function closeMobileMenu() {
      menuOpen = false;
      mobileMenu.classList.remove('open');
      menuIcon.setAttribute('data-icon', 'mdi:menu');
    }

    // ===== REVEAL ON SCROLL =====
    const revealElements = document.querySelectorAll('.reveal');
    const revealObserver = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('active');
        }
      });
    }, { threshold: 0.1, rootMargin: '0px 0px -50px 0px' });

    revealElements.forEach(el => revealObserver.observe(el));

    // ===== TOAST =====
    function showToast(message) {
      const toast = document.getElementById('toast');
      const toastMsg = document.getElementById('toast-msg');
      toastMsg.textContent = message;
      toast.classList.add('show');
      setTimeout(() => toast.classList.remove('show'), 3000);
    }

    // ===== ORDER PRODUCT =====
    function orderProduct(productName) {
      const waLink = `https://wa.me/62083182339790?text=${encodeURIComponent('Halo Toko Amanah! Saya ingin memesan ' + productName + '. Apakah masih tersedia?')}`;
      window.open(waLink, '_blank');
    }

    // ===== CONTACT FORM =====
    document.getElementById('contact-form').addEventListener('submit', (e) => {
      e.preventDefault();
      showToast('Pesan berhasil dikirim! Kami akan segera menghubungi Anda.');
      e.target.reset();
    });
  </script>

</body>
</html>
