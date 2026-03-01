<!doctype html>
<html lang="th" class="h-full">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BBQ Chicken Shopping List</title>
  <script src="https://cdn.tailwindcss.com/3.4.17"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Kanit:wght@300;400;500;600;700&amp;family=Playfair+Display:wght@700&amp;display=swap" rel="stylesheet">
  <style>
    * { font-family: 'Kanit', sans-serif; }
    .title-font { font-family: 'Playfair Display', serif; }
    
    @keyframes flame {
      0%, 100% { transform: scaleY(1) translateY(0); opacity: 1; }
      50% { transform: scaleY(1.2) translateY(-2px); opacity: 0.8; }
    }
    
    @keyframes smoke {
      0% { transform: translateY(0) scale(1); opacity: 0.6; }
      100% { transform: translateY(-20px) scale(1.5); opacity: 0; }
    }
    
    .flame { animation: flame 0.5s ease-in-out infinite; }
    .smoke { animation: smoke 2s ease-out infinite; }
    
    .ingredient-card {
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }
    
    .ingredient-card:hover {
      transform: translateY(-4px);
    }
    
    .checkbox-custom:checked {
      background: linear-gradient(135deg, #f97316 0%, #ea580c 100%);
    }
    
    .btn-adjust {
      transition: all 0.2s ease;
    }
    
    .btn-adjust:active {
      transform: scale(0.95);
    }
    
    .progress-ring {
      transition: stroke-dashoffset 0.5s ease;
    }
    
    input[type="range"] {
      -webkit-appearance: none;
      appearance: none;
      background: transparent;
    }
    
    input[type="range"]::-webkit-slider-track {
      height: 8px;
      border-radius: 4px;
      background: linear-gradient(90deg, #fef3c7 0%, #fbbf24 50%, #f97316 100%);
    }
    
    input[type="range"]::-webkit-slider-thumb {
      -webkit-appearance: none;
      appearance: none;
      width: 28px;
      height: 28px;
      border-radius: 50%;
      background: linear-gradient(135deg, #ffffff 0%, #f1f5f9 100%);
      box-shadow: 0 4px 12px rgba(249, 115, 22, 0.4);
      cursor: pointer;
      margin-top: -10px;
      border: 3px solid #f97316;
    }
  </style>
  <style>body { box-sizing: border-box; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
 </head>
 <body class="h-full bg-gradient-to-br from-amber-50 via-orange-50 to-red-50 overflow-auto">
  <div id="app-container" class="min-h-full w-full"><!-- Header -->
   <header class="relative overflow-hidden bg-gradient-to-r from-orange-600 via-red-500 to-amber-600 text-white py-8 px-6">
    <div class="absolute inset-0 opacity-20">
     <svg class="w-full h-full" viewbox="0 0 100 100" preserveaspectratio="none"><pattern id="grill" patternunits="userSpaceOnUse" width="10" height="10">
       <line x1="0" y1="5" x2="10" y2="5" stroke="currentColor" stroke-width="1" />
      </pattern> <rect fill="url(#grill)" width="100" height="100" />
     </svg>
    </div><!-- Animated flames -->
    <div class="absolute bottom-0 left-0 right-0 flex justify-around">
     <div class="flame text-yellow-400 opacity-60">
      🔥
     </div>
     <div class="flame text-orange-400 opacity-50" style="animation-delay: 0.2s">
      🔥
     </div>
     <div class="flame text-red-400 opacity-40" style="animation-delay: 0.4s">
      🔥
     </div>
     <div class="flame text-yellow-400 opacity-60" style="animation-delay: 0.1s">
      🔥
     </div>
     <div class="flame text-orange-400 opacity-50" style="animation-delay: 0.3s">
      🔥
     </div>
    </div>
    <div class="relative z-10 max-w-4xl mx-auto text-center">
     <div class="inline-block mb-4"><span class="text-6xl">🍗</span>
     </div>
     <h1 id="recipe-title" class="title-font text-4xl md:text-5xl font-bold mb-2 drop-shadow-lg">บาร์บีคิวไก่สูตรเด็ด</h1>
     <p id="subtitle-text" class="text-orange-100 text-lg font-light">ปรับปริมาณส่วนผสมตามจำนวนที่เสิร์ฟ</p>
    </div>
   </header>
   <main class="max-w-4xl mx-auto px-4 py-8"><!-- Servings Control -->
    <section class="bg-white rounded-3xl shadow-xl p-6 mb-8 border border-orange-100">
     <div class="flex flex-col md:flex-row items-center justify-between gap-6">
      <div class="flex items-center gap-4">
       <div class="relative">
        <svg class="w-20 h-20 transform -rotate-90" viewbox="0 0 100 100"><circle cx="50" cy="50" r="45" fill="none" stroke="#fef3c7" stroke-width="8" /> <circle id="progress-circle" class="progress-ring" cx="50" cy="50" r="45" fill="none" stroke="url(#gradient)" stroke-width="8" stroke-linecap="round" stroke-dasharray="283" stroke-dashoffset="141" /> <defs>
          <lineargradient id="gradient" x1="0%" y1="0%" x2="100%" y2="0%">
           <stop offset="0%" stop-color="#f97316" />
           <stop offset="100%" stop-color="#eab308" />
          </lineargradient>
         </defs>
        </svg>
        <div class="absolute inset-0 flex items-center justify-center"><span id="servings-display" class="text-2xl font-bold text-orange-600">4</span>
        </div>
       </div>
       <div>
        <h2 class="text-xl font-semibold text-gray-800">จำนวนที่เสิร์ฟ</h2>
        <p class="text-gray-500 text-sm">เลื่อนเพื่อปรับปริมาณ</p>
       </div>
      </div>
      <div class="flex-1 max-w-md w-full">
       <div class="flex items-center gap-4"><button id="btn-decrease" class="btn-adjust w-12 h-12 rounded-full bg-gradient-to-br from-orange-400 to-red-500 text-white text-2xl font-bold shadow-lg hover:shadow-xl flex items-center justify-center"> − </button> <input type="range" id="servings-slider" min="1" max="20" value="4" class="flex-1 h-8 cursor-pointer"> <button id="btn-increase" class="btn-adjust w-12 h-12 rounded-full bg-gradient-to-br from-orange-400 to-red-500 text-white text-2xl font-bold shadow-lg hover:shadow-xl flex items-center justify-center"> + </button>
       </div>
       <div class="flex justify-between text-sm text-gray-400 mt-2 px-2"><span>1 คน</span> <span>10 คน</span> <span>20 คน</span>
       </div>
      </div>
     </div>
    </section><!-- Progress Bar -->
    <section class="bg-white rounded-2xl shadow-lg p-4 mb-8 border border-orange-100">
     <div class="flex items-center justify-between mb-2"><span class="text-gray-600 font-medium">ความคืบหน้าการเลือกซื้อ</span> <span id="progress-text" class="text-orange-600 font-bold">0%</span>
     </div>
     <div class="h-3 bg-orange-100 rounded-full overflow-hidden">
      <div id="progress-bar" class="h-full bg-gradient-to-r from-orange-400 via-red-400 to-amber-400 rounded-full transition-all duration-500" style="width: 0%"></div>
     </div>
    </section><!-- Ingredients Grid -->
    <section class="mb-8">
     <div class="flex items-center justify-between mb-6">
      <h2 class="text-2xl font-bold text-gray-800 flex items-center gap-2"><span>🛒</span> รายการส่วนผสม</h2><button id="btn-reset" class="px-4 py-2 text-sm bg-gray-100 hover:bg-gray-200 text-gray-600 rounded-full transition-colors"> รีเซ็ตทั้งหมด </button>
     </div>
     <div id="ingredients-container" class="grid grid-cols-1 md:grid-cols-2 gap-4"><!-- Ingredients will be rendered here -->
     </div>
    </section><!-- Summary -->
    <section class="bg-gradient-to-br from-orange-500 via-red-500 to-amber-500 rounded-3xl shadow-xl p-6 text-white">
     <h3 class="text-xl font-bold mb-4 flex items-center gap-2"><span>📋</span> สรุปรายการช้อปปิ้ง</h3>
     <div id="summary-list" class="space-y-2 mb-6 max-h-48 overflow-y-auto"><!-- Summary items will be rendered here -->
     </div>
     <div class="flex flex-col sm:flex-row gap-3"><button id="btn-copy" class="flex-1 bg-white text-orange-600 font-semibold py-3 px-6 rounded-xl hover:bg-orange-50 transition-colors flex items-center justify-center gap-2"> <span>📝</span> คัดลอกรายการ </button> <button id="btn-share" class="flex-1 bg-orange-700 text-white font-semibold py-3 px-6 rounded-xl hover:bg-orange-800 transition-colors flex items-center justify-center gap-2"> <span>📤</span> แชร์รายการ </button>
     </div>
     <div id="copy-toast" class="hidden mt-4 bg-white/20 backdrop-blur rounded-lg p-3 text-center text-sm">
      ✅ คัดลอกรายการเรียบร้อยแล้ว!
     </div>
    </section>
   </main><!-- Footer -->
   <footer class="text-center py-6 text-gray-400 text-sm">
    <p>🍗 ขอให้อร่อยกับบาร์บีคิวไก่! 🔥</p>
   </footer>
  </div>
  <script>
    // Default configuration
    const defaultConfig = {
      recipe_title: 'บาร์บีคิวไก่สูตรเด็ด',
      subtitle_text: 'ปรับปริมาณส่วนผสมตามจำนวนที่เสิร์ฟ',
      primary_color: '#ea580c',
      secondary_color: '#fef3c7',
      text_color: '#1f2937',
      accent_color: '#dc2626',
      surface_color: '#ffffff'
    };

    // Base ingredients for 4 servings
    const baseIngredients = [
      { id: 1, name: 'ไก่ (น่องหรือปีก)', amount: 800, unit: 'กรัม', emoji: '🍗', category: 'เนื้อสัตว์' },
      { id: 2, name: 'ซอสบาร์บีคิว', amount: 200, unit: 'มล.', emoji: '🥫', category: 'ซอส' },
      { id: 3, name: 'น้ำผึ้ง', amount: 60, unit: 'มล.', emoji: '🍯', category: 'ซอส' },
      { id: 4, name: 'ซีอิ๊วขาว', amount: 45, unit: 'มล.', emoji: '🧴', category: 'ซอส' },
      { id: 5, name: 'กระเทียมสับ', amount: 4, unit: 'กลีบ', emoji: '🧄', category: 'เครื่องปรุง' },
      { id: 6, name: 'ขิงสับ', amount: 2, unit: 'ช้อนโต๊ะ', emoji: '🫚', category: 'เครื่องปรุง' },
      { id: 7, name: 'พริกไทยดำ', amount: 1, unit: 'ช้อนชา', emoji: '🌶️', category: 'เครื่องปรุง' },
      { id: 8, name: 'น้ำมันงา', amount: 2, unit: 'ช้อนโต๊ะ', emoji: '🫒', category: 'น้ำมัน' },
      { id: 9, name: 'งาขาว', amount: 2, unit: 'ช้อนโต๊ะ', emoji: '⚪', category: 'ท็อปปิ้ง' },
      { id: 10, name: 'ต้นหอมซอย', amount: 3, unit: 'ต้น', emoji: '🌿', category: 'ท็อปปิ้ง' },
      { id: 11, name: 'มะนาว', amount: 2, unit: 'ลูก', emoji: '🍋', category: 'เครื่องเคียง' },
      { id: 12, name: 'ผักสลัด', amount: 100, unit: 'กรัม', emoji: '🥬', category: 'เครื่องเคียง' }
    ];

    // State
    let servings = 4;
    let checkedItems = new Set();
    const baseServings = 4;

    // DOM Elements
    const servingsDisplay = document.getElementById('servings-display');
    const servingsSlider = document.getElementById('servings-slider');
    const progressCircle = document.getElementById('progress-circle');
    const progressBar = document.getElementById('progress-bar');
    const progressText = document.getElementById('progress-text');
    const ingredientsContainer = document.getElementById('ingredients-container');
    const summaryList = document.getElementById('summary-list');
    const copyToast = document.getElementById('copy-toast');

    // Calculate scaled amount
    function scaleAmount(baseAmount) {
      const scaled = (baseAmount / baseServings) * servings;
      return scaled % 1 === 0 ? scaled : scaled.toFixed(1);
    }

    // Update progress ring
    function updateProgressRing() {
      const maxServings = 20;
      const percentage = servings / maxServings;
      const circumference = 283;
      const offset = circumference - (percentage * circumference);
      progressCircle.style.strokeDashoffset = offset;
    }

    // Update shopping progress
    function updateShoppingProgress() {
      const total = baseIngredients.length;
      const checked = checkedItems.size;
      const percentage = Math.round((checked / total) * 100);
      progressBar.style.width = percentage + '%';
      progressText.textContent = percentage + '%';
    }

    // Render ingredients
    function renderIngredients() {
      const categories = [...new Set(baseIngredients.map(i => i.category))];
      
      ingredientsContainer.innerHTML = categories.map(category => {
        const categoryIngredients = baseIngredients.filter(i => i.category === category);
        return `
          <div class="bg-white rounded-2xl shadow-lg border border-orange-100 overflow-hidden">
            <div class="bg-gradient-to-r from-orange-100 to-amber-100 px-4 py-2">
              <h3 class="font-semibold text-orange-800">${category}</h3>
            </div>
            <div class="p-3 space-y-2">
              ${categoryIngredients.map(ing => `
                <label class="ingredient-card flex items-center gap-3 p-3 rounded-xl cursor-pointer ${checkedItems.has(ing.id) ? 'bg-green-50 border-2 border-green-400' : 'bg-gray-50 border-2 border-transparent hover:bg-orange-50'}">
                  <input type="checkbox" 
                    class="checkbox-custom w-6 h-6 rounded-lg border-2 border-orange-300 appearance-none cursor-pointer checked:border-green-500"
                    data-id="${ing.id}"
                    ${checkedItems.has(ing.id) ? 'checked' : ''}>
                  <span class="text-2xl">${ing.emoji}</span>
                  <div class="flex-1">
                    <p class="font-medium text-gray-800 ${checkedItems.has(ing.id) ? 'line-through text-gray-400' : ''}">${ing.name}</p>
                    <p class="text-sm ${checkedItems.has(ing.id) ? 'text-green-600' : 'text-orange-600'} font-semibold">
                      ${scaleAmount(ing.amount)} ${ing.unit}
                    </p>
                  </div>
                  ${checkedItems.has(ing.id) ? '<span class="text-green-500 text-xl">✓</span>' : ''}
                </label>
              `).join('')}
            </div>
          </div>
        `;
      }).join('');

      // Add event listeners to checkboxes
      document.querySelectorAll('.checkbox-custom').forEach(checkbox => {
        checkbox.addEventListener('change', (e) => {
          const id = parseInt(e.target.dataset.id);
          if (e.target.checked) {
            checkedItems.add(id);
          } else {
            checkedItems.delete(id);
          }
          renderIngredients();
          renderSummary();
          updateShoppingProgress();
        });
      });
    }

    // Render summary
    function renderSummary() {
      const checkedIngredients = baseIngredients.filter(i => checkedItems.has(i.id));
      
      if (checkedIngredients.length === 0) {
        summaryList.innerHTML = '<p class="text-orange-200 text-center py-4">ยังไม่ได้เลือกส่วนผสม</p>';
        return;
      }

      summaryList.innerHTML = checkedIngredients.map(ing => `
        <div class="flex items-center justify-between bg-white/10 rounded-lg px-3 py-2">
          <span>${ing.emoji} ${ing.name}</span>
          <span class="font-bold">${scaleAmount(ing.amount)} ${ing.unit}</span>
        </div>
      `).join('');
    }

    // Update servings
    function updateServings(newValue) {
      servings = Math.max(1, Math.min(20, newValue));
      servingsDisplay.textContent = servings;
      servingsSlider.value = servings;
      updateProgressRing();
      renderIngredients();
      renderSummary();
    }

    // Generate shopping list text
    function generateShoppingListText() {
      const checkedIngredients = baseIngredients.filter(i => checkedItems.has(i.id));
      if (checkedIngredients.length === 0) return '';
      
      const title = document.getElementById('recipe-title').textContent;
      let text = `🍗 ${title} (${servings} ที่)\n`;
      text += '━━━━━━━━━━━━━━━━\n';
      checkedIngredients.forEach(ing => {
        text += `${ing.emoji} ${ing.name}: ${scaleAmount(ing.amount)} ${ing.unit}\n`;
      });
      text += '━━━━━━━━━━━━━━━━\n';
      text += '🔥 ขอให้อร่อย!';
      return text;
    }

    // Event Listeners
    servingsSlider.addEventListener('input', (e) => {
      updateServings(parseInt(e.target.value));
    });

    document.getElementById('btn-decrease').addEventListener('click', () => {
      updateServings(servings - 1);
    });

    document.getElementById('btn-increase').addEventListener('click', () => {
      updateServings(servings + 1);
    });

    document.getElementById('btn-reset').addEventListener('click', () => {
      checkedItems.clear();
      renderIngredients();
      renderSummary();
      updateShoppingProgress();
    });

    document.getElementById('btn-copy').addEventListener('click', async () => {
      const text = generateShoppingListText();
      if (!text) return;
      
      try {
        await navigator.clipboard.writeText(text);
        copyToast.classList.remove('hidden');
        setTimeout(() => copyToast.classList.add('hidden'), 2000);
      } catch (err) {
        console.error('Failed to copy:', err);
      }
    });

    document.getElementById('btn-share').addEventListener('click', async () => {
      const text = generateShoppingListText();
      if (!text) return;
      
      if (navigator.share) {
        try {
          await navigator.share({ title: 'รายการช้อปปิ้ง BBQ ไก่', text });
        } catch (err) {
          console.error('Share failed:', err);
        }
      } else {
        // Fallback to copy
        document.getElementById('btn-copy').click();
      }
    });

    // Element SDK Integration
    async function onConfigChange(config) {
      const title = config.recipe_title || defaultConfig.recipe_title;
      const subtitle = config.subtitle_text || defaultConfig.subtitle_text;
      
      document.getElementById('recipe-title').textContent = title;
      document.getElementById('subtitle-text').textContent = subtitle;
    }

    function mapToCapabilities(config) {
      return {
        recolorables: [
          {
            get: () => config.primary_color || defaultConfig.primary_color,
            set: (value) => {
              config.primary_color = value;
              window.elementSdk.setConfig({ primary_color: value });
            }
          },
          {
            get: () => config.secondary_color || defaultConfig.secondary_color,
            set: (value) => {
              config.secondary_color = value;
              window.elementSdk.setConfig({ secondary_color: value });
            }
          },
          {
            get: () => config.text_color || defaultConfig.text_color,
            set: (value) => {
              config.text_color = value;
              window.elementSdk.setConfig({ text_color: value });
            }
          }
        ],
        borderables: [],
        fontEditable: undefined,
        fontSizeable: undefined
      };
    }

    function mapToEditPanelValues(config) {
      return new Map([
        ['recipe_title', config.recipe_title || defaultConfig.recipe_title],
        ['subtitle_text', config.subtitle_text || defaultConfig.subtitle_text]
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
    }

    // Initial render
    renderIngredients();
    renderSummary();
    updateProgressRing();
    updateShoppingProgress();
  </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9d55a1d7e6ad26e3',t:'MTc3MjM0MTU4NS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
