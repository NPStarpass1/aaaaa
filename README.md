<!doctype html>
<html lang="th" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Electronics Shop</title>
  <script src="https://cdn.tailwindcss.com/3.4.17"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Prompt:wght@300;400;500;600;700&amp;display=swap" rel="stylesheet">
  <style>
    * { font-family: 'Prompt', sans-serif; }
    .product-card {
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .product-card:hover {
      transform: translateY(-8px);
      box-shadow: 0 20px 40px rgba(0,0,0,0.15);
    }
    .gradient-bg {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    }
    .btn-cart {
      transition: all 0.2s ease;
    }
    .btn-cart:hover {
      transform: scale(1.05);
    }
    .badge-sale {
      animation: pulse 2s infinite;
    }
    @keyframes pulse {
      0%, 100% { opacity: 1; }
      50% { opacity: 0.8; }
    }
    .category-btn {
      transition: all 0.2s ease;
    }
    .category-btn:hover, .category-btn.active {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
    }
    .cart-badge {
      animation: bounce 0.5s ease;
    }
    @keyframes bounce {
      0%, 100% { transform: scale(1); }
      50% { transform: scale(1.2); }
    }
  </style>
  <style>body { box-sizing: border-box; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
 </head>
 <body class="h-full bg-gray-50">
  <div id="app" class="h-full overflow-auto"><!-- Header -->
   <header class="gradient-bg text-white sticky top-0 z-50 shadow-lg">
    <div class="max-w-7xl mx-auto px-4 py-4">
     <div class="flex items-center justify-between">
      <div class="flex items-center gap-3">
       <div class="w-12 h-12 bg-white/20 rounded-xl flex items-center justify-center backdrop-blur">
        <svg class="w-7 h-7" fill="currentColor" viewbox="0 0 24 24"><path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z" />
        </svg>
       </div>
       <div>
        <h1 id="store-name" class="text-xl font-bold">ร้านขายเศษเหล็ก</h1>
        <p id="store-tagline" class="text-sm text-white/80">ราคาไม่ดีมา 1-1 กับกุ</p>
       </div>
      </div>
      <div class="flex items-center gap-4"><!-- Search -->
       <div class="hidden md:flex items-center bg-white/20 rounded-full px-4 py-2 backdrop-blur">
        <svg class="w-5 h-5 text-white/70" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
        </svg><input type="text" id="search-input" placeholder="ค้นหาสินค้า..." class="bg-transparent border-none outline-none text-white placeholder-white/70 ml-2 w-48">
       </div><!-- Cart Button --> <button id="cart-btn" class="relative bg-white/20 p-3 rounded-full hover:bg-white/30 transition backdrop-blur">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
        </svg><span id="cart-count" class="absolute -top-1 -right-1 bg-red-500 text-white text-xs w-5 h-5 rounded-full flex items-center justify-center font-bold cart-badge">0</span> </button>
      </div>
     </div>
    </div>
   </header><!-- Categories -->
   <div class="max-w-7xl mx-auto px-4 py-6">
    <div class="flex flex-wrap gap-3 justify-center"><button class="category-btn active px-5 py-2 rounded-full bg-gray-200 font-medium text-sm" data-category="all">ทั้งหมด</button> <button class="category-btn px-5 py-2 rounded-full bg-gray-200 font-medium text-sm" data-category="phone">📱 สมาร์ทโฟน</button> <button class="category-btn px-5 py-2 rounded-full bg-gray-200 font-medium text-sm" data-category="laptop">💻 โน้ตบุ๊ค</button> <button class="category-btn px-5 py-2 rounded-full bg-gray-200 font-medium text-sm" data-category="audio">🎧 หูฟัง/ลำโพง</button> <button class="category-btn px-5 py-2 rounded-full bg-gray-200 font-medium text-sm" data-category="accessory">⌨️ อุปกรณ์เสริม</button> <button class="category-btn px-5 py-2 rounded-full bg-gray-200 font-medium text-sm" data-category="gaming">🎮 Gaming</button>
    </div>
   </div><!-- Products Grid -->
   <main class="max-w-7xl mx-auto px-4 pb-8">
    <div id="products-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6"><!-- Products will be rendered here -->
    </div>
   </main><!-- Cart Modal -->
   <div id="cart-modal" class="fixed inset-0 bg-black/50 z-50 hidden items-center justify-center p-4">
    <div class="bg-white rounded-2xl max-w-lg w-full max-h-[80%] overflow-hidden shadow-2xl">
     <div class="gradient-bg text-white p-5 flex items-center justify-between">
      <h2 class="text-xl font-bold">🛒 ตะกร้าสินค้า</h2><button id="close-cart" class="hover:bg-white/20 p-2 rounded-full transition">
       <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
       </svg></button>
     </div>
     <div id="cart-items" class="p-5 overflow-y-auto max-h-80"><!-- Cart items will be rendered here -->
     </div>
     <div class="border-t p-5 bg-gray-50">
      <div class="flex justify-between items-center mb-4"><span class="text-gray-600">รวมทั้งหมด:</span> <span id="cart-total" class="text-2xl font-bold text-purple-600">฿0</span>
      </div><button id="checkout-btn" class="w-full gradient-bg text-white py-3 rounded-xl font-semibold hover:opacity-90 transition"> สั่งซื้อผ่าน Line </button>
     </div>
    </div>
   </div><!-- Checkout Form Modal -->
   <div id="checkout-modal" class="fixed inset-0 bg-black/50 z-50 hidden items-center justify-center p-4 overflow-y-auto">
    <div class="bg-white rounded-2xl max-w-2xl w-full my-8 shadow-2xl">
     <div class="gradient-bg text-white p-5 flex items-center justify-between">
      <h2 class="text-xl font-bold">📋 ข้อมูลสั่งซื้อ</h2><button id="close-checkout" class="hover:bg-white/20 p-2 rounded-full transition">
       <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
       </svg></button>
     </div>
     <div class="p-6 max-h-96 overflow-y-auto">
      <form id="checkout-form">
       <!-- Customer Info -->
       <div class="mb-6">
        <h3 class="text-lg font-semibold text-gray-800 mb-4">ข้อมูลลูกค้า</h3>
        <div class="space-y-4">
         <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">ชื่อ-สกุล *</label> <input type="text" id="customer-name" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="ชื่อ-สกุล">
         </div>
         <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">อีเมล *</label> <input type="email" id="customer-email" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="example@email.com">
         </div>
         <div>
          <label class="block text-sm font-medium text-gray-700 mb-2">เบอร์โทรศัพท์ *</label> <input type="tel" id="customer-phone" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="08x-xxx-xxxx">
         </div>
        </div>
       </div><!-- Shipping Info -->
       <div class="mb-6">
        <h3 class="text-lg font-semibold text-gray-800 mb-4">ที่อยู่ส่งของ</h3>
        <div>
         <label class="block text-sm font-medium text-gray-700 mb-2">ที่อยู่ *</label> <textarea id="customer-address" required class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="ใส่ที่อยู่ เลขที่ ซอย ถนน จังหวัด" rows="3"></textarea>
        </div>
       </div><!-- Payment Method -->
       <div class="mb-6">
        <h3 class="text-lg font-semibold text-gray-800 mb-4">วิธีการชำระเงิน</h3>
        <div class="space-y-3">
         <label class="flex items-center p-3 border border-gray-300 rounded-lg cursor-pointer hover:bg-purple-50"> <input type="radio" name="payment-method" value="cod" required class="mr-3"> <span class="flex-1"> <span class="font-medium text-gray-800">เก็บปลายทาง</span> <span class="text-sm text-gray-500">ชำระเงินเมื่อได้รับสินค้า</span> </span> </label> <label class="flex items-center p-3 border border-gray-300 rounded-lg cursor-pointer hover:bg-purple-50"> <input type="radio" name="payment-method" value="transfer" required class="mr-3"> <span class="flex-1"> <span class="font-medium text-gray-800">โอนเงินล่วงหน้า</span> <span class="text-sm text-gray-500">โอนเงินก่อนจัดส่ง</span> </span> </label>
        </div>
       </div><!-- Order Summary -->
       <div class="bg-gray-50 p-4 rounded-lg mb-6">
        <h3 class="font-semibold text-gray-800 mb-3">สรุปการสั่งซื้อ</h3>
        <div id="checkout-summary" class="space-y-2 text-sm max-h-40 overflow-y-auto mb-3">
         <!-- Will be filled by JS -->
        </div>
        <div class="border-t pt-3">
         <div class="flex justify-between font-bold text-lg">
          <span>รวมทั้งหมด:</span> <span id="checkout-total" class="text-purple-600">฿0</span>
         </div>
        </div>
       </div>
       <div class="flex gap-3">
        <button type="button" id="cancel-checkout" class="flex-1 py-2 border border-gray-300 rounded-lg font-medium text-gray-700 hover:bg-gray-50">ยกเลิก</button> <button type="submit" class="flex-1 gradient-bg text-white py-2 rounded-lg font-semibold hover:opacity-90">ต่อไปที่ชำระเงิน</button>
       </div>
      </form>
     </div>
    </div>
   </div><!-- Payment Modal -->
   <div id="payment-modal" class="fixed inset-0 bg-black/50 z-50 hidden items-center justify-center p-4">
    <div class="bg-white rounded-2xl max-w-md w-full shadow-2xl">
     <div class="gradient-bg text-white p-5 flex items-center justify-between">
      <h2 class="text-xl font-bold">💳 ชำระเงิน</h2><button id="close-payment" class="hover:bg-white/20 p-2 rounded-full transition">
       <svg class="w-6 h-6" fill="none" stroke="currentColor" viewbox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
       </svg></button>
     </div>
     <div class="p-6">
      <div id="payment-content">
       <!-- Will be filled based on payment method -->
      </div>
     </div>
    </div>
   </div><!-- Contact Bar -->
   <footer class="bg-gray-900 text-white py-6">
    <div class="max-w-7xl mx-auto px-4">
     <div class="flex flex-col md:flex-row items-center justify-between gap-4">
      <div class="flex items-center gap-6">
       <div class="flex items-center gap-2">
        <svg class="w-5 h-5 text-green-400" fill="currentColor" viewbox="0 0 24 24"><path d="M6.62 10.79c1.44 2.83 3.76 5.14 6.59 6.59l2.2-2.2c.27-.27.67-.36 1.02-.24 1.12.37 2.33.57 3.57.57.55 0 1 .45 1 1V20c0 .55-.45 1-1 1-9.39 0-17-7.61-17-17 0-.55.45-1 1-1h3.5c.55 0 1 .45 1 1 0 1.25.2 2.45.57 3.57.11.35.03.74-.25 1.02l-2.2 2.2z" />
        </svg><span id="contact-phone">080-123-4567</span>
       </div>
       <div class="flex items-center gap-2">
        <svg class="w-5 h-5 text-green-400" viewbox="0 0 24 24" fill="currentColor"><path d="M19.365 9.863c.349 0 .63.285.63.631 0 .345-.281.63-.63.63H17.61v1.125h1.755c.349 0 .63.283.63.63 0 .344-.281.629-.63.629h-2.386c-.345 0-.627-.285-.627-.629V8.108c0-.345.282-.63.63-.63h2.386c.346 0 .627.285.627.63 0 .349-.281.63-.63.63H17.61v1.125h1.755zm-3.855 3.016c0 .27-.174.51-.432.596-.064.021-.133.031-.199.031-.211 0-.391-.09-.51-.25l-2.443-3.317v2.94c0 .344-.279.629-.631.629-.346 0-.626-.285-.626-.629V8.108c0-.27.173-.51.43-.595.06-.023.136-.033.194-.033.195 0 .375.104.495.254l2.462 3.33V8.108c0-.345.282-.63.63-.63.345 0 .63.285.63.63v4.771zm-5.741 0c0 .344-.282.629-.631.629-.345 0-.627-.285-.627-.629V8.108c0-.345.282-.63.63-.63.346 0 .628.285.628.63v4.771zm-2.466.629H4.917c-.345 0-.63-.285-.63-.629V8.108c0-.345.285-.63.63-.63.348 0 .63.285.63.63v4.141h1.756c.348 0 .629.283.629.63 0 .344-.282.629-.629.629M24 10.314C24 4.943 18.615.572 12 .572S0 4.943 0 10.314c0 4.811 4.27 8.842 10.035 9.608.391.082.923.258 1.058.59.12.301.079.766.038 1.08l-.164 1.02c-.045.301-.24 1.186 1.049.645 1.291-.539 6.916-4.078 9.436-6.975C23.176 14.393 24 12.458 24 10.314" />
        </svg><span id="contact-line">@techzone</span>
       </div>
      </div>
      <p class="text-gray-400 text-sm">© 2024 TechZone Store - All Rights Reserved</p>
     </div>
    </div>
   </footer>
  </div>
  <script>
    // Default configuration
    const defaultConfig = {
      store_name: 'TechZone Store',
      store_tagline: 'อุปกรณ์อิเล็กทรอนิกส์คุณภาพ ราคาดี',
      contact_phone: '080-123-4567',
      contact_line: '@techzone',
      primary_color: '#667eea',
      secondary_color: '#764ba2',
      text_color: '#1f2937',
      background_color: '#f9fafb',
      accent_color: '#ef4444'
    };

    // Products data - ใส่ URL รูปภาพของคุณในช่อง image
    const products = [
      {
        id: 1,
        name: 'iPhone 15 Pro Max',
        price: 48900,
        originalPrice: 52900,
        category: 'phone',
        image: 'https://spiritpc.com/service/images/productimg/500/500/e5183678-f384-44c4-ac12-89ddf68d3611.jpeg?own=true',
        badge: 'ขายดี',
        description: '256GB | Titanium Blue'
      },
      {
        id: 2,
        name: 'Samsung Galaxy S24 Ultra',
        price: 44900,
        originalPrice: 49900,
        category: 'phone',
        image: 'https://www.ais.th/content/dam/ais/consumer/store/devices/samsung/phone/galaxy-s24-series/s24-ultra-5g/product-detail/titanium-black/samsung-galaxy-s24-ultra-5g-pdp-position-1-color-titanium-black.jpg',
        badge: 'ใหม่',
        description: '256GB | Titanium Gray'
      },
      {
        id: 3,
        name: 'MacBook Pro 14',
        price: 69900,
        originalPrice: 74900,
        category: 'laptop',
        image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS3q_IPJgyaTW7irwht2sgwomfcwcNX8F2y1g&s',
        badge: '',
        description: 'M3 Pro | 18GB | 512GB SSD'
      },
      
      {
        id: 4,
        name: 'ASUS ROG Strix G16',
        price: 52900,
        originalPrice: 59900,
        category: 'laptop',
        image: 'https://addin.co.th/wp-content/uploads/2026/02/notebook-asus-rog-strix-g16-g614-01.jpg',
        badge: 'Gaming',
        description: 'RTX 4070 | i9 | 32GB RAM'
      },
      {
        id: 5,
        name: 'AirPods Pro 2',
        price: 8900,
        originalPrice: 9490,
        category: 'audio',
        image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTEMOH90lFMAoqyMfT9nG2UhA1z0tR8Itq9rQ&s',
        badge: '',
        description: 'USB-C | Active Noise Cancellation'
      },
      {
        id: 6,
        name: 'Sony WH-1000XM5',
        price: 12900,
        originalPrice: 14900,
        category: 'audio',
        image: 'https://www.istudio.store/cdn/shop/files/SonyWH-1000XM5WirelessHeadphone.001.jpg?v=1733888014&width=823',
        badge: 'แนะนำ',
        description: 'หูฟังครอบหู | Noise Canceling'
      },
      {
        id: 7,
        name: 'Logitech MX Master 3S',
        price: 3590,
        originalPrice: 3990,
        category: 'accessory',
        image: 'https://www.jib.co.th/img_master/product/original/2022081613152454647_1.jpg',
        badge: '',
        description: 'เมาส์ไร้สาย | Ergonomic'
      },
      {
        id: 8,
        name: 'Keychron K8 Pro',
        price: 3290,
        originalPrice: 3690,
        category: 'accessory',
        image: 'https://www.keychron.co.th/cdn/shop/files/cover_e6505dae-d493-437d-be37-f3fa03d1beb4_1200x.jpg?v=1725119082',
        badge: 'Hot',
        description: 'Mechanical Keyboard | RGB'
      },
      {
        id: 9,
        name: 'PlayStation 5 Slim',
        price: 17990,
        originalPrice: 19990,
        category: 'gaming',
        image: 'https://mediam.dotlife.store/media/catalog/product/cache/3b7e899159f673788675d87d1d929a98/s/o/sony-ps5-console-d-chassis.001.jpeg',
        badge: 'ขายดี',
        description: 'Digital Edition | 1TB'
      },
      {
        id: 10,
        name: 'Nintendo Switch OLED',
        price: 12990,
        originalPrice: 13990,
        category: 'gaming',
        image: 'https://mediam.dotlife.store/media/catalog/product/cache/3b7e899159f673788675d87d1d929a98/n/i/nintendo_switch_oled_console.006.jpeg',
        badge: '',
        description: 'White Edition | 7" OLED'
      },
      {
        id: 11,
        name: 'iPad Pro 12.9"',
        price: 44900,
        originalPrice: 49900,
        category: 'laptop',
        image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRsmc7ZNEMURnYBXqwmX3hWlMazKA4dBY_MDg&s',
        badge: 'M2 Chip',
        description: 'M2 | 256GB | Wi-Fi'
      },
      {
        id: 12,
        name: 'JBL Flip 6',
        price: 4290,
        originalPrice: 4990,
        category: 'audio',
        image: 'https://www.central.co.th/_next/image?url=https%3A%2F%2Fassets.central.co.th%2Ffile-assets%2FCDSPIM%2Fweb%2FImage%2FMKP1295%2FJBL-BlackJBLFlip6WirelessPortableBluetoothSpeaker-MKP1295071-4.webp&w=1080&q=75',
        badge: '',
        description: 'ลำโพงบลูทูธ | กันน้ำ IP67'
      }
    ];

    let cart = [];
    let currentCategory = 'all';
    let config = { ...defaultConfig };

    // Format price
    function formatPrice(price) {
      return '฿' + price.toLocaleString('th-TH');
    }

    // Get category icon
    function getCategoryIcon(category) {
      const icons = {
        phone: '📱',
        laptop: '💻',
        audio: '🎧',
        accessory: '⌨️',
        gaming: '🎮'
      };
      return icons[category] || '📦';
    }

    // Render products
    function renderProducts(filter = 'all', searchTerm = '') {
      const grid = document.getElementById('products-grid');
      let filtered = filter === 'all' ? products : products.filter(p => p.category === filter);
      
      if (searchTerm) {
        filtered = filtered.filter(p => 
          p.name.toLowerCase().includes(searchTerm.toLowerCase()) ||
          p.description.toLowerCase().includes(searchTerm.toLowerCase())
        );
      }

      grid.innerHTML = filtered.map(product => `
        <div class="product-card bg-white rounded-2xl overflow-hidden shadow-md">
          <div class="relative">
            <div class="aspect-square bg-gradient-to-br from-gray-100 to-gray-200 flex items-center justify-center overflow-hidden">
              ${product.image ? 
                `<img src="${product.image}" alt="${product.name}" class="w-full h-full object-cover" loading="lazy" onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';">
                 <div class="absolute inset-0 flex flex-col items-center justify-center text-gray-400" style="display:none;">
                   <span class="text-6xl mb-2">${getCategoryIcon(product.category)}</span>
                   <span class="text-sm">ใส่รูปภาพ</span>
                 </div>` :
                `<div class="flex flex-col items-center justify-center text-gray-400">
                   <span class="text-6xl mb-2">${getCategoryIcon(product.category)}</span>
                   <span class="text-sm">ใส่รูปภาพ</span>
                 </div>`
              }
            </div>
            ${product.badge ? `<span class="badge-sale absolute top-3 left-3 bg-red-500 text-white text-xs font-bold px-3 py-1 rounded-full">${product.badge}</span>` : ''}
            ${product.originalPrice > product.price ? `<span class="absolute top-3 right-3 bg-green-500 text-white text-xs font-bold px-2 py-1 rounded-full">-${Math.round((1 - product.price/product.originalPrice) * 100)}%</span>` : ''}
          </div>
          <div class="p-4">
            <h3 class="font-semibold text-gray-800 mb-1 line-clamp-1">${product.name}</h3>
            <p class="text-gray-500 text-sm mb-3">${product.description}</p>
            <div class="flex items-center justify-between">
              <div>
                <span class="text-xl font-bold text-purple-600">${formatPrice(product.price)}</span>
                ${product.originalPrice > product.price ? `<span class="text-sm text-gray-400 line-through ml-2">${formatPrice(product.originalPrice)}</span>` : ''}
              </div>
              <button onclick="addToCart(${product.id})" class="btn-cart bg-gradient-to-r from-purple-500 to-pink-500 text-white p-3 rounded-xl hover:shadow-lg">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6v6m0 0v6m0-6h6m-6 0H6"/>
                </svg>
              </button>
            </div>
          </div>
        </div>
      `).join('');
    }

    // Add to cart
    function addToCart(productId) {
      const product = products.find(p => p.id === productId);
      const existingItem = cart.find(item => item.id === productId);
      
      if (existingItem) {
        existingItem.quantity++;
      } else {
        cart.push({ ...product, quantity: 1 });
      }
      
      updateCartUI();
    }

    // Remove from cart
    function removeFromCart(productId) {
      cart = cart.filter(item => item.id !== productId);
      updateCartUI();
    }

    // Update quantity
    function updateQuantity(productId, change) {
      const item = cart.find(item => item.id === productId);
      if (item) {
        item.quantity += change;
        if (item.quantity <= 0) {
          removeFromCart(productId);
        } else {
          updateCartUI();
        }
      }
    }

    // Update cart UI
    function updateCartUI() {
      const countEl = document.getElementById('cart-count');
      const totalCount = cart.reduce((sum, item) => sum + item.quantity, 0);
      countEl.textContent = totalCount;
      countEl.classList.remove('cart-badge');
      void countEl.offsetWidth;
      countEl.classList.add('cart-badge');

      const cartItemsEl = document.getElementById('cart-items');
      const cartTotalEl = document.getElementById('cart-total');

      if (cart.length === 0) {
        cartItemsEl.innerHTML = `
          <div class="text-center py-8 text-gray-500">
            <svg class="w-16 h-16 mx-auto mb-4 text-gray-300" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z"/>
            </svg>
            <p>ตะกร้าว่างเปล่า</p>
          </div>
        `;
      } else {
        cartItemsEl.innerHTML = cart.map(item => `
          <div class="flex items-center gap-4 py-3 border-b last:border-0">
            <div class="w-16 h-16 bg-gray-100 rounded-xl flex items-center justify-center overflow-hidden flex-shrink-0">
              ${item.image ? 
                `<img src="${item.image}" alt="${item.name}" class="w-full h-full object-cover" loading="lazy" onerror="this.style.display='none'; this.parentElement.innerHTML='<span class=\\'text-2xl\\'>${getCategoryIcon(item.category)}</span>'">` :
                `<span class="text-2xl">${getCategoryIcon(item.category)}</span>`
              }
            </div>
            <div class="flex-1 min-w-0">
              <h4 class="font-medium text-gray-800 text-sm truncate">${item.name}</h4>
              <p class="text-purple-600 font-semibold">${formatPrice(item.price)}</p>
            </div>
            <div class="flex items-center gap-2">
              <button onclick="updateQuantity(${item.id}, -1)" class="w-8 h-8 bg-gray-200 rounded-full flex items-center justify-center hover:bg-gray-300 transition">-</button>
              <span class="w-8 text-center font-medium">${item.quantity}</span>
              <button onclick="updateQuantity(${item.id}, 1)" class="w-8 h-8 bg-gray-200 rounded-full flex items-center justify-center hover:bg-gray-300 transition">+</button>
            </div>
            <button onclick="removeFromCart(${item.id})" class="text-red-500 hover:text-red-700 p-1">
              <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
              </svg>
            </button>
          </div>
        `).join('');
      }

      const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
      cartTotalEl.textContent = formatPrice(total);
    }

    // Generate Line message
    function generateLineMessage() {
      if (cart.length === 0) return;
      
      let message = '🛒 สั่งซื้อสินค้า\n\n';
      cart.forEach(item => {
        message += `📦 ${item.name}\n   จำนวน: ${item.quantity} ชิ้น\n   ราคา: ${formatPrice(item.price * item.quantity)}\n\n`;
      });
      const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
      message += `💰 รวมทั้งหมด: ${formatPrice(total)}`;
      
      const lineId = config.contact_line || defaultConfig.contact_line;
      const encodedMessage = encodeURIComponent(message);
      window.open(`https://line.me/R/oaMessage/${lineId.replace('@', '')}/?${encodedMessage}`, '_blank');
    }

    // Category filter
    document.querySelectorAll('.category-btn').forEach(btn => {
      btn.addEventListener('click', () => {
        document.querySelectorAll('.category-btn').forEach(b => b.classList.remove('active'));
        btn.classList.add('active');
        currentCategory = btn.dataset.category;
        renderProducts(currentCategory, document.getElementById('search-input').value);
      });
    });

    // Search
    document.getElementById('search-input').addEventListener('input', (e) => {
      renderProducts(currentCategory, e.target.value);
    });

    // Cart modal
    document.getElementById('cart-btn').addEventListener('click', () => {
      document.getElementById('cart-modal').classList.remove('hidden');
      document.getElementById('cart-modal').classList.add('flex');
    });

    document.getElementById('close-cart').addEventListener('click', () => {
      document.getElementById('cart-modal').classList.add('hidden');
      document.getElementById('cart-modal').classList.remove('flex');
    });

    document.getElementById('cart-modal').addEventListener('click', (e) => {
      if (e.target.id === 'cart-modal') {
        document.getElementById('cart-modal').classList.add('hidden');
        document.getElementById('cart-modal').classList.remove('flex');
      }
    });

    // Checkout
    document.getElementById('checkout-btn').addEventListener('click', () => {
      if (cart.length === 0) return;
      document.getElementById('cart-modal').classList.add('hidden');
      document.getElementById('cart-modal').classList.remove('flex');
      
      // Show checkout form modal
      document.getElementById('checkout-modal').classList.remove('hidden');
      document.getElementById('checkout-modal').classList.add('flex');
      
      // Load saved data
      loadSavedData();
      
      // Update checkout summary
      const summary = document.getElementById('checkout-summary');
      const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
      document.getElementById('checkout-total').textContent = formatPrice(total);
      
      summary.innerHTML = cart.map(item => `
        <div class="flex justify-between">
          <span>${item.name} × ${item.quantity}</span>
          <span>${formatPrice(item.price * item.quantity)}</span>
        </div>
      `).join('');
    });

    // Close checkout modal
    document.getElementById('close-checkout').addEventListener('click', () => {
      document.getElementById('checkout-modal').classList.add('hidden');
      document.getElementById('checkout-modal').classList.remove('flex');
    });

    document.getElementById('cancel-checkout').addEventListener('click', () => {
      document.getElementById('checkout-modal').classList.add('hidden');
      document.getElementById('checkout-modal').classList.remove('flex');
    });

    // Load saved data from browser
    function loadSavedData() {
      const savedName = localStorage.getItem('customer_name');
      const savedEmail = localStorage.getItem('customer_email');
      const savedPhone = localStorage.getItem('customer_phone');
      const savedAddress = localStorage.getItem('customer_address');
      
      if (savedName) document.getElementById('customer-name').value = savedName;
      if (savedEmail) document.getElementById('customer-email').value = savedEmail;
      if (savedPhone) document.getElementById('customer-phone').value = savedPhone;
      if (savedAddress) document.getElementById('customer-address').value = savedAddress;
    }

    // Save data to browser
    function saveCustomerData() {
      const name = document.getElementById('customer-name').value;
      const email = document.getElementById('customer-email').value;
      const phone = document.getElementById('customer-phone').value;
      const address = document.getElementById('customer-address').value;
      
      if (name) localStorage.setItem('customer_name', name);
      if (email) localStorage.setItem('customer_email', email);
      if (phone) localStorage.setItem('customer_phone', phone);
      if (address) localStorage.setItem('customer_address', address);
    }

    // Checkout form submission
    document.getElementById('checkout-form').addEventListener('submit', (e) => {
      e.preventDefault();
      
      const name = document.getElementById('customer-name').value;
      const email = document.getElementById('customer-email').value;
      const phone = document.getElementById('customer-phone').value;
      const address = document.getElementById('customer-address').value;
      const paymentMethod = document.querySelector('input[name="payment-method"]:checked').value;
      
      // Save data for next time
      saveCustomerData();
      
      // Close checkout modal
      document.getElementById('checkout-modal').classList.add('hidden');
      document.getElementById('checkout-modal').classList.remove('flex');
      
      // Show payment modal
      document.getElementById('payment-modal').classList.remove('hidden');
      document.getElementById('payment-modal').classList.add('flex');
      
      // Show payment details based on method
      const paymentContent = document.getElementById('payment-content');
      const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
      
      if (paymentMethod === 'cod') {
        paymentContent.innerHTML = `
          <div class="text-center">
            <div class="mb-6 p-4 bg-green-50 rounded-lg">
              <svg class="w-16 h-16 mx-auto text-green-500 mb-2" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
              <h3 class="text-lg font-semibold text-gray-800 mb-2">เก็บปลายทาง</h3>
              <p class="text-gray-600">คุณจะชำระเงินเมื่อได้รับสินค้า</p>
            </div>
            
            <div class="text-left bg-gray-50 p-4 rounded-lg mb-4 space-y-2">
              <div><span class="text-gray-600">ชื่อ:</span> <span class="font-medium">${name}</span></div>
              <div><span class="text-gray-600">อีเมล:</span> <span class="font-medium">${email}</span></div>
              <div><span class="text-gray-600">เบอร์:</span> <span class="font-medium">${phone}</span></div>
              <div><span class="text-gray-600">ที่อยู่:</span> <span class="font-medium">${address}</span></div>
              <div class="border-t pt-2 mt-2">
                <span class="text-gray-600">รวมทั้งหมด:</span>
                <span class="font-bold text-xl text-purple-600">${formatPrice(total)}</span>
              </div>
            </div>
            
            <button onclick="completeOrder('${name}', '${email}', '${phone}', '${address}', 'เก็บปลายทาง', '${total}')" class="w-full gradient-bg text-white py-3 rounded-lg font-semibold hover:opacity-90 mb-2">
              ยืนยันการสั่งซื้อ
            </button>
            <button type="button" id="close-payment" class="w-full py-2 border border-gray-300 rounded-lg font-medium text-gray-700 hover:bg-gray-50">
              ยกเลิก
            </button>
          </div>
        `;
      } else {
        paymentContent.innerHTML = `
          <div>
            <div class="mb-4 p-4 bg-blue-50 rounded-lg">
              <h3 class="text-lg font-semibold text-gray-800 mb-2">📋 รายละเอียดบัญชี</h3>
              <div class="text-left space-y-3 font-medium text-gray-800">
                <div>
                  <p class="text-gray-600 text-sm mb-1">ธนาคาร:</p>
                  <p class="text-lg">🏦 ธนาคารกสิกรไทย</p>
                </div>
                <div>
                  <p class="text-gray-600 text-sm mb-1">เลขบัญชี:</p>
                  <p class="text-lg bg-gray-100 p-2 rounded text-center tracking-wider">123-4-56789-0</p>
                </div>
              </div>
            </div>
            
            <div class="text-left bg-gray-50 p-4 rounded-lg mb-4 space-y-2 text-sm">
              <div><span class="text-gray-600">ชื่อ:</span> <span class="font-medium">${name}</span></div>
              <div><span class="text-gray-600">อีเมล:</span> <span class="font-medium">${email}</span></div>
              <div><span class="text-gray-600">เบอร์:</span> <span class="font-medium">${phone}</span></div>
              <div class="border-t pt-2 mt-2">
                <span class="text-gray-600">โอนเงินจำนวน:</span>
                <span class="font-bold text-xl text-purple-600 block">${formatPrice(total)}</span>
              </div>
            </div>
            
            <p class="text-xs text-gray-600 mb-4">หลังจากโอนเงินเรียบร้อย กรุณาแจ้งหลักฐานการโอนเพื่อให้เรากำหนดการจัดส่ง</p>
            
            <button onclick="completeOrder('${name}', '${email}', '${phone}', '${address}', 'โอนเงินล่วงหน้า', '${total}')" class="w-full gradient-bg text-white py-3 rounded-lg font-semibold hover:opacity-90 mb-2">
              ยืนยันว่าได้โอนเงินแล้ว
            </button>
            <button type="button" id="close-payment" class="w-full py-2 border border-gray-300 rounded-lg font-medium text-gray-700 hover:bg-gray-50">
              ยกเลิก
            </button>
          </div>
        `;
      }
      
      // Close button handler
      document.getElementById('close-payment').addEventListener('click', () => {
        document.getElementById('payment-modal').classList.add('hidden');
        document.getElementById('payment-modal').classList.remove('flex');
      });
    });

    // Complete order function
    window.completeOrder = function(name, email, phone, address, method, total) {
      let message = '✅ คำสั่งซื้อเสร็จสิ้น\n\n';
      message += `👤 ชื่อ: ${name}\n`;
      message += `📧 อีเมล: ${email}\n`;
      message += `📱 เบอร์: ${phone}\n`;
      message += `📍 ที่อยู่: ${address}\n`;
      message += `💳 วิธีชำระเงิน: ${method}\n\n`;
      message += '📦 สินค้า:\n';
      cart.forEach(item => {
        message += `   - ${item.name} × ${item.quantity} = ${formatPrice(item.price * item.quantity)}\n`;
      });
      message += `\n💰 รวมทั้งหมด: ${formatPrice(parseInt(total))}`;
      
      const lineId = config.contact_line || defaultConfig.contact_line;
      const encodedMessage = encodeURIComponent(message);
      window.open(`https://line.me/R/oaMessage/${lineId.replace('@', '')}/?${encodedMessage}`, '_blank');
      
      // Close payment modal
      document.getElementById('payment-modal').classList.add('hidden');
      document.getElementById('payment-modal').classList.remove('flex');
      
      // Reset cart and form
      cart = [];
      updateCartUI();
      document.getElementById('checkout-form').reset();
      
      // Show success message
      alert('✅ ส่งข้อมูลไปยัง Line สำเร็จ! ร้านจะติดต่อคุณในเร็วๆ นี้');
    };

    // Element SDK
    async function onConfigChange(newConfig) {
      document.getElementById('store-name').textContent = newConfig.store_name || defaultConfig.store_name;
      document.getElementById('store-tagline').textContent = newConfig.store_tagline || defaultConfig.store_tagline;
      document.getElementById('contact-phone').textContent = newConfig.contact_phone || defaultConfig.contact_phone;
      document.getElementById('contact-line').textContent = newConfig.contact_line || defaultConfig.contact_line;
    }

    function mapToCapabilities(config) {
      return {
        recolorables: [
          {
            get: () => config.background_color || defaultConfig.background_color,
            set: (value) => { config.background_color = value; window.elementSdk.setConfig({ background_color: value }); }
          },
          {
            get: () => config.primary_color || defaultConfig.primary_color,
            set: (value) => { config.primary_color = value; window.elementSdk.setConfig({ primary_color: value }); }
          },
          {
            get: () => config.text_color || defaultConfig.text_color,
            set: (value) => { config.text_color = value; window.elementSdk.setConfig({ text_color: value }); }
          }
        ],
        borderables: [],
        fontEditable: undefined,
        fontSizeable: undefined
      };
    }

    function mapToEditPanelValues(config) {
      return new Map([
        ['store_name', config.store_name || defaultConfig.store_name],
        ['store_tagline', config.store_tagline || defaultConfig.store_tagline],
        ['contact_phone', config.contact_phone || defaultConfig.contact_phone],
        ['contact_line', config.contact_line || defaultConfig.contact_line]
      ]);
    }

    // Initialize
    if (window.elementSdk) {
      window.elementSdk.init({
        defaultConfig,
        onConfigChange,
        mapToCapabilities,
        mapToEditPanelValues
      });
      config = window.elementSdk.config || defaultConfig;
    }

    renderProducts();
    updateCartUI();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9d578d3b862ad32d',t:'MTc3MjM2MTcxMi4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
