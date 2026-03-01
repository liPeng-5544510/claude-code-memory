# 科幻风格 (Sci-Fi) 幻灯片模板

> 来源文件: `html_slideshow_framework_scifi.html`
> 保存时间: 2026-03-01
> 适用场景: 科技演示、AI发布会、游戏展示、未来概念

---

## 一、色彩方案

### 主色调
```css
--bg-deep: #0A0A1A      /* 深空黑背景 */
--bg-primary: #0F172A   /* 主背景色 */
--bg-card: rgba(30, 41, 59, 0.6)     /* 卡片半透明背景 */
```

### 霓虹色系
```css
--neon-blue: #00E5FF    /* 霓虹蓝 - 主强调色 */
--neon-purple: #A855F7  /* 霓虹紫 */
--neon-pink: #EC4899    /* 霓虹粉 */
--neon-green: #10B981    /* 霓虹绿 */
--neon-orange: #F59E0B   /* 霓虹橙 */
--neon-gold: #FBBF24     /* 霓虹金 */
```

### 文字色
```css
--text-primary: #F8FAFC  /* 主文字 - 白色 */
--text-secondary: #94A3B8 /* 次要文字 - 灰蓝 */
```

---

## 二、字体系统

### 英文字体
```css
font-family: 'Orbitron', sans-serif;  /* 科幻标题字体 */
```
- 用途: 标题、章节标题、按钮文字
- 特点: 大写字母、字间距 0.05em

### 中文字体
```css
font-family: 'Noto Sans SC', sans-serif;  /* 思源黑体 */
```

### 代码字体
```css
font-family: 'Fira Code', monospace;  /* 代码字体 */
```

---

## 三、字号规范

| 元素 | 字号 | 字重 | 用途 |
|------|------|------|------|
| 封面标题 | 72-150px | 900 | clamp(72px, 10vw, 150px) |
| 章节标题 | 56-110px | 800 | clamp(56px, 8vw, 110px) |
| 卡片标题 | 36px | 700 | 功能卡片标题 |
| 正文 | 28px | 400 | 内容描述 |
| 徽章文字 | 18px | 600 | 标签/徽章 |

---

## 四、特效与动画

### 1. 背景动画
- **移动网格**: 60px 网格，20s 线性移动
- **扫描线**: 水平扫描线效果
- **光晕脉冲**: 2个光晕球，4s 呼吸动画

### 2. 浮动粒子
```css
.particle {
  width: 4px;
  height: 4px;
  background: var(--neon-blue);
  border-radius: 50%;
  box-shadow: 0 0 10px var(--neon-blue);
  animation: floatUp 8s linear infinite;
}
```

### 3. 标题霓虹发光
```css
text-shadow:
  0 0 20px var(--neon-blue),
  0 0 40px var(--neon-blue),
  0 0 80px rgba(0, 229, 255, 0.5);
animation: titleGlow 3s ease-in-out infinite;
```

### 4. 3D卡片悬停
```css
.card-3d:hover {
  transform: translateY(-16px) rotateX(5deg) rotateY(-5deg);
  border-color: var(--neon-blue);
  box-shadow:
    0 20px 60px rgba(0, 229, 255, 0.3),
    0 0 100px rgba(0, 229, 255, 0.2);
}
```

### 5. 全息图标扫描
```css
.holo-icon::after {
  background: linear-gradient(45deg, transparent 40%, rgba(255,255,255,0.1) 50%, transparent 60%);
  animation: holoScan 3s linear infinite;
}
```

---

## 五、组件样式

### 徽章
```css
.badge {
  background: rgba(0, 229, 255, 0.1);
  border: 2px solid rgba(0, 229, 255, 0.3);
  border-radius: 100px;
  padding: 12px 28px;
  box-shadow: 0 0 20px rgba(0, 229, 255, 0.2);
}
```

### 导航按钮
```css
.nav-btn {
  width: 64px;
  height: 64px;
  background: rgba(0, 229, 255, 0.1);
  border: 2px solid rgba(0, 229, 255, 0.3);
  border-radius: 50%;
  box-shadow: 0 0 20px rgba(0, 229, 255, 0.2);
}
```

### 页面指示点
```css
.page-dot.active {
  width: 48px;
  background: var(--neon-blue);
  box-shadow: 0 0 30px var(--neon-blue);
}
```

---

## 六、布局模式

### 两栏对比
```css
.comparison {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: var(--space-lg);
  perspective: 1500px;
}
```

### 四栏网格
```css
.grid-4 {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: var(--space-md);
}
```

---

## 七、关键CSS代码片段

### 幻灯片容器
```css
.slideshow-container {
  width: 100vw;
  height: 100vh;
  perspective: 2000px;
}
```

### 幻灯片切换
```css
.slide {
  opacity: 0;
  transform: scale(1.05) translateZ(-100px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.slide.active {
  opacity: 1;
  transform: scale(1) translateZ(0);
}
```

### 进度条
```css
.progress-bar {
  height: 4px;
  background: linear-gradient(90deg,
    var(--neon-blue),
    var(--neon-purple),
    var(--neon-pink));
}
```

---

## 八、动画关键帧

```css
/* 标题发光 */
@keyframes titleGlow {
  0%, 100% {
    text-shadow: 0 0 20px var(--neon-blue), 0 0 40px var(--neon-blue);
  }
  50% {
    text-shadow: 0 0 30px var(--neon-blue), 0 0 60px var(--neon-blue),
                 0 0 100px rgba(0, 229, 255, 0.8);
  }
}

/* 边框发光 */
@keyframes borderGlow {
  0%, 100% { filter: hue-rotate(0deg); }
  50% { filter: hue-rotate(180deg); }
}

/* 浮动上升 */
@keyframes floatUp {
  0% { transform: translateY(100vh) scale(0); opacity: 0; }
  10% { opacity: 1; }
  90% { opacity: 1; }
  100% { transform: translateY(-100px) scale(1); opacity: 0; }
}
```

---

## 九、Google Fonts 链接

```
https://fonts.googleapis.com/css2?family=Fira+Code:wght@400;500;600;700&family=Orbitron:wght@400;500;600;700;800;900&family=Noto+Sans+SC:wght@400;500;700;900&display=swap
```

---

## 十、使用建议

1. **深色背景** - 适合暗场演示，科技感强
2. **霓虹强调** - 重点信息用霓虹色突出
3. **适度动画** - 动画要克制，避免过度干扰
4. **大字体** - 标题 72-150px，适合投影
5. **玻璃质感** - backdrop-filter: blur(20px)

---

## 十一、适用场景

- ✅ AI/科技产品发布会
- ✅ 游戏展示
- ✅ 未来概念演示
- ✅ 开发者大会
- ✅ 技术分享

---

## 十二、与其它风格对比

| 风格 | 背景 | 色调 | 适用场景 |
|------|------|------|----------|
| 科幻风 | 深色 #0A0A1A | 霓虹色 | 科技/AI |
| 等距工业风 | 浅灰 #F5F5F5 | 橙/蓝 | 工业/制造 |
| 手绘风 | 纸质 #F5F0EB | 彩色手绘 | 教育/创意 |
| 麦肯锡风 | 白色 | 深蓝+金 | 商务咨询 |

---

*更新日志:*
- *2026-03-01: 初始创建，从 scifi 模板提取设计要素*
