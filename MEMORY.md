# Memory - Claude Code

## 快速链接

### 核心框架
- [全屏网页幻灯片框架](web_slideshow_framework.md) - **HTML 演示系统，替代 PPT** ⭐
  - **Frontend-Slides 技能**: 12种预设风格，强制视口适配，零依赖
- [PPT/网页设计风格库](ppt_design_styles.md) - **主流设计风格速查** ⭐
- [科幻风格模板](scifi_style_template.md) - **Sci-Fi 风格模板，AI/科技演示** ⭐

### 外部工具
- [UI-UX-Pro-Max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) - **UI/UX 设计系统生成器** (npm: uipro-cli)
- [Everything Claude Code](https://github.com/affaan-m/everything-claude-code) - **Anthropic 黑客松冠军配置** (已安装到 `~/.claude/`)

### GitHub 仓库
- **记忆仓库**: https://github.com/liPeng-5544510/claude-code-memory
  - 路径: `C:\Users\31681\Desktop\claude-code-memory`
  - **重要**: 当用户说"更新记忆"或"上传"时，自动执行：
    ```bash
    cp C:\Users\31681\.claude\projects\C--Users-31681-Desktop-test\memory\* C:\Users\31681\Desktop\claude-code-memory\
    cd C:\Users\31681\Desktop\claude-code-memory
    git add .
    git commit -m "update memory"
    git push
    ```

### 专项经验
- [浏览器书签清理](browser_bookmark_cleanup.md) - 处理云端同步问题
- [技术指南封面设计风格](design_style_tech_guide.md) - 等距3D科技风

### 项目参考
- [PPT Master 技能知识库](ppt-master.md) - PPT 生成系统

---

## 最近工作

### 2026-03-01: GitHub 记忆仓库建立

**工作内容**: 创建 GitHub 仓库存储 Claude Code 记忆文件

**仓库信息**:
- URL: https://github.com/liPeng-5544510/claude-code-memory
- 本地路径: `C:\Users\31681\Desktop\claude-code-memory`

**自动更新命令**:
```bash
# 复制记忆文件
cp C:\Users\31681\.claude\projects\C--Users-31681-Desktop-test\memory\* C:\Users\31681\Desktop\claude-code-memory\

# 提交并推送
cd C:\Users\31681\Desktop\claude-code-memory
git add .
git commit -m "update memory"
git push
```

**触发词**: "更新记忆"、"上传"、"同步"

---

### 2026-02-28: 设计风格库完整版 (21种风格)

**工作内容**: 学习并整理 PPT Master 全部 21 种设计风格

**成果**: 更新 `ppt_design_styles.md` 完整版
- 21 种设计风格速查表
- 每种风格的详细配色方案
- 特色元素说明
- 风格选择指南 (按场景/按调性)
- 企业/机构配色速查

**风格清单**:
麦肯锡、顶级咨询、咨询顾问、谷歌、通用灵活、像素复古、易理、智能红、
政府蓝、政府红、学术答辩、医学、Anthropic、重庆大学、中国电建(常规+现代)、
中汽研(常规+商务+现代)、招商银行、科技工业

---

### 2026-02-28: 全屏网页幻灯片框架 (整合 PPT Master 经验)

**用户需求**: 给大教室学生做演示，需要比 PPT 更好的展示效果

**解决方案**: 创建了完整的 HTML 幻灯片系统
- 5 页内容：封面、架构、技能、流程、结束
- 键盘控制翻页，F 键全屏，N 键演讲备注
- 丰富动画效果
- 超大字体，适合投影

**新功能** (整合自 PPT Master):
- **演讲备注系统** - N 键切换显示，支持 notes/ 目录
- **项目标准化结构** - `项目名_html_日期` 命名规范
- **配置文件** - config.json 快速切换主题
- **质量检查工具** - 自动检查对比度/字号/动画数
- **21种设计风格** - 整合自 ppt_design_styles.md

**模板文件**: `C:\Users\31681\Desktop\test\ppt_slideshow.html`

**重要**: 用户之后提供新内容时，优先使用这个框架制作网页

---

### 2026-02-28: PPT Master 工具集经验整合

**学习内容**: 分析 `C:\Users\31681\ppt-master\tools` 目录下的工具集

**可借鉴到 HTML 幻灯片的功能**:

| PPT Master 工具 | HTML 实现方案 | 用途 |
|----------------|--------------|------|
| `notes/` + `total_md_split.py` | N键备注面板 | 演讲者视图 |
| `project_manager.py` | 标准项目结构 | 项目管理 |
| `config.py` | `config.json` | 主题配置 |
| `svg_quality_checker.py` | JS质量检查器 | 自动检测问题 |
| `web_to_md.py` | 内容准备 | 从网页抓取内容 |
| 21种风格模板 | 主题系统 | 快速切换风格 |

**已整合功能**:
- 演讲备注系统（按N显示）
- 项目命名规范（`项目名_html_日期`）
- 配置文件驱动（config.json）
- 质量检查工具（对比度/字号/动画）
- 21种设计风格集成

---

### 2026-03-01: UI-UX-Pro-Max 技能学习与整合

**技能来源**: https://github.com/nextlevelbuilder/ui-ux-pro-max-skill

**安装命令**:
```bash
npm install -g uipro-cli
uipro init --ai claude
```

**核心设计系统**:
- **风格**: Vibrant & Block-based（大胆块状布局）
- **配色**: Dark Tech Green (#0F172A + #22C55E)
- **字体**: Space Grotesk（标题）+ DM Sans（正文）
- **过渡**: 150-300ms cubic-bezier(0.4, 0, 0.2, 1)

**关键设计原则**:
1. CSS 变量系统管理主题
2. 大区块布局（48px+ 间距）
3. 卡片设计带顶部彩色条
4. 悬停效果：位移 + 阴影 + 边框高亮
5. 所有可点击元素必须 cursor-pointer
6. 使用 SVG 图标，禁止 emoji
7. 渐变文字效果增强视觉冲击

**可访问性检查清单**:
- [ ] 无 emoji 图标
- [ ] cursor-pointer 在可点击元素上
- [ ] 悬停状态有平滑过渡
- [ ] 对比度 ≥ 4.5:1
- [ ] focus 状态可见
- [ ] prefers-reduced-motion 尊重
- [ ] 响应式断点检查

**示例文件**: `C:\Users\31681\Desktop\test\html_slideshow_framework_uipro.html`

**更新文档**: `web_slideshow_framework.md` 新增 "UI-UX-Pro-Max 设计原则" 章节

---

### 2026-03-01: Frontend-Slides 技能学习与整合

**技能路径**: `C:\Users\31681\.claude\skills\frontend-slides`

**12种预设风格**:
| 风格 | 适用场景 | 关键特征 |
|------|----------|----------|
| **Bold Signal** | 路演、发布会 | 炭黑+热橙，超大数字 |
| **Electric Studio** | 客户演示 | 黑白+钴蓝，双面板分屏 |
| **Neon Cyber** | AI/开发工具 | 青色+洋红，光晕粒子 |
| **Terminal Green** | API/CLI工具 | 终端绿，扫描线效果 |
| **Dark Botanical** | 奢侈品牌 | 模糊圆圈，细线，克制 |
| **Creative Voltage** | 创意工作室 | 半点纹理，徽章，强对比 |
| **Notebook Tabs** | 报告/评审 | 纸张，彩色标签，活页细节 |
| **Pastel Geometry** | 产品概览 | 垂直药丸，圆角卡，软阴影 |
| **Split Pastel** | 机构介绍 | 分割背景，圆角标签 |
| **Vintage Editorial** | 个人品牌 | 几何装饰，边框引用 |
| **Swiss Modern** | 企业/数据 | 可见网格，不对称 |
| **Paper & Ink** | 散文/宣言 | 拉引语，首字下沉 |

**强制性技术规范**:
```css
/* 视口适配 - 不可协商 */
.slide {
    width: 100vw;
    height: 100vh;
    height: 100dvh;  /* 动态视口 */
    overflow: hidden;
}

/* 响应式字号 */
--title-size: clamp(2rem, 6vw, 5rem);
--h2-size: clamp(1.25rem, 3.5vw, 2.5rem);
--body-size: clamp(0.875rem, 1.5vw, 1.25rem);
```

**内容密度限制**:
- 标题页: 1标题 + 1副标题
- 内容页: 1标题 + 4-6要点
- 代码页: 8-10行最多
- 特性网格: 6卡片最多

**心情 → 风格映射**:
- 印象/自信 → Bold Signal, Electric Studio
- 兴奋/活力 → Neon Cyber, Creative Voltage
- 平静/专注 → Notebook Tabs, Swiss Modern
- 受启发/感动 → Dark Botanical, Vintage Editorial

**完整导航**:
- 键盘: ← → 方向键，F 全屏
- 触摸: 滑动翻页
- 滚轮: 节流滚动翻页
- 点状导航: 右侧跳转

**可访问性**:
- `prefers-reduced-motion` 尊重用户偏好
- 语义化 HTML (main, section, nav)
- 键盘导航支持
- 对比度 ≥ 4.5:1

**示例文件**: `C:\Users\31681\Desktop\test\ppt_master_intro_neon.html`

**更新文档**: `web_slideshow_framework.md` 新增 "Frontend-Slides 技能整合" 章节

---

### 2026-03-01: 科幻风格模板存储

**模板文件**: `C:\Users\31681\Desktop\test\html_slideshow_framework_scifi.html`

**设计风格**: 科幻3D风格 (Sci-Fi 3D)

**核心特点**:
- 深色背景 #0A0A1A + 霓虹色强调 (蓝#00E5FF、紫#A855F7、粉#EC4899)
- Orbitron 科幻字体 + 思源黑体
- 大字体: 标题 72-150px，适合投影
- 3D卡片悬停效果 (translateY + rotateX + rotateY)
- 丰富背景动画: 移动网格、扫描线、光晕脉冲、浮动粒子
- 全息图标扫描效果
- 玻璃质感: backdrop-filter: blur(20px)

**适用场景**: AI/科技发布会、游戏展示、未来概念演示、开发者大会

**模板文档**: `scifi_style_template.md` - 完整设计要素提取

**重要**: 以后生成科技/AI相关演示时，优先使用此科幻风格模板

---

### 2026-03-01: 大教室投影核心原则（重要更新）

**问题**: 之前的幻灯片在大教室演示时，后排学生看不清

**核心原则**:
1. **超大字体** - 标题 80-160px，确保后排可见
2. **图片为主** - 大图标/emoji 占主要空间
3. **文字精炼** - 只有关键词，每页 <100 字
4. **画幅填满** - 2×2/3×2 大板块布局，无空白
5. **视觉冲击力** - 充实、鲜艳、有动画

**关键技术**:
- 使用 `clamp(50px, 10vw, 160px)` 响应式超大字体
- 使用 `dvh` 动态视口高度替代 `vh`
- 使用 `min(80px, 6dvh)` 响应式边距控制
- `justify-content: flex-start` 防止内容顶部被裁剪
- 4K 优化：根字体缩放 + 字体渲染优化

**边距溢出控制**:
```css
/* ❌ 错误：垂直居中会导致内容被裁剪 */
.slide { justify-content: center; padding: 60px; }

/* ✅ 正确：从顶部开始 + 动态边距 */
.slide {
  justify-content: flex-start;
  padding: min(80px, 6dvh) min(40px, 4vw);
  overflow-y: auto;
}
```

**特效组件**:
- 粒子效果 - 50个浮动粒子，三种颜色
- 光晕脉冲 - 2个大光球，呼吸动画
- 移动网格背景 - 持续移动
- 扫描线效果 - CRT 复古风格
- 3D 卡片悬停 - perspective + rotate

**示例文件**: `C:\Users\31681\Desktop\test\ppt_master_final.html`

**更新文档**: `web_slideshow_framework.md` 新增 "大教室投影核心原则" 章节

---

## 核心经验

### 演示制作优先级

1. **HTML 网页 > PPT** - 网页支持动画、交互、易分享
2. **全屏展示 > 常规尺寸** - 大教室需要大字体、高对比度
3. **动画增强效果** - 但要克制，避免过度
4. **对称布局 > 不对称** - 更专业、更易理解

### 设计原则

- **信息密度要高** - 一页展示完整概念
- **字体要大** - 标题 60-100px
- **对比度要高** - 深色背景 + 亮色强调
- **动画要流畅** - 0.5-1s 过渡时间

### UI/UX 专业原则 (来自 UI-UX-Pro-Max)

- **过渡时间 150-300ms** - 超过会让界面感觉迟钝
- **所有可点击元素要有 cursor-pointer**
- **悬停反馈** - 颜色变化 + 阴影 + 轻微位移
- **使用 SVG 图标** - 不要用 emoji
- **CSS 变量管理主题** - 便于切换和维护
- **响应式字号** - 使用 clamp() 函数
- **对比度 ≥ 4.5:1** - 满足 WCAG 标准
