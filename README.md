<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no">
  <meta name="apple-mobile-web-app-capable" content="yes">
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
  <title>色彩碰撞：解锁你们的亲密CP色</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link href="https://cdn.jsdelivr.net/npm/font-awesome@4.7.0/css/font-awesome.min.css" rel="stylesheet">
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            'pink': '#FF3366',
            'orange': '#FF9933',
            'green': '#33CC66',
            'blue': '#3399FF',
            'purple': '#9966CC'
          },
          fontFamily: {
            sans: ['-apple-system', 'BlinkMacSystemFont', 'Segoe UI', 'Roboto', 'Helvetica', 'Arial', 'sans-serif']
          },
          animation: {
            'float': 'float 3s ease-in-out infinite',
            'confetti': 'confetti 5s ease-in-out infinite',
            'pulse-slow': 'pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite',
            'rainbow-bg': 'rainbowBg 15s ease infinite',
            'door-open': 'doorOpen 1.5s cubic-bezier(0.34, 1.56, 0.64, 1) forwards',
            'spray-in': 'sprayIn 2s ease-out forwards',
            'fade-in-up': 'fadeInUp 0.8s ease-out forwards'
          },
          keyframes: {
            float: {
              '0%, 100%': { transform: 'translateY(0)' },
              '50%': { transform: 'translateY(-10px)' }
            },
            confetti: {
              '0%': { transform: 'translateY(0) rotate(0deg)', opacity: 1 },
              '100%': { transform: 'translateY(100vh) rotate(720deg)', opacity: 0 }
            },
            rainbowBg: {
              '0%': { backgroundPosition: '0% 50%' },
              '50%': { backgroundPosition: '100% 50%' },
              '100%': { backgroundPosition: '0% 50%' }
            },
            doorOpen: {
              '0%': { transform: 'scaleX(0.8) translateX(-50%)', opacity: 0 },
              '100%': { transform: 'scaleX(1) translateX(-50%)', opacity: 1 }
            },
            sprayIn: {
              '0%': { transform: 'scale(0.5) translate(-50%, -50%)', opacity: 0 },
              '70%': { transform: 'scale(1.1) translate(-50%, -50%)', opacity: 0.9 },
              '100%': { transform: 'scale(1) translate(-50%, -50%)', opacity: 0.7 }
            },
            fadeInUp: {
              '0%': { transform: 'translateY(20px)', opacity: 0 },
              '100%': { transform: 'translateY(0)', opacity: 1 }
            }
          }
        }
      }
    }
  </script>
  <style type="text/tailwindcss">
    @layer utilities {
      .text-shadow { text-shadow: 0 2px 4px rgba(0,0,0,0.1); }
      .text-shadow-lg { text-shadow: 0 4px 8px rgba(0,0,0,0.25); }
      .bg-gradient-rainbow {
        background: linear-gradient(90deg, #FF3366, #FF9933, #FFCC00, #33CC66, #3399FF, #9966CC);
        background-size: 600% 600%;
      }
      .mask-gradient {
        mask-image: linear-gradient(to bottom, black 85%, transparent 100%);
        -webkit-mask-image: linear-gradient(to bottom, black 85%, transparent 100%);
      }
      .card-ins {
        background-color: #ffffff;
        border-radius: 16px;
        box-shadow: 0 8px 30px rgba(0, 0, 0, 0.05);
        transition: all 0.3s ease;
        padding: 20px !important;
      }
      .btn-ins {
        border-radius: 8px;
        font-weight: 600;
        transition: all 0.3s ease;
        position: relative;
        overflow: hidden;
        min-height: 44px;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 12px 24px !important;
        font-size: 16px !important;
      }
      .btn-ins::after {
        content: '';
        position: absolute;
        top: 0;
        left: -100%;
        width: 100%;
        height: 100%;
        background: linear-gradient(90deg, transparent, rgba(255,255,255,0.2), transparent);
        transition: 0.5s;
      }
      .btn-ins:hover::after {
        left: 100%;
      }
      .btn-ins-primary {
        background: linear-gradient(135deg, #FF3366, #FF6B81);
        color: white;
      }
      .btn-ins-primary:hover {
        transform: translateY(-2px);
        box-shadow: 0 10px 20px rgba(255, 51, 102, 0.2);
      }
      .btn-ins-secondary {
        background: linear-gradient(135deg, #3399FF, #64B5F6);
        color: white;
      }
      .btn-ins-secondary:hover {
        transform: translateY(-2px);
        box-shadow: 0 10px 20px rgba(51, 153, 255, 0.2);
      }
      .option-ins {
        border: 1px solid #e6e6e6;
        border-radius: 12px;
        transition: all 0.3s ease;
        cursor: pointer;
        padding: 16px !important;
        margin-bottom: 12px !important;
      }
      .option-ins:hover {
        border-color: #d1d1d1;
        background-color: #f9f9f9;
        transform: translateY(-2px);
      }
      .option-ins.selected {
        border-color: #FF3366;
        background-color: #FFF5F7;
      }
      .progress-bar-ins {
        transition: width 0.5s cubic-bezier(0.4, 0, 0.2, 1);
      }
    }

    /* 刮刮乐核心样式 - 重点优化兼容性 */
    #scratch-container, #cp-scratch-container {
      position: relative;
      cursor: grab;
      width: 100%;
      height: 220px;
      border-radius: 16px;
      overflow: hidden;
      background: linear-gradient(45deg, #f5f5f5, #fafafa);
      border: 1px solid #eee;
      margin-bottom: 20px !important;
      -ms-touch-action: none;
          touch-action: none; /* 禁止所有默认触摸行为 */
    }
    #scratch-container:active, #cp-scratch-container:active {
      cursor: grabbing;
      transform: scale(0.98);
    }
    #scratch-canvas, #cp-scratch-canvas {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: block;
      z-index: 10;
      pointer-events: none; /* 让事件穿透到容器上 */
    }
    #scratch-result, #cp-scratch-result {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 20px;
      background: #fff;
      z-index: 1;
    }
    #result-description, #cp-result-description {
      font-size: 14px !important;
      line-height: 1.7 !important;
      color: #666 !important;
    }
    #cp-result-title {
      font-size: 18px !important;
      margin-bottom: 10px !important;
    }

    .spray-can {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 100%;
      height: 100%;
      border-radius: 50%;
      opacity: 0;
    }

    body {
      overflow-x: hidden;
      font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
      -webkit-tap-highlight-color: transparent; /* 移除点击高亮 */
    }
    h1 { font-size: 28px !important; }
    h2 { font-size: 20px !important; margin-bottom: 16px !important; }
    p { font-size: 15px !important; line-height: 1.6 !important; }

    #cp-product-recommendation { padding: 20px 16px !important; }
    .product-grid {
      display: flex !important;
      flex-direction: column !important;
      gap: 12px !important;
    }
    .product-card {
      width: 100% !important;
      display: flex !important;
      align-items: center !important;
      gap: 12px !important;
      background: #f9f9f9 !important;
      padding: 12px !important;
      border-radius: 12px !important;
    }
    .product-color { width: 24px !important; height: 24px !important; border-radius: 50% !important; }
    .product-info { flex: 1 !important; }
    .product-name { font-size: 14px !important; font-weight: 600 !important; color: #333 !important; }
    .product-desc { font-size: 12px !important; color: #999 !important; }

    .absolute.bottom-8 { bottom: 16px !important; font-size: 12px !important; }
  </style>
</head>
<body class="bg-gray-50 font-sans text-gray-800">
  <div id="app-container" class="relative w-full min-h-screen flex flex-col items-center justify-start">

    <!-- 开场页面 -->
    <div id="opening-page" class="absolute inset-0 z-50 flex flex-col items-center justify-center p-4 transition-opacity duration-1000">
      <div class="fixed inset-0 -z-20 bg-gradient-rainbow animate-rainbow-bg opacity-90"></div>
      <div class="fixed inset-0 -z-10 bg-black opacity-20"></div>
      <div class="text-center mb-8 opacity-0 animate-fade-in-up" style="animation-delay: 0.3s;">
        <h1 class="font-bold text-white mb-4 text-shadow-lg">色彩碰撞</h1>
        <p class="text-white font-medium">解锁你们的亲密CP色</p>
      </div>
      <div class="relative w-full max-w-md mx-auto mb-12 opacity-0 animate-fade-in-up" style="animation-delay: 0.6s;">
        <div class="card-ins">
          <p class="text-gray-600 text-sm leading-tight mb-8 text-center">
            欢迎踏入能量色彩秘境。一起来解锁你们的专属CP色吧~
          </p>
          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <button id="start-test-btn" class="btn-ins btn-ins-primary">开始测试</button>
            <button id="invite-partner-btn" class="btn-ins btn-ins-secondary">
              <i class="fa fa-share-alt mr-2"></i>邀请另一半
            </button>
          </div>
        </div>
      </div>
      <div class="absolute bottom-8 text-center text-white/80 text-sm opacity-0 animate-fade-in-up" style="animation-delay: 0.9s;">
        <p>DUREX × THE COLOR RUN 联合呈现</p>
      </div>
    </div>
    
    <!-- 题目页面 -->
    <div id="question-page" class="absolute inset-0 z-40 flex flex-col items-center justify-start bg-gray-50 p-4 opacity-0 pointer-events-none transition-opacity duration-500">
      <div class="w-full max-w-md mx-auto mt-8 mb-6">
        <div class="flex justify-between items-center">
          <div class="text-gray-600 font-medium">问题 <span id="current-question">1</span>/5</div>
          <div class="w-2/3 bg-gray-200 rounded-full h-2.5">
            <div id="progress-bar" class="bg-pink h-2.5 rounded-full progress-bar-ins" style="width: 20%"></div>
          </div>
        </div>
      </div>
      <div id="question-container" class="w-full max-w-md mx-auto mt-4 mb-20"></div>
      <div class="fixed bottom-8 left-1/2 transform -translate-x-1/2 w-full max-w-md px-4 flex justify-between">
        <button id="prev-btn" class="hidden bg-gray-200 hover:bg-gray-300 text-gray-700 font-medium py-2.5 px-6 rounded-full transition-all duration-300 focus:outline-none">
          <i class="fa fa-arrow-left mr-2"></i>上一题
        </button>
        <button id="next-btn" class="btn-ins btn-ins-primary">
          下一题 <i class="fa fa-arrow-right ml-2"></i>
        </button>
      </div>
    </div>
    
    <!-- 个人结果页面 -->
    <div id="personal-result-page" class="absolute inset-0 z-30 flex flex-col items-center justify-start bg-gray-50 p-4 opacity-0 pointer-events-none transition-opacity duration-500">
      <div id="personal-spray-bg" class="fixed inset-0 z-0 pointer-events-none">
        <div id="personal-spray-can" class="spray-can"></div>
      </div>
      <div id="result-content" class="relative z-10 w-full max-w-md mx-auto mt-12 mb-12 opacity-0">
        <div class="card-ins overflow-hidden mb-8">
          <div class="text-center mb-6">
            <h2 class="font-bold text-gray-800 mb-2">你的专属色彩人格</h2>
            <p class="text-gray-500">刮开涂层，解锁你的色彩秘密</p>
          </div>
          <div id="scratch-container">
            <div id="scratch-result">
              <h3 id="result-title" class="text-xl font-bold mb-3 text-pink"></h3>
              <p id="result-description" class="text-gray-600 text-sm leading-relaxed"></p>
            </div>
            <canvas id="scratch-canvas"></canvas>
          </div>
          <div id="product-recommendation" class="mt-8 bg-gradient-to-r from-pink-50 to-purple-50 rounded-xl p-4">
            <h3 class="text-xl font-bold text-gray-800 mb-3">为你推荐</h3>
            <div class="flex items-center mb-4">
              <div id="product-color" class="w-10 h-10 rounded-full mr-4"></div>
              <div>
                <p id="product-name" class="font-medium"></p>
                <p class="text-sm text-gray-500">为你的Play加一分可食用甜趣</p>
              </div>
            </div>
            <button id="buy-product-btn" class="w-full btn-ins btn-ins-primary">立即抢购</button>
          </div>
        </div>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <button id="share-result-btn" class="btn-ins btn-ins-secondary">
            <i class="fa fa-share-alt mr-2"></i>分享给另一半
          </button>
          <button id="wait-partner-btn" class="btn-ins btn-ins-primary">
            等待另一半完成 <span id="partner-status" class="ml-2">...</span>
          </button>
        </div>
      </div>
      <div class="absolute bottom-8 text-center text-gray-500 text-sm">
        <p>每个人都是独特的色彩，等待与伴侣碰撞出新的可能</p>
      </div>
    </div>
    
    <!-- CP结果页面 -->
    <div id="cp-result-page" class="absolute inset-0 z-20 flex flex-col items-center justify-start bg-gray-50 p-4 opacity-0 pointer-events-none transition-opacity duration-500">
      <div id="cp-spray-bg" class="fixed inset-0 z-0 pointer-events-none">
        <div id="cp-spray-can-1" class="spray-can"></div>
        <div id="cp-spray-can-2" class="spray-can"></div>
      </div>
      <div id="cp-result-content" class="relative z-10 w-full max-w-md mx-auto mt-12 mb-12 opacity-0">
        <div class="card-ins overflow-hidden mb-8">
          <div class="text-center mb-6">
            <h2 class="font-bold text-gray-800 mb-2">你们的CP色彩组合</h2>
            <p class="text-gray-500">色彩碰撞，创造独一无二的亲密关系</p>
          </div>
          
          <div id="cp-scratch-container">
            <div id="cp-scratch-result">
              <h3 id="cp-result-title" class="text-xl font-bold mb-3 text-pink"></h3>
              <p id="cp-result-description" class="text-gray-600 text-sm leading-relaxed"></p>
            </div>
            <canvas id="cp-scratch-canvas"></canvas>
          </div>
          
          <div id="cp-product-recommendation" class="mt-8 bg-gradient-to-r from-pink-50 to-purple-50 rounded-xl">
            <h3 class="text-xl font-bold text-gray-800 mb-4 px-2">为你们的关系增添色彩</h3>
            <div class="product-grid mb-6 px-2">
              <div class="product-card">
                <div id="cp-product-color-1" class="product-color"></div>
                <div class="product-info">
                  <p id="cp-product-name-1" class="product-name"></p>
                  <p class="product-desc">你的专属选择</p>
                </div>
              </div>
              <div class="product-card">
                <div id="cp-product-color-2" class="product-color"></div>
                <div class="product-info">
                  <p id="cp-product-name-2" class="product-name"></p>
                  <p class="product-desc">伴侣的专属选择</p>
                </div>
              </div>
            </div>
            <div class="flex flex-col sm:flex-row gap-4 px-2 pb-2">
              <button id="buy-cp-single-btn" class="flex-1 btn-ins btn-ins-primary">购买单品</button>
              <button id="buy-cp-set-btn" class="flex-1 btn-ins btn-ins-secondary">
                购买套装 <i class="fa fa-gift ml-1"></i>
              </button>
            </div>
          </div>
        </div>
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <button id="share-cp-result-btn" class="btn-ins btn-ins-secondary">
            <i class="fa fa-share-alt mr-2"></i>分享到朋友圈
          </button>
          <button id="restart-test-btn" class="btn-ins bg-gray-200 text-gray-700">重新测试</button>
        </div>
      </div>
      <div class="absolute bottom-8 text-center">
        <a href="#" class="inline-block bg-pink-100 text-pink-700 text-xs font-semibold px-4 py-2 rounded-full shadow-sm">
          #好色敢食 #ColorPlayCP
        </a>
      </div>
    </div>
  </div>

  <script>
    // 色彩数据
    const colorData = {
      pink: {
        name: '浪漫粉',
        hex: '#FF3366',
        slogan: '你的专属色：浪漫粉光！',
        description: '你是温柔梦想家！在亲密关系中，你偏好梦幻氛围与情感真挚，善于用温柔幻想点缀日常，让互动充满诗意与深度连接。你追求心灵交织的浪漫，像粉色雾气般柔软缠绵，总能带来安全感官的甜蜜惊喜。',
        product: { name: 'Durex Color Play 莓语甜酿风味' }
      },
      orange: {
        name: '活力橙',
        hex: '#FF9933',
        slogan: '你的专属色：活力橙光！',
        description: '你是不折不扣的冒险玩家！讨厌一成不变，善于将平凡日常变成刺激游戏。在亲密关系中，你追求新鲜感与即兴乐趣，是永远能带来惊喜的活力源泉。你像橙色爆发般注入肾上腺素，强调敢玩的感官碰撞与安全探索。',
        product: { name: 'Durex Color Play 橙光炽燃风味' }
      },
      green: {
        name: '自然绿',
        hex: '#33CC66',
        slogan: '你的专属色：自然绿光！',
        description: '你是和谐平衡者！在亲密关系中，你偏好自然流动与放松共处，强调纯净与环保般的平衡感。你善于营造宁静氛围，让互动如绿野般自在舒适，总能带来感官的自然治愈与安全依偎的温暖。',
        product: { name: 'Durex Color Play 青提沁玉风味' }
      },
      blue: {
        name: '自由蓝',
        hex: '#3399FF',
        slogan: '你的专属色：自由蓝光！',
        description: '你是细腻策略家！在亲密关系中，你注重规划与安全守护，偏好细腻依偎与心灵融合。你像蓝色海洋般包容深邃，总能提供温柔的支持，让互动充满策略性的感官探索与可靠的甜蜜保障。',
        product: { name: 'Durex Color Play 蓝莓幻梦风味' }
      },
      purple: {
        name: '神秘紫',
        hex: '#9966CC',
        slogan: '你的专属色：神秘紫光！',
        description: '你是独特探索者！在亲密关系中，你喜爱非凡发现与感官诗意，善于用神秘元素点缀生活，让互动充满独特惊喜与艺术表达。你像紫色迷雾般引人入胜，总能带来创新的感官冒险与安全的深度连接。',
        product: { name: 'Durex Color Play 葡绒紫韵风味' }
      }
    };

    // CP组合数据
    const cpCombinationData = {
      'pink-orange': { title: '粉橙火花：梦幻冒险之旅 交织！', description: '粉的温柔梦想遇上橙的冒险惊喜，碰撞出浪漫与新鲜的完美平衡。在亲密中，你们是幻想与游戏的搭档，将夜晚变成甜蜜探索，却总有情感守护。像Color Run色彩狂欢，融合感官甜趣与安全敢玩。' },
      'pink-green': { title: '粉绿火花：梦幻和谐之旅 交织！', description: '粉的温柔梦想遇上绿的和谐平衡，碰撞出浪漫与自然的纯净连接。在亲密中，你们是幻想与放松的搭档，将互动变成治愈绿洲，却总有情感深度。像Color Run色彩狂欢，融合感官甜趣与安全敢玩。' },
      'pink-blue': { title: '粉蓝火花：梦幻守护之旅 交织！', description: '粉的温柔梦想遇上蓝的细腻守护，碰撞出浪漫与安全的深邃包容。在亲密中，你们是幻想与规划的搭档，将时刻变成温柔融合，却总有可靠支持。像Color Run色彩狂欢，融合感官甜趣与安全敢玩。' },
      'pink-purple': { title: '粉紫火花：梦幻探索之旅 交织！', description: '粉的温柔梦想遇上紫的独特探索，碰撞出浪漫与神秘的诗意发现。在亲密中，你们是幻想与创新的搭档，将日常变成艺术冒险，却总有情感连接。像Color Run色彩狂欢，融合感官甜趣与安全敢玩。' },
      'orange-green': { title: '橙绿火花：冒险和谐之旅 交织！', description: '橙的冒险惊喜遇上绿的和谐平衡，碰撞出新鲜与自然的放松游戏。在亲密中，你们是活力与治愈的搭档，将夜晚变成平衡探索，却总有纯净守护。像Color Run色彩狂欢，融合感官甜趣与安全敢玩。' },
      'orange-blue': { title: '橙蓝火花：冒险守护之旅 交织！', description: '橙的冒险惊喜遇上蓝的细腻守护，碰撞出新鲜与安全的策略融合。在亲密中，你们是活力与规划的搭档，将互动变成可靠游戏，却总有温柔支持。像Color Run色彩狂欢，融合感官甜趣与安全敢玩。' },
      'orange-purple': { title: '橙紫火花：冒险探索之旅 交织！', description: '橙的冒险惊喜遇上紫的独特探索，碰撞出新鲜与神秘的创新冒险。在亲密中，你们是活力与艺术的搭档，将时刻变成诗意游戏，却总有独特发现。像Color Run色彩狂欢，融合感官甜趣与安全敢玩。' },
      'green-blue': { title: '绿蓝火花：和谐守护之旅 交织！', description: '绿的和谐平衡遇上蓝的细腻守护，碰撞出自然与安全的纯净包容。在亲密中，你们是放松与规划的搭档，将互动变成治愈融合，却总有可靠温暖。像Color Run色彩狂欢，融合感官甜趣与安全敢玩。' },
      'green-purple': { title: '绿紫火花：和谐探索之旅 交织！', description: '绿的和谐平衡遇上紫的独特探索，碰撞出自然与神秘的纯净发现。在亲密中，你们是放松与创新的搭档，将夜晚变成艺术绿洲，却总有平衡诗意。像Color Run色彩狂欢，融合感官甜趣与安全敢玩。' },
      'blue-purple': { title: '蓝紫火花：守护探索之旅 交织！', description: '蓝的细腻守护遇上紫的独特探索，碰撞出安全与神秘的策略发现。在亲密中，你们是规划与艺术的搭档，将时刻变成可靠冒险，却总有深度连接。像Color Run色彩狂欢，融合感官甜趣与安全敢玩。' },
      'same-pink': { title: '双倍浪漫粉：梦幻加倍！', description: '两个浪漫粉的相遇，创造出极致梦幻的亲密关系。你们都是温柔梦想家，擅长用浪漫点缀生活。完美匹配：双倍浪漫粉光加成，增强你们的梦幻温柔与情感浓度。' },
      'same-orange': { title: '双倍活力橙：冒险升级！', description: '两个活力橙的碰撞，创造出无尽的冒险与惊喜。你们都是冒险玩家，将亲密关系变成一场永不停歇的刺激游戏。完美匹配：双倍活力橙光加成，增强你们的冒险惊喜与即兴火花！' },
      'same-green': { title: '双倍自然绿：和谐共鸣！', description: '两个自然绿的相遇，创造出完美的和谐与平衡。你们都是和谐平衡者，让亲密关系如自然流动般自在舒适。完美匹配：双倍自然绿光加成，增强你们的和谐平衡与纯净治愈！' },
      'same-blue': { title: '双倍自由蓝：深度守护！', description: '两个自由蓝的相遇，创造出最细腻的守护与连接。你们都是细腻策略家，让亲密关系充满安全感与深度理解。完美匹配：双倍自由蓝光加成，增强你们的细腻守护与安全依偎！' },
      'same-purple': { title: '双倍神秘紫：独特探索！', description: '两个神秘紫的碰撞，创造出充满独特与创新的亲密关系。你们都是独特探索者，将日常变成一场艺术冒险。完美匹配：双倍神秘紫光加成，增强你们的独特探索与感官诗意！' }
    };

    // 题目数据
    const questions = [
      {
        question: '你们在秘境中遇到一条发光的彩河，对岸传来甜蜜的召唤声，你们会怎么跨越？',
        options: [
          { text: '一起抓起粗壮藤蔓，兴奋地荡过去，享受肾上腺素的冲撞！', color: 'orange' },
          { text: '手拉手观察水流，找最安全的浅滩，温柔地一步步渡过。', color: 'blue' },
          { text: '先被河边闪烁的奇异花吸引，两人好奇地摘取，幻想着它能带来神秘惊喜。', color: 'purple' }
        ]
      },
      {
        question: '穿过河流，一片魔法森林出现，三扇彩门闪烁，你们会选择哪扇一起进入？',
        options: [
          { text: '粉色梦幻门，里面传来温柔的星辰低语，两人互相脑洞大开，沉浸浪漫幻想。', color: 'pink' },
          { text: '绿色自然门，通往宁静的绿野，两人选择放松依偎，感受和谐的自然流动。', color: 'green' },
          { text: '蓝色水晶门，透明可见平静花园，两人安静守护彼此，规划内心的温柔空间。', color: 'blue' }
        ]
      },
      {
        question: '在门后，一位色彩精灵求助，需要你们为它创造一件亲密礼物，你们会选？',
        options: [
          { text: '调配一款瞬间点燃快乐的魔法香水，两人分工，喷洒出甜蜜的惊喜泡沫。', color: 'orange' },
          { text: '谱写一首让星辰动容的浪漫夜曲，你们互相启发，哼唱出温柔的旋律。', color: 'pink' },
          { text: '设计一个隐形自然结界，两人心有灵犀地筑起平衡和谐的私密绿洲', color: 'green' }
        ]
      },
      {
        question: '探索途中，你们发现一个闪烁的色彩泉，你们会如何互动？',
        options: [
          { text: '两人好奇地触摸泉水，探索它带来的神秘变化与独特惊喜。', color: 'purple' },
          { text: '一起规划如何安全汲取泉水，温柔守护彼此，享受细腻的平衡流动。', color: 'blue' },
          { text: '兴奋地喷洒泉水玩耍，制造即兴的色彩碰撞与冒险乐趣。', color: 'orange' }
        ]
      },
      {
        question: '离开秘境前，你们回头，最想记住的色彩画面是？',
        options: [
          { text: '所有颜色如绿野般自然蔓延，壮丽和谐，两人放松拥抱那份平衡余韵。', color: 'green' },
          { text: '两棵发光古树枝叶温柔交织，像你们的关系般梦幻缠绵。', color: 'pink' },
          { text: '你们的脚印生长出奇异发光花朵，象征独特而神秘的回忆。', color: 'purple' }
        ]
      }
    ];

    // 全局变量
    let currentQuestionIndex = 0;
    let userAnswers = [];
    let userResult = null;
    let partnerResult = null;
    let isWaitingForPartner = false;
    
    // DOM元素
    const openingPage = document.getElementById('opening-page');
    const questionPage = document.getElementById('question-page');
    const personalResultPage = document.getElementById('personal-result-page');
    const cpResultPage = document.getElementById('cp-result-page');
    const questionContainer = document.getElementById('question-container');
    const progressBar = document.getElementById('progress-bar');
    const currentQuestionEl = document.getElementById('current-question');
    const resultContent = document.getElementById('result-content');
    const scratchContainer = document.getElementById('scratch-container');
    const scratchCanvas = document.getElementById('scratch-canvas');
    const scratchResult = document.getElementById('scratch-result');
    const resultTitle = document.getElementById('result-title');
    const resultDescription = document.getElementById('result-description');
    const productColor = document.getElementById('product-color');
    const productName = document.getElementById('product-name');
    const partnerStatus = document.getElementById('partner-status');
    const cpResultContent = document.getElementById('cp-result-content');
    const cpScratchContainer = document.getElementById('cp-scratch-container');
    const cpScratchCanvas = document.getElementById('cp-scratch-canvas');
    const cpScratchResult = document.getElementById('cp-scratch-result');
    const cpResultTitle = document.getElementById('cp-result-title');
    const cpResultDescription = document.getElementById('cp-result-description');
    const cpProductColor1 = document.getElementById('cp-product-color-1');
    const cpProductColor2 = document.getElementById('cp-product-color-2');
    const cpProductName1 = document.getElementById('cp-product-name-1');
    const cpProductName2 = document.getElementById('cp-product-name-2');
    const personalSprayCan = document.getElementById('personal-spray-can');
    const cpSprayCan1 = document.getElementById('cp-spray-can-1');
    const cpSprayCan2 = document.getElementById('cp-spray-can-2');
    
    // 按钮元素
    const startTestBtn = document.getElementById('start-test-btn');
    const invitePartnerBtn = document.getElementById('invite-partner-btn');
    const nextBtn = document.getElementById('next-btn');
    const prevBtn = document.getElementById('prev-btn');
    const shareResultBtn = document.getElementById('share-result-btn');
    const waitPartnerBtn = document.getElementById('wait-partner-btn');
    const shareCpResultBtn = document.getElementById('share-cp-result-btn');
    const restartTestBtn = document.getElementById('restart-test-btn');
    const buyProductBtn = document.getElementById('buy-product-btn');
    const buyCpSingleBtn = document.getElementById('buy-cp-single-btn');
    const buyCpSetBtn = document.getElementById('buy-cp-set-btn');
    
    // --- 刮刮乐核心逻辑 - 重点优化百度浏览器兼容性 ---
    function initScratchCard(canvasEl, containerEl) {
      const canvas = canvasEl;
      const ctx = canvas.getContext('2d');
      let isScratching = false;
      let lastX = 0;
      let lastY = 0;
      const dpr = window.devicePixelRatio || 1;

      function resizeAndDraw() {
        // 使用 offsetWidth 和 offsetHeight 以获得更准确的元素尺寸
        const width = containerEl.offsetWidth;
        const height = containerEl.offsetHeight;
        
        if (width === 0 || height === 0) {
            // 如果尺寸为0，延迟后重试，防止元素尚未渲染
            setTimeout(resizeAndDraw, 100);
            return;
        }
        
        canvas.width = width * dpr;
        canvas.height = height * dpr;
        canvas.style.width = `${width}px`;
        canvas.style.height = `${height}px`;
        
        ctx.scale(dpr, dpr);
        ctx.fillStyle = '#E0E0E0';
        ctx.fillRect(0, 0, width, height);
        
        ctx.fillStyle = '#D0D0D0';
        for (let i = 0; i < 300; i++) {
          const x = Math.random() * width;
          const y = Math.random() * height;
          const size = Math.random() * 1.5;
          ctx.beginPath();
          ctx.arc(x, y, size, 0, Math.PI * 2);
          ctx.fill();
        }
        
        ctx.strokeStyle = '#DDDDDD';
        ctx.lineWidth = 0.5;
        const gridSize = 20;
        for (let x = 0; x <= width; x += gridSize) {
          ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, height); ctx.stroke();
        }
        for (let y = 0; y <= height; y += gridSize) {
          ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(width, y); ctx.stroke();
        }
      }
      
      // 确保DOM完全渲染后再绘制
      if (document.readyState === "complete" || document.readyState === "interactive") {
        resizeAndDraw();
      } else {
        document.addEventListener("DOMContentLoaded", resizeAndDraw);
      }
      // 延迟再次绘制，应对百度浏览器可能的布局延迟
      setTimeout(resizeAndDraw, 500);

      function startScratch(e) {
        e.preventDefault(); // 关键：阻止浏览器默认行为
        document.body.style.overflow = 'hidden';
        const pos = getEventPosition(e, canvas, containerEl);
        lastX = pos.x;
        lastY = pos.y;
        isScratching = true;
        // 立即绘制一个点，确保刮擦开始时就能看到效果
        ctx.globalCompositeOperation = 'destination-out';
        ctx.beginPath();
        ctx.arc(lastX, lastY, 15, 0, Math.PI * 2);
        ctx.fill();
      }
      
      function endScratch() {
        isScratching = false;
        document.body.style.overflow = '';
      }
      
      function scratch(e) {
        if (!isScratching) return;
        e.preventDefault(); // 关键：在移动过程中持续阻止默认行为
        
        const pos = getEventPosition(e, canvas, containerEl);
        const currentX = pos.x;
        const currentY = pos.y;
        
        ctx.globalCompositeOperation = 'destination-out';
        ctx.lineWidth = 35;
        ctx.lineCap = 'round';
        ctx.lineJoin = 'round';
        
        ctx.beginPath();
        ctx.moveTo(lastX, lastY);
        ctx.lineTo(currentX, currentY);
        ctx.stroke();
        
        lastX = currentX;
        lastY = currentY;
        
        // 降低检查频率，提高性能
        if (Math.random() > 0.7) {
            checkScratchProgress();
        }
      }
      
      // 优化坐标计算，确保在各种情况下都准确
      function getEventPosition(e, canvas, container) {
        const rect = container.getBoundingClientRect(); // 使用容器的rect而非canvas
        let x, y;
        
        if (e.type.startsWith('touch')) {
          const touch = e.touches[0] || e.changedTouches[0];
          x = touch.clientX - rect.left;
          y = touch.clientY - rect.top;
        } else if (e.type.startsWith('pointer')) {
          x = e.clientX - rect.left;
          y = e.clientY - rect.top;
        } else {
          x = e.clientX - rect.left;
          y = e.clientY - rect.top;
        }
        
        // 坐标转换
        const scaleX = canvas.width / container.offsetWidth;
        const scaleY = canvas.height / container.offsetHeight;
        
        return { x: x * scaleX, y: y * scaleY };
      }
      
      function checkScratchProgress() {
        const width = canvas.width;
        const height = canvas.height;
        const imageData = ctx.getImageData(0, 0, width, height);
        const pixels = imageData.data;
        const totalPixels = width * height;
        let transparentPixels = 0;
        
        // 每隔8个像素检查一次，进一步提高性能
        for (let i = 0; i < pixels.length; i += 4 * 8) {
          if (pixels[i + 3] === 0) {
            transparentPixels++;
          }
        }
        
        const actualTransparentRatio = transparentPixels / (totalPixels / 8);
        
        if (actualTransparentRatio > 0.5) { // 降低阈值，更容易触发自动清除
          ctx.globalCompositeOperation = 'destination-out';
          ctx.fillRect(0, 0, width / dpr, height / dpr);
          isScratching = false;
          document.body.style.overflow = '';
        }
      }
      
      // 事件监听优化
      // 主要监听容器的事件，而非canvas
      if ('PointerEvent' in window) {
        // 优先使用 Pointer Events
        containerEl.addEventListener('pointerdown', startScratch, { passive: false });
        containerEl.addEventListener('pointermove', scratch, { passive: false });
        containerEl.addEventListener('pointerup', endScratch);
        containerEl.addEventListener('pointercancel', endScratch);
        containerEl.addEventListener('pointerleave', endScratch);
      } else {
        // 降级使用 Touch 和 Mouse Events
        containerEl.addEventListener('touchstart', startScratch, { passive: false });
        containerEl.addEventListener('touchmove', scratch, { passive: false });
        containerEl.addEventListener('touchend', endScratch);
        containerEl.addEventListener('touchcancel', endScratch);
        
        containerEl.addEventListener('mousedown', startScratch);
        containerEl.addEventListener('mousemove', scratch);
        containerEl.addEventListener('mouseup', endScratch);
        containerEl.addEventListener('mouseleave', endScratch);
      }
      
      window.addEventListener('resize', () => {
        // 窗口大小变化时，重置刮刮乐状态
        isScratching = false;
        setTimeout(resizeAndDraw, 300);
      });
      window.addEventListener('orientationchange', () => {
        isScratching = false;
        setTimeout(resizeAndDraw, 300);
      });
    }

    // 重置刮刮乐
    function resetScratchCard(canvasId) {
      const canvas = document.getElementById(canvasId);
      if (!canvas) return;
      const container = canvas.parentElement;
      const ctx = canvas.getContext('2d');
      
      const width = container.offsetWidth;
      const height = container.offsetHeight;
      const dpr = window.devicePixelRatio || 1;
      
      ctx.save();
      ctx.setTransform(1, 0, 0, 1, 0, 0);
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      ctx.restore();

      ctx.scale(dpr, dpr);
      ctx.fillStyle = '#E0E0E0';
      ctx.fillRect(0, 0, width, height);
      
      ctx.fillStyle = '#D0D0D0';
      for (let i = 0; i < 300; i++) {
        const x = Math.random() * width;
        const y = Math.random() * height;
        const size = Math.random() * 1.5;
        ctx.beginPath();
        ctx.arc(x, y, size, 0, Math.PI * 2);
        ctx.fill();
      }
      
      ctx.strokeStyle = '#DDDDDD';
      ctx.lineWidth = 0.5;
      const gridSize = 20;
      for (let x = 0; x <= width; x += gridSize) {
        ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, height); ctx.stroke();
      }
      for (let y = 0; y <= height; y += gridSize) {
        ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(width, y); ctx.stroke();
      }
    }
    
    // 显示当前题目
    function showCurrentQuestion() {
      const question = questions[currentQuestionIndex];
      currentQuestionEl.textContent = currentQuestionIndex + 1;
      progressBar.style.width = `${(currentQuestionIndex + 1) * 20}%`;
      
      prevBtn.classList.toggle('hidden', currentQuestionIndex <= 0);
      
      nextBtn.innerHTML = currentQuestionIndex === questions.length - 1 
        ? '查看结果 <i class="fa fa-arrow-right ml-2"></i>' 
        : '下一题 <i class="fa fa-arrow-right ml-2"></i>';
      
      let optionsHtml = '';
      question.options.forEach((option, index) => {
        const colorInfo = colorData[option.color];
        const isSelected = userAnswers[currentQuestionIndex] === index;
        
        optionsHtml += `
          <div class="option-ins ${isSelected ? 'selected' : ''}" data-index="${index}">
            <div class="flex items-start">
              <div class="flex-shrink-0 w-8 h-8 rounded-full mr-4 flex items-center justify-center text-white text-xs font-bold" style="background-color: ${colorInfo.hex}">
                ${String.fromCharCode(65 + index)}
              </div>
              <div class="flex-grow">
                <p class="text-gray-700 text-sm leading-relaxed">${option.text}</p>
              </div>
            </div>
          </div>
        `;
      });
      
      questionContainer.innerHTML = `
        <div class="card-ins overflow-hidden opacity-0 animate-fade-in-up" style="animation-delay: 0.3s;">
          <h2 class="font-bold text-gray-800 mb-6">${question.question}</h2>
          <div class="space-y-3">
            ${optionsHtml}
          </div>
        </div>
      `;
      
      document.querySelectorAll('.option-ins').forEach(option => {
        option.addEventListener('click', () => {
          const index = parseInt(option.dataset.index);
          userAnswers[currentQuestionIndex] = index;
          
          document.querySelectorAll('.option-ins').forEach(opt => opt.classList.remove('selected'));
          option.classList.add('selected');
        });
      });
    }
    
    // 计算结果
    function calculateResult() {
      const score = { orange: 0, blue: 0, purple: 0, pink: 0, green: 0 };
      
      userAnswers.forEach((answer, questionIndex) => {
        const question = questions[questionIndex];
        const color = question.options[answer].color;
        score[color]++;
      });
      
      let max = Math.max(...Object.values(score));
      let winners = Object.keys(score).filter(key => score[key] === max);
      
      const priority = ['orange', 'blue', 'purple', 'pink', 'green'];
      
      if (Object.values(score).every(v => v === 1)) {
        return priority[Math.floor(Math.random() * priority.length)];
      }
      
      return winners.sort((a, b) => priority.indexOf(a) - priority.indexOf(b))[0];
    }
    
    // 显示个人结果
    function showPersonalResult() {
      userResult = calculateResult();
      const resultInfo = colorData[userResult];
      
      personalSprayCan.style.background = `radial-gradient(circle, ${resultInfo.hex}80 0%, ${resultInfo.hex}00 70%)`;
      personalSprayCan.classList.add('animate-spray-in');
      
      resultTitle.textContent = resultInfo.slogan;
      resultDescription.textContent = resultInfo.description;
      
      productColor.style.backgroundColor = resultInfo.hex;
      productName.textContent = resultInfo.product.name;

      resetScratchCard('scratch-canvas');
      
      setTimeout(() => {
        resultContent.style.opacity = '1';
        resultContent.classList.add('animate-fade-in-up');
      }, 1000);
    }
    
    // 显示CP结果
    function showCPResult() {
      const userColorInfo = colorData[userResult];
      
      cpSprayCan1.style.background = `radial-gradient(circle, ${userColorInfo.hex}80 0%, ${userColorInfo.hex}00 70%)`;
      cpSprayCan1.classList.add('animate-spray-in');
      cpSprayCan1.style.animationDelay = '0s';

      cpSprayCan2.style.background = `radial-gradient(circle, ${partnerResult.hex}80 0%, ${partnerResult.hex}00 70%)`;
      cpSprayCan2.classList.add('animate-spray-in');
      cpSprayCan2.style.animationDelay = '0.3s';
      
      cpProductColor1.style.backgroundColor = userColorInfo.hex;
      cpProductName1.textContent = userColorInfo.product.name;
      cpProductColor2.style.backgroundColor = partnerResult.hex;
      cpProductName2.textContent = partnerResult.product.name;
      
      let combinationKey;
      if (userResult === partnerResult.key) {
        combinationKey = `same-${userResult}`;
      } else {
        combinationKey = [userResult, partnerResult.key].sort().join('-');
      }
      const combinationInfo = cpCombinationData[combinationKey];
      
      cpResultTitle.textContent = combinationInfo.title;
      cpResultDescription.textContent = combinationInfo.description;

      resetScratchCard('cp-scratch-canvas');
      
      setTimeout(() => {
        cpResultContent.style.opacity = '1';
        cpResultContent.classList.add('animate-fade-in-up');
      }, 1200);
    }
    
    // 模拟等待伴侣
    function simulateWaitingForPartner() {
      isWaitingForPartner = true;
      let dots = 0;
      
      const statusInterval = setInterval(() => {
        dots = (dots + 1) % 4;
        partnerStatus.textContent = '.'.repeat(dots);
        
        if (Math.random() > 0.97) {
          clearInterval(statusInterval);
          isWaitingForPartner = false;
          
          const otherColors = Object.keys(colorData).filter(color => color !== userResult);
          const randomColorKey = otherColors[Math.floor(Math.random() * otherColors.length)];
          partnerResult = {...colorData[randomColorKey], key: randomColorKey};

          personalResultPage.style.opacity = '0';
          personalResultPage.style.pointerEvents = 'none';
          cpResultPage.style.opacity = '1';
          cpResultPage.style.pointerEvents = 'auto';
          
          showCPResult();
        }
      }, 500);
    }
    
    // 页面切换
    function goToPage(pageId) {
      [openingPage, questionPage, personalResultPage, cpResultPage].forEach(page => {
        page.style.opacity = '0';
        page.style.pointerEvents = 'none';
      });

      resultContent.style.opacity = '0';
      resultContent.classList.remove('animate-fade-in-up');
      cpResultContent.style.opacity = '0';
      cpResultContent.classList.remove('animate-fade-in-up');
      [personalSprayCan, cpSprayCan1, cpSprayCan2].forEach(can => {
        can.classList.remove('animate-spray-in');
        can.style.animationDelay = '';
      });

      const targetPage = document.getElementById(pageId);
      targetPage.style.opacity = '1';
      targetPage.style.pointerEvents = 'auto';
      
      if (pageId === 'question-page') {
        currentQuestionIndex = 0;
        userAnswers = new Array(questions.length).fill(null);
        showCurrentQuestion();
      } else if (pageId === 'personal-result-page') {
        showPersonalResult();
      }
    }
    
    // 事件监听
    document.addEventListener('DOMContentLoaded', () => {
      // 初始化刮刮乐
      initScratchCard(scratchCanvas, scratchContainer);
      initScratchCard(cpScratchCanvas, cpScratchContainer);

      startTestBtn.addEventListener('click', () => {
        goToPage('question-page');
      });
      
      invitePartnerBtn.addEventListener('click', () => {
        if (navigator.share) {
          navigator.share({
            title: '快来和我一起测试我们的亲密CP色！',
            text: '我正在参加Color Play色彩碰撞测试，快来一起解锁我们的亲密CP色吧！',
            url: window.location.href
          });
        } else {
          alert('请将链接分享给你的伴侣');
        }
      });
      
      nextBtn.addEventListener('click', () => {
        if (userAnswers[currentQuestionIndex] === null) {
          alert('请选择一个选项后再继续');
          return;
        }
        
        if (currentQuestionIndex === questions.length - 1) {
          goToPage('personal-result-page');
        } else {
          currentQuestionIndex++;
          showCurrentQuestion();
        }
      });
      
      prevBtn.addEventListener('click', () => {
        if (currentQuestionIndex > 0) {
          currentQuestionIndex--;
          showCurrentQuestion();
        }
      });
      
      shareResultBtn.addEventListener('click', () => {
        if (navigator.share) {
          navigator.share({
            title: '我的色彩人格是' + colorData[userResult].name + '，快来和我配对！',
            text: `我刚刚完成了Color Play色彩碰撞测试，我的色彩人格是${colorData[userResult].name}，快来一起解锁我们的亲密CP色吧！`,
            url: window.location.href
          });
        } else {
          alert('请将你的结果分享给伴侣，邀请TA一起测试');
        }
      });
      
      waitPartnerBtn.addEventListener('click', () => {
        if (!isWaitingForPartner) {
          simulateWaitingForPartner();
        }
      });
      
      shareCpResultBtn.addEventListener('click', () => {
        if (navigator.share) {
          navigator.share({
            title: '我们的CP色彩是' + cpResultTitle.textContent,
            text: `我和伴侣完成了Color Play色彩碰撞测试，我们的CP色彩是${cpResultTitle.textContent}，快来一起解锁你们的亲密CP色吧！`,
            url: window.location.href
          });
        } else {
          alert('分享到朋友圈，晒出你们的CP色吧！');
        }
      });
      
      restartTestBtn.addEventListener('click', () => {
        userAnswers = [];
        userResult = null;
        partnerResult = null;
        goToPage('opening-page');
      });
      
      [buyProductBtn, buyCpSingleBtn, buyCpSetBtn].forEach(btn => {
        btn.addEventListener('click', () => {
          window.location.href = 'https://www.durex.com';
        });
      });
    });
  </script>
</body>
</html>
