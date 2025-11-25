# 迪尚 AI 数智化平台 UI 规范落地清单

## 一、颜色变量定义（CSS 变量，全局引入）



```
/\* 1. 基础颜色（Arco Design 适配） \*/

:root {

&#x20; /\* 主色调 \*/

&#x20; --color-primary: #165DFF; /\* 品牌主色、按钮、选中态 \*/

&#x20; --color-primary-hover: #0E4BD8; /\* 主色hover态 \*/

&#x20; --color-primary-light: #EEF4FF; /\* 主色浅背景 \*/

&#x20;&#x20;

&#x20; /\* 背景色 \*/

&#x20; --color-bg-page: #F8F9FA; /\* 页面背景 \*/

&#x20; --color-bg-module: #FFFFFF; /\* 卡片、对话框背景 \*/

&#x20;&#x20;

&#x20; /\* 文字色 \*/

&#x20; --color-text-primary: #1D2129; /\* 标题、正文 \*/

&#x20; --color-text-secondary: #86909C; /\* 辅助说明 \*/

&#x20; --color-text-disabled: #C9CDD4; /\* 禁用文字 \*/

&#x20;&#x20;

&#x20; /\* 边框/分割线色 \*/

&#x20; --color-border: #E5E6EB; /\* 模块边框、分割线 \*/

&#x20; --color-border-focus: rgba(22, 93, 255, 0.1); /\* 输入框聚焦阴影 \*/

&#x20;&#x20;

&#x20; /\* 2. 业务板块专属色 \*/

&#x20; --color-design: #E67E22; /\* 趋势与设计：面料、设计稿相关 \*/

&#x20; --color-production: #00B42A; /\* 生产与供应链：排产、库存相关 \*/

&#x20; --color-marketing: #722ED1; /\* 营销与销售：客户、素材相关 \*/

&#x20; --color-service: #36CFFB; /\* 客户服务：客服、售后相关 \*/

&#x20; --color-management: #FF7D00; /\* 内部管理与协同：合同、培训相关 \*/

&#x20;&#x20;

&#x20; /\* 3. 功能状态色 \*/

&#x20; --color-success: #00B42A; /\* 成功、完成 \*/

&#x20; --color-warning: #FF7D00; /\* 警告、延期 \*/

&#x20; --color-error: #F53F3F; /\* 错误、禁用 \*/

&#x20; --color-loading: #165DFF; /\* 加载中、进行中 \*/

}
```

## 二、核心组件 HTML 结构示例（Vue 3 + Arco Design Vue）

### 2.1 整体布局框架（基础骨架）



```
\<template>

&#x20; \<!-- 根容器：100vh 全屏布局 -->

&#x20; \<div class="ai-platform-container" style="height: 100vh; overflow: hidden;">

&#x20;   \<!-- 1. 顶部状态栏（固定） -->

&#x20;   \<header class="top-status-bar">

&#x20;     \<div class="status-left">

&#x20;       \<!-- 用户信息（带角色标识） -->

&#x20;       \<div class="user-info">

&#x20;         \<span class="user-avatar">设\</span> \<!-- 设计师角色简写 -->

&#x20;         \<span class="user-name">张明（设计部）\</span>

&#x20;       \</div>

&#x20;     \</div>

&#x20;     \<div class="status-right">

&#x20;       \<!-- 系统通知 -->

&#x20;       \<a-bell :count="2" size="20" class="status-icon" />

&#x20;       \<!-- 帮助入口 -->

&#x20;       \<a-question-circle size="20" class="status-icon" />

&#x20;       \<!-- 设置入口 -->

&#x20;       \<a-setting size="20" class="status-icon" />

&#x20;     \</div>

&#x20;   \</header>

&#x20;   \<!-- 中间主体：左侧导航 + 中间交互区 + 右侧辅助区 -->

&#x20;   \<div class="main-container" style="display: flex; height: calc(100vh - 140px);">

&#x20;     \<!-- 2. 左侧板块导航（可折叠） -->

&#x20;     \<aside class="left-nav" :class="{ 'collapsed': isNavCollapsed }">

&#x20;       \<!-- 收藏夹入口 -->

&#x20;       \<div class="nav-favorite">

&#x20;         \<a-icon name="star" size="20" />

&#x20;         \<span class="nav-text" v-if="!isNavCollapsed">常用Agent\</span>

&#x20;       \</div>

&#x20;       \<!-- 业务板块列表 -->

&#x20;       \<ul class="nav-menu">

&#x20;         \<!-- 趋势与设计（当前选中） -->

&#x20;         \<li class="nav-item active">

&#x20;           \<a-icon name="palette" size="20" :style="{ color: 'var(--color-design)' }" />

&#x20;           \<span class="nav-text" v-if="!isNavCollapsed">趋势与设计\</span>

&#x20;         \</li>

&#x20;         \<!-- 生产与供应链 -->

&#x20;         \<li class="nav-item">

&#x20;           \<a-icon name="factory" size="20" :style="{ color: 'var(--color-production)' }" />

&#x20;           \<span class="nav-text" v-if="!isNavCollapsed">生产与供应链\</span>

&#x20;         \</li>

&#x20;         \<!-- 营销与销售 -->

&#x20;         \<li class="nav-item">

&#x20;           \<a-icon name="shopping-cart" size="20" :style="{ color: 'var(--color-marketing)' }" />

&#x20;           \<span class="nav-text" v-if="!isNavCollapsed">营销与销售\</span>

&#x20;         \</li>

&#x20;         \<!-- 客户服务 -->

&#x20;         \<li class="nav-item">

&#x20;           \<a-icon name="headset" size="20" :style="{ color: 'var(--color-service)' }" />

&#x20;           \<span class="nav-text" v-if="!isNavCollapsed">客户服务\</span>

&#x20;         \</li>

&#x20;         \<!-- 内部管理与协同 -->

&#x20;         \<li class="nav-item">

&#x20;           \<a-icon name="users" size="20" :style="{ color: 'var(--color-management)' }" />

&#x20;           \<span class="nav-text" v-if="!isNavCollapsed">内部管理与协同\</span>

&#x20;         \</li>

&#x20;       \</ul>

&#x20;       \<!-- 折叠按钮 -->

&#x20;       \<button class="collapse-btn" @click="isNavCollapsed = !isNavCollapsed">

&#x20;         \<a-icon :name="isNavCollapsed ? 'right' : 'left'" size="18" />

&#x20;       \</button>

&#x20;     \</aside>

&#x20;     \<!-- 3. 中间主交互区（对话模式） -->

&#x20;     \<main class="middle-content" style="flex: 1; overflow-y: auto; padding: 0 20px;">

&#x20;       \<!-- 对话记录区 -->

&#x20;       \<div class="chat-container">

&#x20;         \<!-- 系统通知 -->

&#x20;         \<div class="chat-system">2024-10-20 14:30 已唤醒「款式创新Agent」，可继续补充需求\</div>

&#x20;        &#x20;

&#x20;         \<!-- 用户消息 -->

&#x20;         \<div class="chat-item user">

&#x20;           \<div class="chat-avatar">用\</div>

&#x20;           \<div class="chat-bubble">@款式创新Agent 生成2024秋季商务西装设计稿，目标客群30-45岁男性高管\</div>

&#x20;         \</div>

&#x20;        &#x20;

&#x20;         \<!-- Agent消息（带设计稿预览） -->

&#x20;         \<div class="chat-item agent">

&#x20;           \<div class="chat-avatar" :style="{ backgroundColor: 'var(--color-design)' }">设\</div>

&#x20;           \<div class="chat-bubble">

&#x20;             \<div class="agent-name">款式创新Agent\</div>

&#x20;             \<div class="agent-content">已生成5套设计稿，核心元素：高支羊毛面料、简约戗驳领、隐形口袋，可查看预览：\</div>

&#x20;             \<!-- 设计稿预览（2D/3D切换） -->

&#x20;             \<div class="design-preview">

&#x20;               \<a-tabs v-model:active-key="previewTab">

&#x20;                 \<a-tab-pane key="2d" title="2D预览">

&#x20;                   \<img src="@/assets/fabrics/suit-2d.jpg" alt="2D设计稿" style="width: 200px; border-radius: 8px;" />

&#x20;                 \</a-tab-pane>

&#x20;                 \<a-tab-pane key="3d" title="3D预览">

&#x20;                   \<div class="3d-viewer" style="width: 200px; height: 280px; background: var(--color-bg-page); border-radius: 8px; display: flex; align-items: center; justify-content: center;">

&#x20;                     \<three-viewer :model-url="suit3dModel" /> \<!-- 3D组件引用 -->

&#x20;                   \</div>

&#x20;                 \</a-tab-pane>

&#x20;               \</a-tabs>

&#x20;               \<!-- 快捷操作按钮 -->

&#x20;               \<div class="agent-actions">

&#x20;                 \<a-button size="small" :style="{ color: 'var(--color-design)' }">同步至PLM\</a-button>

&#x20;                 \<a-button size="small" :style="{ color: 'var(--color-design)' }">发起局部改款\</a-button>

&#x20;               \</div>

&#x20;             \</div>

&#x20;           \</div>

&#x20;         \</div>

&#x20;       \</div>

&#x20;     \</main>

&#x20;     \<!-- 4. 右侧辅助区（任务进度） -->

&#x20;     \<aside class="right-aside" :class="{ 'collapsed': isAsideCollapsed }">

&#x20;       \<div class="aside-header">

&#x20;         \<span class="aside-title">任务进度：秋季西装设计\</span>

&#x20;         \<button class="aside-collapse-btn" @click="isAsideCollapsed = !isAsideCollapsed">

&#x20;           \<a-icon :name="isAsideCollapsed ? 'left' : 'right'" size="16" />

&#x20;         \</button>

&#x20;       \</div>

&#x20;       \<div class="aside-content" v-if="!isAsideCollapsed">

&#x20;         \<!-- 进度条 -->

&#x20;         \<a-progress percent="60" status="active" stroke-color="var(--color-design)" />

&#x20;         \<!-- 进度详情 -->

&#x20;         \<ul class="progress-list">

&#x20;           \<li class="progress-item completed">

&#x20;             \<a-icon name="check-circle" size="16" :style="{ color: 'var(--color-success)' }" />

&#x20;             \<span>趋势分析Agent：输出秋季趋势报告\</span>

&#x20;           \</li>

&#x20;           \<li class="progress-item completed">

&#x20;             \<a-icon name="check-circle" size="16" :style="{ color: 'var(--color-success)' }" />

&#x20;             \<span>款式创新Agent：生成5套设计稿\</span>

&#x20;           \</li>

&#x20;           \<li class="progress-item active">

&#x20;             \<a-icon name="loading" size="16" :style="{ color: 'var(--color-loading)' }" />

&#x20;             \<span>原料选型Agent：匹配面料（预计10分钟）\</span>

&#x20;           \</li>

&#x20;           \<li class="progress-item pending">

&#x20;             \<a-icon name="clock-circle" size="16" :style="{ color: 'var(--color-text-secondary)' }" />

&#x20;             \<span>成本分析Agent：核算生产成本\</span>

&#x20;           \</li>

&#x20;         \</ul>

&#x20;         \<!-- 关联数据预览（SCM面料库存） -->

&#x20;         \<div class="related-data">

&#x20;           \<div class="data-title">SCM面料库存预览\</div>

&#x20;           \<a-table :columns="fabricColumns" :data="fabricData" size="small" :pagination="false">

&#x20;             \<!-- 表格内容由Arco组件渲染 -->

&#x20;           \</a-table>

&#x20;         \</div>

&#x20;       \</div>

&#x20;     \</aside>

&#x20;   \</div>

&#x20;   \<!-- 5. 底部输入区（固定） -->

&#x20;   \<footer class="bottom-input-bar">

&#x20;     \<div class="input-tools">

&#x20;       \<!-- 切换模式（对话/任务） -->

&#x20;       \<button class="tool-btn active">

&#x20;         \<a-icon name="message" size="20" />

&#x20;       \</button>

&#x20;       \<!-- 上传文件 -->

&#x20;       \<button class="tool-btn">

&#x20;         \<a-icon name="upload" size="20" />

&#x20;       \</button>

&#x20;     \</div>

&#x20;     \<!-- 输入框 -->

&#x20;     \<a-input

&#x20;       v-model="inputValue"

&#x20;       placeholder="输入需求或@Agent唤醒（如：@款式创新Agent 生成秋季西装设计稿）"

&#x20;       class="main-input"

&#x20;       :style="{&#x20;

&#x20;         height: '48px',&#x20;

&#x20;         borderRadius: '24px',&#x20;

&#x20;         borderColor: 'var(--color-border)',

&#x20;         '&:focus': { borderColor: 'var(--color-primary)', boxShadow: '0 0 0 2px var(--color-border-focus)' }

&#x20;       }"

&#x20;     />

&#x20;     \<!-- 发送按钮 -->

&#x20;     \<a-button&#x20;

&#x20;       class="send-btn"&#x20;

&#x20;       :disabled="!inputValue"

&#x20;       :style="{&#x20;

&#x20;         height: '48px',&#x20;

&#x20;         width: '80px',&#x20;

&#x20;         borderRadius: '24px',&#x20;

&#x20;         backgroundColor: inputValue ? 'var(--color-primary)' : 'var(--color-bg-module)',

&#x20;         color: inputValue ? '#FFFFFF' : 'var(--color-text-disabled)'

&#x20;       }"

&#x20;     \>

&#x20;       发送

&#x20;     \</a-button>

&#x20;   \</footer>

&#x20; \</div>

\</template>

\<script setup>

import { ref } from 'vue';

import { ThreeViewer } from '@/components/3DViewer.vue'; // 引入3D组件

// 状态管理

const isNavCollapsed = ref(false); // 左侧导航折叠状态

const isAsideCollapsed = ref(true); // 右侧辅助区折叠状态

const inputValue = ref(''); // 输入框内容

const previewTab = ref('2d'); // 设计稿预览Tab

const suit3dModel = ref('@/assets/models/suit-3d.glb'); // 3D模型路径

// SCM面料库存表格数据

const fabricColumns = ref(\[

&#x20; { title: '面料名称', dataIndex: 'name', key: 'name', width: 100 },

&#x20; { title: '库存（米）', dataIndex: 'stock', key: 'stock', width: 80 },

&#x20; { title: '单价（元/米）', dataIndex: 'price', key: 'price', width: 100 },

]);

const fabricData = ref(\[

&#x20; { name: '高支羊毛', stock: 500, price: 280 },

&#x20; { name: '羊毛混纺', stock: 1200, price: 180 },

]);

\</script>

\<style scoped>

/\* 基础样式补充（仅列核心，其余用Tailwind或Arco默认） \*/

.top-status-bar {

&#x20; height: 60px;

&#x20; display: flex;

&#x20; justify-content: space-between;

&#x20; align-items: center;

&#x20; padding: 0 20px;

&#x20; border-bottom: 1px solid var(--color-border);

}

.status-icon {

&#x20; margin-left: 24px;

&#x20; color: var(--color-text-secondary);

&#x20; cursor: pointer;

}

.left-nav {

&#x20; width: 240px;

&#x20; background: var(--color-bg-module);

&#x20; border-right: 1px solid var(--color-border);

&#x20; transition: width 0.3s ease;

}

.left-nav.collapsed {

&#x20; width: 80px;

}

.nav-text {

&#x20; margin-left: 8px;

&#x20; transition: opacity 0.3s ease;

}

.left-nav.collapsed .nav-text {

&#x20; opacity: 0;

&#x20; width: 0;

&#x20; overflow: hidden;

}

.bottom-input-bar {

&#x20; height: 80px;

&#x20; display: flex;

&#x20; align-items: center;

&#x20; gap: 16px;

&#x20; padding: 0 20px;

&#x20; border-top: 1px solid var(--color-border);

}

.main-input {

&#x20; flex: 1;

}

\</style>
```

### 2.2 核心组件单独示例（高频复用）

#### （1）Agent 卡片（左侧板块导航展开后显示）



```
\<template>

&#x20; \<a-card&#x20;

&#x20;   class="agent-card"

&#x20;   :style="{&#x20;

&#x20;     height: '80px',&#x20;

&#x20;     border: '1px solid var(--color-border)',&#x20;

&#x20;     borderRadius: '8px',&#x20;

&#x20;     transition: 'all 0.3s ease',

&#x20;     '&:hover': {&#x20;

&#x20;       borderColor: 'var(--color-design)',&#x20;

&#x20;       boxShadow: '0 2px 8px rgba(0,0,0,0.08)'&#x20;

&#x20;     }

&#x20;   }"

&#x20; \>

&#x20;   \<div class="card-content" style="display: flex; align-items: center; height: 100%; padding: 0 16px;">

&#x20;     \<!-- Agent图标 -->

&#x20;     \<div class="agent-icon" :style="{&#x20;

&#x20;       width: '40px',&#x20;

&#x20;       height: '40px',&#x20;

&#x20;       borderRadius: '50%',&#x20;

&#x20;       backgroundColor: 'var(--color-design-light)',&#x20;

&#x20;       display: 'flex',&#x20;

&#x20;       align-items: 'center',&#x20;

&#x20;       justify-content: 'center',

&#x20;       marginRight: '16px'

&#x20;     }">

&#x20;       \<a-icon name="brush" size="20" :style="{ color: 'var(--color-design)' }" />

&#x20;     \</div>

&#x20;     \<!-- Agent信息 -->

&#x20;     \<div class="agent-info" style="flex: 1; overflow: hidden;">

&#x20;       \<div class="agent-name" style="font-size: 16px; font-weight: 500; color: var(--color-text-primary);">

&#x20;         款式创新Agent

&#x20;       \</div>

&#x20;       \<div class="agent-desc" style="font-size: 14px; color: var(--color-text-secondary); white-space: nowrap; overflow: hidden; text-overflow: ellipsis;">

&#x20;         生成服装新款设计稿，支持商务/休闲等风格

&#x20;       \</div>

&#x20;     \</div>

&#x20;     \<!-- 快捷操作 -->

&#x20;     \<div class="agent-actions">

&#x20;       \<!-- 唤醒按钮 -->

&#x20;       \<a-button&#x20;

&#x20;         size="small"&#x20;

&#x20;         :style="{ color: 'var(--color-primary)', backgroundColor: 'transparent' }"

&#x20;         @click="wakeAgent('款式创新Agent')"

&#x20;       \>

&#x20;         唤醒

&#x20;       \</a-button>

&#x20;       \<!-- 收藏按钮 -->

&#x20;       \<a-icon&#x20;

&#x20;         name="star-o"&#x20;

&#x20;         size="18"&#x20;

&#x20;         style="margin-left: 8px; color: var(--color-text-secondary); cursor: pointer;"

&#x20;         @click="toggleFavorite('款式创新Agent')"

&#x20;       />

&#x20;     \</div>

&#x20;   \</div>

&#x20; \</a-card>

\</template>

\<script setup>

import { ref } from 'vue';

import { useStore } from '@/stores/agentStore'; // 引入Agent状态管理

const store = useStore();

const props = defineProps({

&#x20; agent: {

&#x20;   type: Object,

&#x20;   required: true,

&#x20;   default: () => ({

&#x20;     name: '款式创新Agent',

&#x20;     desc: '生成服装新款设计稿，支持商务/休闲等风格',

&#x20;     category: '趋势与设计',

&#x20;     icon: 'brush',

&#x20;     color: 'var(--color-design)'

&#x20;   })

&#x20; }

});

// 唤醒Agent：填充输入框

const wakeAgent = (agentName) => {

&#x20; store.setInputValue(\`@\${agentName} \`);

};

// 收藏/取消收藏

const toggleFavorite = (agentName) => {

&#x20; store.toggleFavorite(agentName);

};

\</script>
```

#### （2）任务卡片（中间区任务模式）



```
\<template>

&#x20; \<div&#x20;

&#x20;   class="task-card"

&#x20;   :style="{&#x20;

&#x20;     height: '100px',&#x20;

&#x20;     border: '1px solid var(--color-border)',&#x20;

&#x20;     borderRadius: '8px',&#x20;

&#x20;     backgroundColor: 'var(--color-bg-module)',

&#x20;     padding: '16px',

&#x20;     position: 'relative',

&#x20;     marginBottom: '16px'

&#x20;   }"

&#x20; \>

&#x20;   \<!-- 状态标识线 -->

&#x20;   \<div&#x20;

&#x20;     class="task-status-line"

&#x20;     :style="{&#x20;

&#x20;       width: '4px',&#x20;

&#x20;       height: '100%',&#x20;

&#x20;       backgroundColor: getStatusColor(props.task.status),

&#x20;       position: 'absolute',

&#x20;       left: '0',

&#x20;       top: '0',

&#x20;       borderRadius: '4px 0 0 4px'

&#x20;     }"

&#x20;   \>\</div>

&#x20;   \<!-- 任务内容 -->

&#x20;   \<div class="task-content" style="padding-left: 12px;">

&#x20;     \<div class="task-top" style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 8px;">

&#x20;       \<div class="task-name" style="font-size: 16px; color: var(--color-text-primary); font-weight: 500;">

&#x20;         {{ props.task.name }}

&#x20;       \</div>

&#x20;       \<div class="task-tag" :style="{&#x20;

&#x20;         fontSize: '12px',&#x20;

&#x20;         color: getCategoryColor(props.task.category),

&#x20;         border: \`1px solid \${getCategoryColor(props.task.category)}\`,

&#x20;         borderRadius: '4px',

&#x20;         padding: '2px 8px'

&#x20;       }">

&#x20;         {{ props.task.category }}

&#x20;       \</div>

&#x20;     \</div>

&#x20;     \<div class="task-middle" style="margin-bottom: 8px;">

&#x20;       \<div class="task-desc" style="font-size: 14px; color: var(--color-text-secondary); white-space: nowrap; overflow: hidden; text-overflow: ellipsis;">

&#x20;         {{ props.task.desc }}

&#x20;       \</div>

&#x20;       \<a-progress&#x20;

&#x20;         :percent="props.task.progress"&#x20;

&#x20;         size="small"

&#x20;         :style="{&#x20;

&#x20;           height: '4px',&#x20;

&#x20;           marginTop: '4px',

&#x20;           backgroundColor: 'var(--color-border)'

&#x20;         }"

&#x20;         :stroke-color="getStatusColor(props.task.status)"

&#x20;       />

&#x20;     \</div>

&#x20;     \<div class="task-bottom" style="display: flex; justify-content: space-between; align-items: center;">

&#x20;       \<div class="task-time" style="font-size: 12px; color: var(--color-text-disabled);">

&#x20;         {{ props.task.createTime }}

&#x20;       \</div>

&#x20;       \<div class="task-actions">

&#x20;         \<a-button size="small" style="color: var(--color-primary); padding: 0 8px;">查看详情\</a-button>

&#x20;         \<a-button size="small" style="color: var(--color-text-secondary); padding: 0 8px;">取消任务\</a-button>

&#x20;       \</div>

&#x20;     \</div>

&#x20;   \</div>

&#x20; \</div>

\</template>

\<script setup>

import { computed } from 'vue';

const props = defineProps({

&#x20; task: {

&#x20;   type: Object,

&#x20;   required: true,

&#x20;   default: () => ({

&#x20;     name: '2024秋季商务西装设计',

&#x20;     desc: '生成5套设计稿，目标客群30-45岁男性高管',

&#x20;     category: '趋势与设计',

&#x20;     status: 'active', // active/completed/pending/expired

&#x20;     progress: 60,

&#x20;     createTime: '2024-10-20 14:00'

&#x20;   })

&#x20; }

});

// 根据任务状态获取颜色

const getStatusColor = computed(() => {

&#x20; const statusMap = {

&#x20;   active: 'var(--color-loading)',

&#x20;   completed: 'var(--color-success)',

&#x20;   pending: 'var(--color-text-secondary)',

&#x20;   expired: 'var(--color-error)'

&#x20; };

&#x20; return statusMap\[props.task.status] || 'var(--color-text-secondary)';

});

// 根据业务板块获取颜色

const getCategoryColor = computed(() => {

&#x20; const categoryMap = {

&#x20;   '趋势与设计': 'var(--color-design)',

&#x20;   '生产与供应链': 'var(--color-production)',

&#x20;   '营销与销售': 'var(--color-marketing)',

&#x20;   '客户服务': 'var(--color-service)',

&#x20;   '内部管理与协同': 'var(--color-management)'

&#x20; };

&#x20; return categoryMap\[props.task.category] || 'var(--color-text-secondary)';

});

\</script>
```

## 三、交互动画参数规范



| 动画场景           | 动画类型      | 时长（ms） | easing 函数   | 触发条件           | 效果描述                                     |
| -------------- | --------- | ------ | ----------- | -------------- | ---------------------------------------- |
| 左侧导航折叠 / 展开    | 宽度过渡      | 300    | ease-in-out | 点击折叠按钮         | 导航宽度从 240px 平滑过渡到 80px（反之亦然），文字渐隐 / 渐显   |
| Agent 卡片 hover | 边框 + 阴影过渡 | 200    | ease        | 鼠标移入卡片         | 边框色从 var (--color-border) 变为板块专属色，阴影从无到有 |
| 对话气泡加载         | 淡入 + 高度过渡 | 400    | ease-out    | Agent 开始回复     | 气泡从透明度 0→1，高度从 0→实际高度，避免突兀出现             |
| 右侧辅助区收起 / 展开   | 宽度过渡      | 300    | ease-in-out | 点击收起按钮         | 辅助区宽度从 320px→0（反之亦然），内容同步显隐              |
| 任务状态变更（如完成）    | 颜色 + 进度过渡 | 500    | ease        | Agent 完成任务步骤   | 进度条颜色从进行中色→成功色，进度从当前值→100%               |
| 输入框聚焦 / 失焦     | 边框 + 阴影过渡 | 200    | ease        | 点击输入框 / 点击其他区域 | 聚焦时边框色变主色 + 显示聚焦阴影，失焦时恢复默认               |
| 板块切换（中间区内容）    | 淡入淡出      | 300    | ease-in-out | 点击左侧不同板块导航     | 原板块内容透明度 0→1 隐藏，新板块内容透明度 0→1 显示          |
| 3D 模型加载        | 旋转 + 淡入   | 800    | ease-out    | 切换到 3D 预览 Tab  | 模型从透明旋转状态→清晰静止状态，提升加载感知                  |

## 四、响应式适配落地规则



| 设备尺寸              | 布局调整规则                                      | 组件适配细节                                                          |
| ----------------- | ------------------------------------------- | --------------------------------------------------------------- |
| PC 端（≥1200px）     | 完整显示 “顶部 + 左侧 + 中间 + 右侧 + 底部” 五区域           | 所有组件正常显示，3D 预览区宽度 200px，Agent 卡片一行显示 2 个                        |
| 平板端（768px-1199px） | 右侧辅助区默认收起（点击展开后覆盖中间区 30% 宽度），左侧导航保持可折叠      | 3D 预览区宽度 160px，Agent 卡片一行显示 1 个，底部输入区工具按钮仅保留图标（隐藏文字）            |
| 移动端（≤767px）       | 左侧导航改为底部 Tab 栏（高度 60px），右侧辅助区隐藏（从任务详情页进入查看） | 3D 预览区宽度 100%（独占一行），输入框 placeholder 简化为 “@Agent 或输入需求”，任务卡片全屏宽度 |

### 移动端底部 Tab 栏 HTML 示例



```
\<template>

&#x20; \<div class="mobile-tab-bar" style="height: 60px; border-top: 1px solid var(--color-border); display: flex; align-items: center; background: var(--color-bg-module);">

&#x20;   \<div class="tab-item" :class="{ active: currentTab === 'design' }" @click="currentTab = 'design'">

&#x20;     \<a-icon name="palette" size="24" :style="{ color: currentTab === 'design' ? 'var(--color-design)' : 'var(--color-text-secondary)' }" />

&#x20;     \<div class="tab-text" style="font-size: 12px; margin-top: 4px; color: inherit;">设计\</div>

&#x20;   \</div>

&#x20;   \<div class="tab-item" :class="{ active: currentTab === 'production' }" @click="currentTab = 'production'">

&#x20;     \<a-icon name="factory" size="24" :style="{ color: currentTab === 'production' ? 'var(--color-production)' : 'var(--color-text-secondary)' }" />

&#x20;     \<div class="tab-text" style="font-size: 12px; margin-top: 4px; color: inherit;">生产\</div>

&#x20;   \</div>

&#x20;   \<div class="tab-item" :class="{ active: currentTab === 'marketing' }" @click="currentTab = 'marketing'">

&#x20;     \<a-icon name="shopping-cart" size="24" :style="{ color: currentTab === 'marketing' ? 'var(--color-marketing)' : 'var(--color-text-secondary)' }" />

&#x20;     \<div class="tab-text" style="font-size: 12px; margin-top: 4px; color: inherit;">营销\</div>

&#x20;   \</div>

&#x20;   \<div class="tab-item" :class="{ active: currentTab === 'service' }" @click="currentTab = 'service'">

&#x20;     \<a-icon name="headset" size="24" :style="{ color: currentTab === 'service' ? 'var(--color-service)' : 'var(--color-text-secondary)' }" />

&#x20;     \<div class="tab-text" style="font-size: 12px; margin-top: 4px; color: inherit;">客服\</div>

&#x20;   \</div>

&#x20;   \<div class="tab-item" :class="{ active: currentTab === 'management' }" @click="currentTab = 'management'">

&#x20;     \<a-icon name="users" size="24" :style="{ color: currentTab === 'management' ? 'var(--color-management)' : 'var(--color-text-secondary)' }" />

&#x20;     \<div class="tab-text" style="font-size: 12px; margin-top: 4px; color: inherit;">管理\</div>

&#x20;   \</div>

&#x20; \</div>

\</template>

\<script setup>

import { ref } from 'vue';

const currentTab = ref('design'); // 当前选中的Tab

\</script>

\<style scoped>

.tab-item {

&#x20; flex: 1;

&#x20; display: flex;

&#x20; flex-direction: column;

&#x20; align-items: center;

&#x20; justify-content: center;

}

.tab-item.active {

&#x20; color: var(--color-primary);

}

\</style>
```

> （注：文档部分内容可能由 AI 生成）