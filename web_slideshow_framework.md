# 全屏网页幻灯片框架

> 用于替代 PPT 的 HTML 全屏演示系统，支持动画、翻页、全屏、演讲备注等完整功能。
> 整合 PPT Master 工具集的有效经验。

---

## 框架特点

| 特点 | 说明 |
|------|------|
| **真·全屏** | 100vw × 100vh，F 键切换全屏 |
| **超大字体** | 标题 60-100px，适合大教室投影 |
| **丰富动画** | 元素进入、页面切换、脉冲效果 |
| **键盘控制** | 方向键翻页、F 全屏、N 备注等 |
| **演讲备注** | 按 N 键显示演讲者备注/讲稿 |
| **进度指示** | 页码、进度条、点状指示器 |
| **配置驱动** | 支持 config.json 快速切换主题 |
| **易于扩展** | 模块化设计，添加新页面只需复制结构 |

---

## 核心代码结构

### HTML 结构
```html
<div class="slideshow-container">
  <!-- 每一页 -->
  <div class="slide active" data-page="1">
    页面内容
    <!-- 演讲备注（可选） -->
    <div class="speaker-notes" data-notes="这是演讲备注内容"></div>
  </div>
  <div class="slide" data-page="2">页面内容</div>
  ...
</div>

<!-- 演讲者备注面板（默认隐藏） -->
<div class="speaker-panel" id="speakerPanel">
  <div class="speaker-notes-content" id="speakerNotesContent"></div>
  <div class="speaker-next-preview" id="speakerNextPreview"></div>
</div>

<!-- 控件 -->
<div class="page-number" id="pageNumber">01</div>
<div class="page-indicator" id="pageIndicator"></div>
<div class="nav-controls">
  <button class="nav-btn" id="prevBtn">◀</button>
  <button class="nav-btn" id="nextBtn">▶</button>
</div>
<div class="progress-bar" id="progressBar"></div>
```

### CSS 关键样式
```css
body {
  font-family: "Microsoft YaHei", "微软雅黑", Arial, sans-serif;
  background: #000;
  overflow: hidden;
  /* 不要设置 cursor: none; 保持鼠标可见 */
}

.slide {
  position: absolute;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: all 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}
.slide.active {
  opacity: 1;
}

/* 演讲者备注面板 */
.speaker-panel {
  position: fixed;
  right: 20px;
  top: 20px;
  width: 400px;
  max-height: 80vh;
  background: rgba(0, 0, 0, 0.95);
  border: 1px solid #333;
  border-radius: 10px;
  padding: 20px;
  color: #fff;
  display: none;
  z-index: 1000;
  overflow-y: auto;
}
.speaker-panel.visible {
  display: block;
}
```

### JavaScript 核心逻辑
```javascript
class Slideshow {
  constructor() {
    this.slides = document.querySelectorAll('.slide');
    this.currentSlide = 0;
    this.notesVisible = false;
    // 初始化...
  }

  goToSlide(index) {
    this.slides[this.currentSlide].classList.remove('active');
    this.currentSlide = index;
    this.slides[this.currentSlide].classList.add('active');
    this.updateSpeakerNotes();
  }

  next() {
    if (this.currentSlide < this.totalSlides - 1)
      this.goToSlide(this.currentSlide + 1);
  }

  prev() {
    if (this.currentSlide > 0)
      this.goToSlide(this.currentSlide - 1);
  }

  toggleSpeakerNotes() {
    this.notesVisible = !this.notesVisible;
    const panel = document.getElementById('speakerPanel');
    panel.classList.toggle('visible', this.notesVisible);
    this.updateSpeakerNotes();
  }

  updateSpeakerNotes() {
    const currentSlide = this.slides[this.currentSlide];
    const notes = currentSlide.querySelector('.speaker-notes');
    const content = document.getElementById('speakerNotesContent');

    if (notes && notes.dataset.notes) {
      content.textContent = notes.dataset.notes;
    } else {
      content.textContent = '无演讲备注';
    }

    // 更新下一页预览
    if (this.currentSlide < this.totalSlides - 1) {
      const nextSlide = this.slides[this.currentSlide + 1];
      // ... 预览逻辑
    }
  }
}
```

---

## 操作方式

| 按键 | 功能 |
|------|------|
| `→` / `空格` / `PageDown` | 下一页 |
| `←` / `PageUp` | 上一页 |
| `F` | 切换全屏 |
| `N` | 显示/隐藏演讲备注 |
| `ESC` | 退出全屏/隐藏备注 |
| `Home` | 第一页 |
| `End` | 最后一页 |
| 点击底部圆点 | 跳转到指定页 |

---

## 项目标准化结构

借鉴 PPT Master 的项目结构：

```
projects/
├── my_presentation_html_20260228/
│   ├── index.html          # 主幻灯片文件
│   ├── config.json         # 配置文件（主题、动画）
│   ├── notes/              # 演讲备注目录
│   │   ├── 01_封面.md
│   │   ├── 02_目录.md
│   │   └── total.md        # 完整讲稿（可选）
│   ├── assets/             # 图片/图标资源
│   │   ├── images/
│   │   └── icons/
│   └── README.md           # 项目说明
```

**命名规范**：`项目名_html_日期`
- 示例：`tech_share_html_20260228`

---

## 配置文件系统

支持通过 `config.json` 快速切换主题和设置：

```json
{
  "project": {
    "name": "技术分享",
    "author": "演讲者姓名",
    "date": "2026-02-28"
  },
  "theme": "tech_industrial",
  "format": "16:9",
  "fonts": {
    "title": "64px Bold Microsoft YaHei",
    "subtitle": "48px Bold",
    "body": "22px Regular",
    "notes": "18px Regular"
  },
  "colors": {
    "primary": "#FF6B35",
    "secondary": "#00D4FF",
    "accent": "#A855F7",
    "bg": "#0a0a1a",
    "card": "rgba(30,37,48,0.9)"
  },
  "animations": {
    "slideTransition": "fade 0.8s",
    "elementEntrance": "slideInUp 0.6s",
    "pulse": "2s infinite"
  },
  "controls": {
    "keyboard": true,
    "speakerNotes": true,
    "autoAdvance": false,
    "autoAdvanceInterval": 5
  },
  "export": {
    "includeNotes": false,
    "pdfPageFormat": "A4"
  }
}
```

---

## 演讲备注系统

### 备注格式（notes/ 目录）

**单页备注** (`01_封面.md`):
```markdown
# 01_封面

欢迎各位同事参加本次技术分享。

开场白（约2分钟）：
- 问候与自我介绍
- 今天分享的主题
- 预期收获

重点提示：
- 确保声音设备正常
- 提醒观众关闭手机静音
```

**完整讲稿** (`total.md`):
```markdown
# 01_封面

欢迎各位...

---

# 02_目录

本次分享分为三个部分...

---

# 03_第一部分

第一部分的核心内容...
```

### JavaScript 加载备注

```javascript
// 自动加载 notes/ 目录中的备注
async function loadSpeakerNotes() {
  const slideNum = String(currentSlide + 1).padStart(2, '0');
  const slideTitle = slides[currentSlide].querySelector('h2')?.textContent || '未知';
  const noteFile = `notes/${slideNum}_${slideTitle}.md`;

  try {
    const response = await fetch(noteFile);
    const text = await response.text();
    // 解析 Markdown 并显示
    showSpeakerNotes(parseMarkdown(text));
  } catch (e) {
    // 如果没有单独文件，尝试从 total.md 提取
    extractFromTotalNotes(slideNum, slideTitle);
  }
}
```

---

## 设计风格主题

整合 PPT Master 的 21 种设计风格，可直接应用：

### 1. 科技工业风 (Tech Industrial)
```json
{
  "colors": {
    "primary": "#FF6B35",
    "secondary": "#00D4FF",
    "bg": "#E8E8E8",
    "card": "#FFFFFF"
  },
  "features": ["等距3D", "技术标注", "网格背景"]
}
```

### 2. 麦肯锡风 (McKinsey)
```json
{
  "colors": {
    "primary": "#005587",
    "accent": "#F5A623",
    "bg": "#FFFFFF",
    "card": "#ECF0F1"
  },
  "features": ["数据驱动", "专业留白", "左侧蓝条"]
}
```

### 3. 顶级咨询风 (Top Consultant)
```json
{
  "colors": {
    "bg_dark": "#0D1117",
    "gold": "#D4AF37",
    "purple_blue": "#6366F1"
  },
  "features": ["深色封面", "Exhibit标题条", "金色装饰"]
}
```

### 4. 谷歌风 (Google)
```json
{
  "colors": {
    "blue": "#4285F4",
    "red": "#EA4335",
    "yellow": "#FBBC04",
    "green": "#34A853"
  },
  "features": ["四色品牌", "Material Design", "圆角卡片"]
}
```

### 5. 中汽研现代风 (CATARC Modern)
```json
{
  "colors": {
    "dark": "#001529",
    "tech_blue": "#1890FF",
    "neon_cyan": "#00E5FF"
  },
  "features": ["未来感", "非对称设计", "HUD显示"]
}
```

### 6. 招商银行风
```json
{
  "colors": {
    "red": "#C41230",
    "gold": "#C9A962",
    "bg": "#FAFAFA"
  },
  "features": ["极简轻奢", "精致双线", "多层圆环"]
}
```

更多风格详见 `ppt_design_styles.md`（21种完整风格库）

---

## 设计规范

### 默认配色方案
```css
--primary-orange: #FF6B35
--primary-cyan: #00D4FF
--primary-purple: #A855F7
--primary-green: #10B981
--bg-dark: #0a0a1a
--bg-card: rgba(30,37,48,0.9)
```

### 字体大小
| 元素 | 字号 | 字重 |
|------|------|------|
| 封面主标题 | 100px | 900 |
| 页面标题 | 60px | bold |
| 卡片标题 | 32-36px | bold |
| 正文 | 20-22px | regular |
| 辅助文字 | 14-16px | regular |
| 演讲备注 | 16-18px | regular |

### 间距规范
- 卡片间距: 40-50px
- 列表项间距: 15px
- 内边距: 30-50px
- 圆角: 15-30px

---

## 页面模板

### 1. 封面页模板
```html
<div class="slide slide-cover active">
  <div class="cover-bg-grid"></div>
  <div class="cover-glow cover-glow-1"></div>
  <div class="cover-glow cover-glow-2"></div>
  <div class="cover-title">主标题</div>
  <div class="cover-subtitle">副标题</div>
  <div class="cover-tags">
    <div class="cover-tag tag-1">标签1</div>
    <div class="cover-tag tag-2">标签2</div>
  </div>
</div>
```

### 2. 三栏架构页模板
```html
<div class="slide slide-architecture">
  <div class="arch-container">
    <div class="arch-card arch-card-1">左侧内容</div>
    <div class="arch-core">中央核心</div>
    <div class="arch-card arch-card-3">右侧内容</div>
  </div>
</div>
```

### 3. 四宫格内容页模板
```html
<div class="slide slide-skills">
  <div class="slide-title">页面标题</div>
  <div class="skills-grid">
    <div class="skill-card skill-1">内容1</div>
    <div class="skill-card skill-2">内容2</div>
    <div class="skill-card skill-3">内容3</div>
    <div class="skill-card skill-4">内容4</div>
  </div>
</div>
```

### 4. 流程页模板
```html
<div class="slide slide-flow">
  <div class="slide-title">流程标题</div>
  <div class="flow-container">
    <div class="flow-step flow-step-1"><div class="flow-box">步骤1</div></div>
    <div class="flow-arrow">→</div>
    <div class="flow-step flow-step-2"><div class="flow-box">步骤2</div></div>
    ...
  </div>
</div>
```

### 5. 结束页模板
```html
<div class="slide slide-end">
  <div class="end-title">感谢观看</div>
  <div class="end-subtitle">THANK YOU</div>
  <div class="end-info">...</div>
</div>
```

---

## 常用组件

### 卡片组件
```html
<div class="arch-card arch-card-1">
  <div class="arch-icon"><svg>...</svg></div>
  <div class="arch-title">标题</div>
  <div class="arch-subtitle">副标题</div>
  <ul class="arch-list">
    <li>列表项1</li>
    <li>列表项2</li>
  </ul>
</div>
```

### 技能卡片组件
```html
<div class="skill-card skill-1">
  <div class="skill-header">
    <span class="skill-number">01</span>
    <div class="skill-name">名称 <span>英文</span></div>
  </div>
  <div class="skill-desc">描述内容</div>
</div>
```

---

## 动画效果

### 进入动画
```css
@keyframes slideInUp {
  from { opacity: 0; transform: translateY(50px); }
  to { opacity: 1; transform: translateY(0); }
}
@keyframes fadeInDown {
  from { opacity: 0; transform: translateY(-30px); }
  to { opacity: 1; transform: translateY(0); }
}
```

### 脉冲动画（用于强调元素）
```css
@keyframes corePulse {
  0%, 100% { box-shadow: 0 0 80px rgba(255,107,53,0.5); }
  50% { box-shadow: 0 0 150px rgba(255,107,53,0.8); }
}
```

### 旋转动画
```css
@keyframes rotate {
  from { transform: rotate(0deg); }
  to { transform: rotate(360deg); }
}
```

---

## 质量检查工具

借鉴 PPT Master 的 `svg_quality_checker.py`：

```javascript
// HTML 幻灯片质量检查器
const SlideshowQualityChecker = {
  checks: {
    // 对比度检查
    contrast(element) {
      const bg = getComputedStyle(element).backgroundColor;
      const fg = getComputedStyle(element).color;
      return this.calculateContrastRatio(bg, fg) >= 4.5;
    },

    // 字号检查
    fontSize(element) {
      const size = parseInt(getComputedStyle(element).fontSize);
      const tag = element.tagName;
      const minSizes = { H1: 60, H2: 48, P: 20 };
      return size >= (minSizes[tag] || 16);
    },

    // 动画数量检查
    animations(slide) {
      const anims = slide.querySelectorAll('[class*="anim"], [class*="fade"], [class*="slide"]');
      return anims.length <= 8;
    },

    // 内容密度检查
    contentDensity(slide) {
      const text = slide.innerText.trim();
      const words = text.length;
      return words <= 500; // 每页不超过500字
    }
  },

  checkAll() {
    const slides = document.querySelectorAll('.slide');
    const issues = [];

    slides.forEach((slide, index) => {
      // 检查字号
      slide.querySelectorAll('h1, h2, p').forEach(el => {
        if (!this.checks.fontSize(el)) {
          issues.push(`第${index+1}页: ${el.tagName}字号过小`);
        }
      });

      // 检查动画数量
      if (!this.checks.animations(slide)) {
        issues.push(`第${index+1}页: 动画数量过多`);
      }

      // 检查内容密度
      if (!this.checks.contentDensity(slide)) {
        issues.push(`第${index+1}页: 文字内容过多`);
      }
    });

    return issues;
  }
};
```

---

## 输入转换工具

复用 PPT Master 的输入工具准备内容：

```bash
# 1. 从网页抓取内容
python3 C:/Users/31681/ppt-master/tools/web_to_md.py https://example.com/article

# 2. 从 PDF 提取内容
python3 C:/Users/31681/ppt-master/tools/pdf_to_md.py document.pdf

# 3. 然后用 AI 将 Markdown 转换为 HTML 幻灯片
```

---

## 使用流程

当用户需要制作新的演示网页时：

1. **准备内容**
   - 使用 `web_to_md.py` 或 `pdf_to_md.py` 提取内容
   - 或直接从用户提供的文档/图片中提取关键信息

2. **创建项目结构**
   - 按标准化命名创建项目目录
   - 创建 `config.json` 配置文件
   - 创建 `notes/` 目录存放演讲备注

3. **确定风格**
   - 根据 `ppt_design_styles.md` 选择合适的风格
   - 应用对应的配色和布局

4. **生成页面**
   - 确定需要多少页
   - 为每页选择合适的页面模板
   - 将内容填入模板结构

5. **添加备注**
   - 为每页编写演讲备注
   - 保存到 `notes/` 目录

6. **质量检查**
   - 运行质量检查工具
   - 检查对比度、字号、动画数量等

7. **生成 HTML**
   - 输出完整的 HTML 文件
   - 浏览器预览确认效果

---

## 完整模板文件

参考文件: `C:\Users\31681\Desktop\test\ppt_slideshow.html`

---

## 更新日志

- 2026-02-28: 创建框架，PPT Master 演示
- 2026-02-28: 整合 PPT Master 经验
  - 添加演讲备注系统（N键切换）
  - 添加项目标准化结构
  - 添加配置文件系统（config.json）
  - 整合21种设计风格
  - 添加质量检查工具
  - 添加输入转换工具引用
- 2026-03-01: 整合 UI-UX-Pro-Max 设计原则
  - 添加CSS变量系统
  - 添加专业过渡时间规范（150-300ms）
  - 添加交互反馈规则
  - 添加可访问性检查清单
  - 整合Vibrant & Block-based风格

---

## UI-UX-Pro-Max 设计原则

> 整合自 UI-UX-Pro-Max 技能 (npm: uipro-cli)
> 参考: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill

### CSS 变量系统

使用 CSS 自定义属性实现主题管理：

```css
:root {
  /* Colors - Dark Tech Green */
  --bg-primary: #0F172A;
  --bg-secondary: #1E293B;
  --bg-tertiary: #334155;
  --text-primary: #F8FAFC;
  --text-secondary: #94A3B8;
  --accent: #22C55E;
  --accent-glow: rgba(34, 197, 94, 0.4);

  /* Spacing - Large sections for impact */
  --space-xs: 12px;
  --space-sm: 24px;
  --space-md: 48px;
  --space-lg: 72px;
  --space-xl: 120px;

  /* Transitions */
  --transition-fast: 150ms cubic-bezier(0.4, 0, 0.2, 1);
  --transition-base: 200ms cubic-bezier(0.4, 0, 0.2, 1);
  --transition-smooth: 300ms cubic-bezier(0.4, 0, 0.2, 1);
}
```

### 设计风格：Vibrant & Block-based

| 特征 | 说明 |
|------|------|
| **关键词** | Bold, energetic, playful, block layout, geometric shapes |
| **适用场景** | Startups, creative agencies, gaming, tech, SaaS |
| **布局特点** | 大区块（48px+间距）、卡片式、高对比度 |
| **视觉效果** | 渐变文字、顶部彩色条、悬停位移 |

### 过渡时间规范

| 场景 | 时间 | 缓动函数 |
|------|------|----------|
| 微交互（按钮、悬停） | 150ms | cubic-bezier(0.4, 0, 0.2, 1) |
| 常规过渡 | 200ms | cubic-bezier(0.4, 0, 0.2, 1) |
| 页面切换 | 300ms | cubic-bezier(0.4, 0, 0.2, 1) |

**重要**：不要使用超过 300ms 的过渡时间，会让界面感觉迟钝。

### 交互反馈规则

```css
/* 所有可点击元素必须有 */
.card, .nav-btn, .page-dot, .feature-card {
  cursor: pointer;
  transition: all var(--transition-base);
}

/* 悬停效果：颜色 + 阴影 + 轻微位移 */
.card:hover {
  transform: translateY(-8px);
  border-color: var(--accent-glow);
  box-shadow: 0 20px 60px rgba(34, 197, 94, 0.15);
}
```

### 卡片设计模式

```css
.card {
  background: var(--bg-secondary);
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 24px;
  padding: var(--space-md);
  position: relative;
  overflow: hidden;
}

/* 顶部彩色条 */
.card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 4px;
  background: linear-gradient(90deg, var(--accent), var(--cyan));
  opacity: 0;
  transition: opacity var(--transition-base);
}

.card:hover::before {
  opacity: 1;
}
```

### 字体系统

| 用途 | 字体 | 字重 |
|------|------|------|
| 标题 | Space Grotesk | 600-700 |
| 正文 | DM Sans | 400-500 |
| 代码 | Monaco/Consolas | - |

**Google Fonts 引入**：
```html
<link href="https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;700&family=Space+Grotesk:wght@400;500;600;700&display=swap" rel="stylesheet">
```

### 渐变文字效果

```css
.display-title {
  font-size: clamp(48px, 8vw, 96px);
  font-weight: 700;
  background: linear-gradient(135deg, var(--text-primary) 0%, var(--accent) 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}
```

### 响应式字号

使用 `clamp()` 实现流畅的响应式：

```css
/* 最小48px，首选8vw，最大96px */
font-size: clamp(48px, 8vw, 96px);

/* 最小36px，首选5vw，最大64px */
font-size: clamp(36px, 5vw, 64px);
```

### 可访问性检查清单

交付前必须检查：

- [ ] **无 emoji 图标** - 使用 SVG（Heroicons/Lucide）
- [ ] **cursor-pointer** - 所有可点击元素
- [ ] **悬停状态** - 颜色/阴影变化，过渡 150-300ms
- [ ] **对比度 4.5:1** - 浅色模式文字
- [ ] **focus 状态** - 键盘导航可见
- [ ] **prefers-reduced-motion** - 尊重用户偏好
- [ ] **aria-label** - 图标按钮有标签
- [ ] **响应式断点** - 375px, 768px, 1024px, 1440px

### 图标规范

**DO - 使用 SVG**:
```html
<svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
  <polyline points="9 18 15 12 9 6"/>
</svg>
```

**DON'T - 不要用 emoji**:
```html
<!-- ❌ 避免使用 -->
<button>👍 点赞</button>
<span>⚡ 快速</span>
```

### 常用反模式（Avoid）

| 反模式 | 问题 | 替代方案 |
|--------|------|----------|
| Flat design without depth | 缺乏层次感 | 添加阴影、边框、渐变 |
| Text-heavy pages | 视觉疲劳 | 使用图表、图标、卡片 |
| 过渡时间过长 | 感觉迟钝 | 保持在 150-300ms |
| 无 hover 反馈 | 用户困惑 | 添加颜色/阴影变化 |
| 小字号 | 难以阅读 | 标题 48px+，正文 16px+ |

### 动画延迟技巧

使用 `nth-child` 实现交错动画：

```css
.slide.active .animate-up:nth-child(1) { animation-delay: 0.1s; }
.slide.active .animate-up:nth-child(2) { animation-delay: 0.2s; }
.slide.active .animate-up:nth-child(3) { animation-delay: 0.3s; }
.slide.active .animate-up:nth-child(4) { animation-delay: 0.4s; }
```

---

## 经验教训（UI-UX-Pro-Max）

### 安装与使用

```bash
# 1. 安装 UI-UX-Pro-Max
npm install -g uipro-cli

# 2. 初始化为 Claude Code 使用
cd project-directory
uipro init --ai claude

# 3. 获取设计系统
python .claude/skills/ui-ux-pro-max/scripts/search.py "项目描述" --design-system -p "项目名"
```

### 设计流程

1. **先获取设计系统** - 运行 search.py 获取配色、字体、效果推荐
2. **应用 CSS 变量** - 使用 :root 定义主题
3. **遵循过渡时间** - 150-300ms，不要超过
4. **添加交互反馈** - cursor-pointer + hover 效果
5. **检查可访问性** - 对比度、焦点、标签

### 代码质量检查

```javascript
// 检查常见的 UI 问题
const UI_CHECKS = {
  // 检查过渡时间是否过长
  transitionTime(element) {
    const style = getComputedStyle(element);
    const duration = style.transitionDuration;
    // 解析时间值，确保不超过 300ms
    return parseFloat(duration) <= 0.3;
  },

  // 检查是否有 cursor-pointer
  hasCursorPointer(element) {
    if (element.onclick || element.classList.contains('card') ||
        element.classList.contains('btn')) {
      const style = getComputedStyle(element);
      return style.cursor === 'pointer';
    }
    return true;
  },

  // 检查是否使用了 emoji 作为图标
  hasEmojiIcons(text) {
    // 简单检查，实际可能需要更复杂的检测
    const emojiPattern = /[\p{Emoji_Presentation}\p{Extended_Pictographic}]/u;
    return emojiPattern.test(text);
  }
};
```

### 完整示例文件

参考: `C:\Users\31681\Desktop\test\html_slideshow_framework_uipro.html`
