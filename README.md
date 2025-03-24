# XperiaWiki

## 欢迎来到 XperiaWiki

本站意在帮助索粉少走点 van♂路，且告慰在天国的 <del>机锋网</del>。

**1.** 本 Wiki 用爱发电，请勿盗取页面，qqqxx，，，

**2.** 本页面由个人付出了个人时间进行整理，记载的内容可能在三分钟之内死亡，注意备份。

**3.** 本 Wiki 的内容均来自于网络，仅供参考，如果因为本站教程而导致的变砖或者数据丢失等问题，本站概不负责，刷机不规范，变砖两行泪 —— <del>kenichioshima</del>

[了解更多](wiki.html)

## 超级巨星

介绍今年的年度 Xperia 旗舰机型。

[了解更多](superstar.html)

### 预览

加载预览中...

## 年度硬汉

介绍目前 Xperia 最热门的机型。

[了解更多](hardman.html)

### 预览

加载预览中...

## 高雅创作

Xperia 用机技巧的页面。

[了解更多](creation.html)

---

## 侧边栏/顶部导航

* [首页](#)
* [超级巨星](superstar.html)
* [年度硬汉](hardman.html)
* [高雅创作](creation.html)
* [Xperia 机型](目录.html)
* [刷机指南](#)

---

## 音频控制

<button id="toggleAudio" onclick="toggleAudio()"></button>

---

## JavaScript 代码

```javascript
const audio = document.getElementById('backgroundAudio');
const toggleBtn = document.getElementById('toggleAudio');

function toggleAudio() {
  if (audio.paused) {
    audio.play();
    toggleBtn.textContent = "";
  } else {
    audio.pause();
    toggleBtn.textContent = "";
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
