<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <title>XperiaWiki</title>
  <style>
    /* 颜色 & 变量 */
    :root {
      --bg-color: #f8f9fa;
      --text-color: #202122;
      --link-color: #0645ad;
      --hover-color: #0b0080;
      --border-color: #a2a9b1;
      --sidebar-bg: rgba(243, 243, 243, 0.8);
      --glass-bg: rgba(255, 255, 255, 0.2);
      --shadow-color: rgba(0, 0, 0, 0.1);
    }
    
    /* 暗黑模式 */
    @media (prefers-color-scheme: dark) {
      :root {
        --bg-color: #121212;
        --text-color: #e0e0e0;
        --link-color: #5fa3ff;
        --hover-color: #99c2ff;
        --border-color: #444;
        --sidebar-bg: rgba(40, 40, 40, 0.8);
        --glass-bg: rgba(255, 255, 255, 0.1);
        --shadow-color: rgba(255, 255, 255, 0.1);
      }
    }
    
    /* 全局样式 */
    body {
      font-family: 'Arial', sans-serif;
      margin: 0;
      padding: 0;
      background: var(--bg-color);
      color: var(--text-color);
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    
    /* 侧边栏 */
    .sidebar {
      width: 220px;
      background: var(--sidebar-bg);
      border-right: 1px solid var(--border-color);
      padding: 15px;
      height: 100vh;
      overflow-y: auto;
      position: fixed;
      left: 0;
      top: 0;
      transition: transform 0.3s ease-in-out;
      backdrop-filter: blur(10px);
      box-shadow: 0 4px 6px var(--shadow-color);
    }
    
    .sidebar h3 {
      font-size: 1.2em;
      margin-bottom: 10px;
    }
    
    .sidebar ul {
      list-style: none;
      padding: 0;
    }
    
    .sidebar ul li {
      margin: 8px 0;
    }
    
    .sidebar ul li a {
      text-decoration: none;
      color: var(--link-color);
      font-size: 0.95em;
    }
    
    .sidebar ul li a:hover {
      color: var(--hover-color);
    }
    
    /* 主要内容 */
    .content {
      margin-left: 240px;
      padding: 20px;
      max-width: 900px;
      width: 100%;
    }
    
    /* 标题 */
    .main-title {
      font-size: 2em;
      font-weight: bold;
      border-bottom: 2px solid var(--border-color);
      padding-bottom: 5px;
      margin-bottom: 15px;
    }
    
    /* 章节 */
    .section {
      background: var(--glass-bg);
      padding: 15px;
      border-radius: 10px;
      backdrop-filter: blur(10px);
      box-shadow: 0 4px 6px var(--shadow-color);
      margin-bottom: 20px;
    }
    
    .section h2 {
      font-size: 1.4em;
      border-bottom: 1px solid var(--border-color);
      padding-bottom: 5px;
    }
    
    /* 按钮 */
    .button {
      display: inline-block;
      padding: 8px 15px;
      background-color: var(--link-color);
      color: white;
      text-decoration: none;
      border-radius: 4px;
      font-weight: bold;
      margin-top: 10px;
    }
    
    .button:hover {
      background-color: var(--hover-color);
    }
    
    /* 图片预览区域 */
    .preview {
      margin-top: 10px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    
    .image-frame {
      width: 200px;
      height: 200px;
      overflow: hidden;
      position: relative;
      border: 1px solid var(--border-color);
      margin-bottom: 10px;
    }
    
    .image-frame img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
    
    /* 响应式布局 */
    @media (max-width: 768px) {
      .sidebar {
        width: 100%;
        height: auto;
        position: relative;
        border-right: none;
        border-bottom: 1px solid var(--border-color);
        padding: 10px;
        text-align: center;
      }
    
      .sidebar ul {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        padding: 0;
      }
    
      .sidebar ul li {
        margin: 5px 10px;
      }
    
      .content {
        margin-left: 0;
        padding: 15px;
        width: 100%;
      }
    
      .main-title {
        font-size: 1.8em;
        text-align: center;
      }
    }
    
    @media (max-width: 480px) {
      .main-title {
        font-size: 1.5em;
      }
    
      .section {
        padding: 10px;
      }
    
      .button {
        font-size: 0.9em;
        padding: 6px 12px;
      }
    }
    
    /* 小喇叭按钮 */
    #toggleAudio {
      position: fixed;
      right: 20px;
      bottom: 20px;
      background-color: var(--link-color);
      color: #fff;
      border: none;
      border-radius: 50%;
      width: 50px;
      height: 50px;
      font-size: 24px;
      cursor: pointer;
      box-shadow: 0 4px 6px var(--shadow-color);
      transition: background-color 0.3s;
      z-index: 1000;
    }
    
    #toggleAudio:hover {
      background-color: var(--hover-color);
    }
  </style>
</head>
<body>
  <!-- 自动播放音频 -->
  <audio id="backgroundAudio" src="./上海红茶馆.mp3" autoplay loop></audio>
  
  <!-- 侧边栏/顶部导航 -->
  <div class="sidebar">
    <h3>导航</h3>
    <ul>
      <li><a href="#">首页</a></li>
      <li><a href="#">超级巨星</a></li>
      <li><a href="#">年度硬汉</a></li>
      <li><a href="#">高雅创作</a></li>
      <li><a href="./目录.html">Xperia 机型</a></li>
      <li><a href="#">刷机指南</a></li>
    </ul>
  </div>
  
  <!-- 主要内容 -->
  <div class="content">
    <div class="main-title">XperiaWiki</div>
    
    <div class="section">
      <h2>欢迎来到 XperiaWiki</h2>
      <p>本站意在帮助索粉少走点 van♂路，且告慰在天国的 <del>机锋网</del>。</p>
      <p><strong>1.</strong> 本 Wiki 用爱发电，请勿盗取页面，qqqxx，，，</p>
      <p><strong>2.</strong> 本页面由个人付出了个人时间进行整理，记载的内容可能在三分钟之内死亡，注意备份。</p>
      <p><strong>3.</strong> 本 Wiki 的内容均来自于网络，仅供参考，如果因为本站教程而导致的变砖或者数据丢失等问题，本站概不负责，刷机不规范，变砖两行泪 —— <del>kenichioshima</del></p>
      <a href="wiki.html" class="button">了解更多</a>
    </div>
    
    <!-- 超级巨星板块 -->
    <div class="section">
      <h2>超级巨星</h2>
      <p>介绍今年的年度 Xperia 旗舰机型。</p>
      <a href="superstar.html" class="button">了解更多</a>
      <!-- 添加预览区域 -->
      <div class="preview" id="superstar-preview">
        <!-- 图片框与简介将由 JavaScript 动态填充 -->
        <p>加载预览中...</p>
      </div>
    </div>
    
    <!-- 年度硬汉板块 -->
    <div class="section">
      <h2>年度硬汉</h2>
      <p>介绍目前 Xperia 最热门的机型。</p>
      <a href="hardman.html" class="button">了解更多</a>
      <!-- 添加预览区域 -->
      <div class="preview" id="hardman-preview">
        <!-- 图片框与简介将由 JavaScript 动态填充 -->
        <p>加载预览中...</p>
      </div>
    </div>
    
    <div class="section">
      <h2>高雅创作</h2>
      <p>Xperia 用机技巧的页面。</p>
      <a href="creation.html" class="button">了解更多</a>
    </div>
  </div>
  
  <!-- 右下角喇叭按钮 -->
  <button id="toggleAudio" onclick="toggleAudio()">🔊</button>
  
  <script>
    const audio = document.getElementById('backgroundAudio');
    const toggleBtn = document.getElementById('toggleAudio');
    
    function toggleAudio() {
      if (audio.paused) {
        audio.play();
        toggleBtn.textContent = "🔊";
      } else {
        audio.pause();
        toggleBtn.textContent = "🔇";
      }
    }
    
    // 通用预览抓取函数：抓取指定页面的第一个 <img> 和 <p>
    function fetchPreview(pageUrl, containerId) {
      fetch(pageUrl)
        .then(response => response.text())
        .then(html => {
          const parser = new DOMParser();
          const doc = parser.parseFromString(html, 'text/html');
          // 获取第一个图片：如果页面中有 <img> 标签，则取 src，否则为空
          const imgElem = doc.querySelector('img');
          const imgSrc = imgElem ? imgElem.src : "";
          // 获取简介：取第一个 <p> 标签的文本内容
          const summaryElem = doc.querySelector('p');
          const summary = summaryElem ? summaryElem.innerText.trim() : "暂无简介";
          
          const container = document.getElementById(containerId);
          container.innerHTML = "";
          
          // 创建 1:1 图片框
          const imageDiv = document.createElement('div');
          imageDiv.className = "image-frame";
          if (imgSrc) {
            const image = document.createElement('img');
            image.src = imgSrc;
            image.alt = "机型图片";
            imageDiv.appendChild(image);
          } else {
            imageDiv.textContent = "无图片";
          }
          
          // 添加图片框和简介到预览区域
          container.appendChild(imageDiv);
          const summaryPara = document.createElement('p');
          summaryPara.textContent = summary;
          container.appendChild(summaryPara);
        })
        .catch(error => {
          console.error("预览加载错误:", error);
          const container = document.getElementById(containerId);
          container.innerHTML = "<p>预览加载失败</p>";
        });
    }
    
    // 抓取超级巨星和年度硬汉的预览
    fetchPreview("superstar.html", "superstar-preview");
    fetchPreview("hardman.html", "hardman-preview");
  </script>
</body>
</html>
