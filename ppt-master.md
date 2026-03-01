# PPT Master 技能知识库

## 项目概述
PPT Master 是一个 AI 驱动的多格式 SVG 内容生成系统，通过多角色协作将源文档转化为高质量的 SVG 内容和 PPT。

**项目路径**: `C:\Users\31681\ppt-master`

---

## 核心工作流程

```
源文档(PDF/URL/MD) → 转换 → 创建项目 → 模板选项 → Strategist(八项确认)
→ Image_Generator(可选) → Executor(SVG生成+演讲备注) → 后处理 → 导出PPTX
```

---

## 🎯 用户自定义工作规则

### ⚠️ 强制要求：每个设计步骤前先提供选项

**在任何设计/执行工作之前，必须先给用户展示多个参考选项，让用户选择后再执行。**

#### 适用环节

| 环节 | 需要提供的选项 |
|------|----------------|
| **配色方案** | 提供 3-4 套配色方案供选择（商务、科技、清新等风格） |
| **设计风格** | 提供 2-3 种风格参考图/描述 |
| **封面布局** | 提供 3 种封面版式选项 |
| **内容页布局** | 每页提供 2-3 种排版方案 |
| **图标选择** | 关键图标提供 2-3 个候选 |
| **图片风格** | 提供 2-3 种图片风格描述/示例 |

#### 提问格式
```markdown
## 🎨 请选择 [配色方案 / 封面布局 / 其他]

| 选项 | 预览/描述 | 特点 |
|------|-----------|------|
| A | [描述或示例] | ... |
| B | [描述或示例] | ... |
| C | [描述或示例] | ... |

请输入 A/B/C 或提供自定义要求
```

> 💡 **原则**：先问后做，而非先做后改。让用户有参与感和控制权。

### 🎬 动画效果要求

**生成的 SVG 应包含简单的动画效果，提升演示体验。**

#### 推荐动画类型

| 动画类型 | 适用场景 | CSS 实现 |
|----------|----------|----------|
| **淡入** | 标题、内容逐个出现 | `@keyframes fadeIn { from { opacity: 0; } }` |
| **滑入** | 侧边内容进入 | `@keyframes slideIn { from { transform: translateX(-20px); opacity: 0; } }` |
| **缩放** | 重点强调元素 | `@keyframes scaleIn { from { transform: scale(0.8); opacity: 0; } }` |
| **计数动画** | 数字滚动效果 | 适用于数据展示页面 |
| **图表动画** | 柱状图/折线图生长 | 高度/路径渐进显示 |

#### 动画实现方式

**方式一：SVG 内嵌 CSS 动画**（推荐用于 HTML 演示）
```svg
<style>
  .fade-in {
    animation: fadeIn 0.8s ease-out forwards;
    animation-delay: 0.3s;
    opacity: 0;
  }
  @keyframes fadeIn {
    to { opacity: 1; }
  }
</style>
<text class="fade-in" x="640" y="200">标题</text>
```

**方式二：使用项目内置动画工具**
```bash
python3 tools/pptx_animations.py <项目路径>  # 为导出的 PPTX 添加动画
```

#### 动画使用原则

- **克制使用**：每页不超过 2-3 处动画
- **时序合理**：标题 → 核心内容 → 次要内容，依次出现
- **时长适中**：0.5s-1s 为宜，避免拖沓
- **保持一致**：同类元素使用相同动画效果

> ⚠️ **注意**：SVG 动画在浏览器预览中有效，导出到 PPT 后动画可能失效。如需 PPT 动画，使用 `pptx_animations.py` 工具。

### 🖼️ 图片设计原则（强制执行）

**视觉设计优先级：原始资料 > 背景设计 > 简单图形 > 手绘风格图片**

#### 设计优先级流程

```
1️⃣ 原始资料 → 2️⃣ 背景设计 → 3️⃣ 图标+形状 → 4️⃣ 手绘风格图片
```

#### 详细规则

| 优先级 | 方案 | 适用条件 | 实现方式 |
|--------|------|----------|----------|
| **1️⃣ 最高** | 使用原始资料中的图片 | 源文档包含相关图片 | 直接引用或优化处理 |
| **2️⃣ 次选** | 设计背景 + 简单图形 | 无合适图片 | SVG 背景渐变 + 几何形状 |
| **3️⃣ 补充** | 图标库 + 形状组合 | 表达概念/流程 | 使用内置图标库 |
| **4️⃣ 兜底** | 手绘风格图片 | 需要视觉表现时 | AI 生成手绘风格 |

#### 背景设计优先方案

当没有图片时，**优先设计背景**而非生成图片：

```svg
<!-- 渐变背景示例 -->
<defs>
  <linearGradient id="bg-gradient" x1="0%" y1="0%" x2="100%" y2="100%">
    <stop offset="0%" style="stop-color:#667eea;stop-opacity:1" />
    <stop offset="100%" style="stop-color:#764ba2;stop-opacity:1" />
  </linearGradient>
</defs>
<rect width="1280" height="720" fill="url(#bg-gradient)"/>

<!-- 几何装饰 -->
<circle cx="100" cy="100" r="50" fill="white" opacity="0.1"/>
<rect x="1100" y="600" width="100" height="100" fill="white" opacity="0.05" transform="rotate(45 1150 650)"/>
```

#### 简单形式原则

- **几何优先**：圆形、方形、三角形等基础形状
- **线条表达**：用线条分隔、引导视线
- **留白运用**：不填满，给内容呼吸空间
- **克制装饰**：每页装饰元素不超过 3-5 个

#### 手绘风格图片（如需生成）

**AI 生图提示词模板**：
```
手绘风格，[内容描述]，简洁线条，水彩/素描风格，
白色背景，minimalist，flat design，插画风格
```

**推荐风格关键词**：
- `hand drawn style` / `sketch style`
- `watercolor illustration` / `ink drawing`
- `minimalist flat illustration`
- `doodle style` / `line art`

---

## 六大 AI 角色

| 角色 | 文件 | 职责 | 触发条件 |
|------|------|------|----------|
| **策略师** | `roles/Strategist.md` | 八项确认 + 设计规范与内容大纲 | 项目启动（必须） |
| **模板设计师** | `roles/Template_Designer.md` | 生成页面模板 | `/create-template` 工作流 |
| **图片生成师** | `roles/Image_Generator.md` | AI 图片生成提示词与执行 | 图片方式含「C) AI 生成」 |
| **通用执行师** | `roles/Executor_General.md` | 通用灵活风格 SVG | 选择「A) 通用灵活」 |
| **咨询执行师** | `roles/Executor_Consultant.md` | 一般咨询风格 SVG | 选择「B) 一般咨询」 |
| **顶级咨询执行师** | `roles/Executor_Consultant_Top.md` | MBB 级咨询风格 SVG | 选择「C) 顶级咨询」 |
| **CRAP 优化师** | `roles/Optimizer_CRAP.md` | 视觉质量优化 | 用户要求优化（可选） |

---

## Strategist 八项确认（强制）

1. **画布格式** - PPT 16:9 / PPT 4:3 / 小红书 / 朋友圈等
2. **页数范围** - 基于内容量给出建议
3. **目标受众与场景** - 内部汇报 / 外部展示 / 培训等
4. **设计风格** - A) 通用灵活 B) 一般咨询 C) 顶级咨询（MBB级）
5. **配色方案** - 主导色、辅助色、强调色的 HEX 色值
6. **图标方式** - A) Emoji B) AI 生成 C) 内置图标库 D) 自定义路径
7. **图片使用** - A) 不使用 B) 用户提供 C) AI 生成 D) 占位符预留
8. **排版方案** - 字体组合 + 正文字号基准（18-24px）

---

## 常用命令

```bash
# 初始化项目
python3 tools/project_manager.py init <项目名> --format ppt169

# 源内容转换
python3 tools/pdf_to_md.py <PDF文件>
python3 tools/web_to_md.py <URL>
node tools/web_to_md.cjs <URL>  # 微信/高防站点

# 图片分析（用户提供图片时必须）
python3 tools/analyze_images.py <项目路径>/images

# 后处理三步骤（必须按顺序执行）
python3 tools/total_md_split.py <项目路径>      # 1. 拆分演讲备注
python3 tools/finalize_svg.py <项目路径>        # 2. 后处理SVG
python3 tools/svg_to_pptx.py <项目路径> -s final  # 3. 导出PPTX

# 质量检查
python3 tools/svg_quality_checker.py <项目路径>

# Gemini 水印去除
python3 tools/gemini_watermark_remover.py <图片路径>
```

---

## 支持的画布格式

| 格式 | 尺寸 | viewBox |
|------|------|---------|
| PPT 16:9 | 1280×720 | `0 0 1280 720` |
| PPT 4:3 | 1024×768 | `0 0 1024 768` |
| 小红书 | 1242×1660 | `0 0 1242 1660` |
| 朋友圈 | 1080×1080 | `0 0 1080 1080` |
| Story | 1080×1920 | `0 0 1080 1920` |
| 公众号头图 | 900×383 | `0 0 900 383` |

---

## SVG 技术约束（PPT 兼容性）

### 禁用功能黑名单
`clipPath` | `mask` | `<style>` | `class/id` | 外部 CSS | `<foreignObject>` | `textPath` | `@font-face` | `<animate*>` | `<script>` | `marker-end` | `<iframe>`

### PPT 兼容性规则
| ❌ 禁止 | ✅ 替代方案 |
|--------|-------------|
| `rgba()` 颜色 | `fill-opacity` / `stroke-opacity` |
| `<g opacity>` 组透明 | 每个子元素单独设置 |
| `<image opacity>` | 遮罩层叠加 |
| `marker-end` 箭头 | `<polygon>` 三角形 |

---

## 角色切换协议（强制执行）

1. **切换角色前必须阅读角色定义文件**
   ```bash
   view_file: roles/[角色名].md
   ```

2. **输出显式角色切换标记**
   ```markdown
   ## 【角色切换：[角色名称]】
   📖 **阅读角色定义**: `roles/[角色文件名].md`
   📋 **当前任务**: [简述任务]
   ```

3. **每个阶段结束必须输出检查点**

---

## 关键路径

| 资源 | 路径 |
|------|------|
| 规则手册 | `AGENTS.md` |
| 工作流 | `.agent/workflows/generate-ppt.md` |
| 角色定义 | `roles/` |
| 图表模板 | `templates/charts/` |
| 图标库 | `templates/icons/` (640+ 图标) |
| 工具集 | `tools/` |
| 示例项目 | `examples/` (15个项目，229页SVG) |
| 文档 | `docs/` |

---

## AI 模型推荐
- **最佳效果**: Opus 4.5
- **免费方案**: Antigravity.dev（免费使用 Opus 4.5）
- **生图建议**: Gemini（下载 Full Size，分辨率更高）
