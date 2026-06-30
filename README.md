# Grok Imagine 视频生成工具

这是一个基于 AnyAIGC 的 Grok Imagine 视频生成单页工具。项目只有一个 `index.html`，可以直接在浏览器中打开使用，用于提交视频生成/编辑任务、自动查询任务进度，并预览或复制生成结果。

## AnyAIGC 信息

AnyAIGC 是面向开发者和 AI 应用构建者的 API 服务平台，提供统一的 AI 模型 API 调用入口，方便在一个平台中接入不同模型能力。

官网地址：

```text
https://anyaigc.com
```

本页面默认使用的 API Base URL 也是：

```text
https://anyaigc.com
```

使用前需要准备 AnyAIGC API Key，并在页面的 `API Key` 输入框中填写。

## 页面功能介绍

### 创建视频

在“创建视频”模式下，页面会调用视频生成接口，根据提示词和参数创建 Grok Imagine 视频任务。

支持配置：

- 模型：`grok-imagine-video`、`grok-imagine-video-1.5-preview`
- 分辨率：`480p`、`720p`
- 画幅：`16:9`、`9:16`、`1:1`
- 时长：1 到 15 秒
- 提示词
- 首帧图片 URL
- 多张参考图片 URL

### 编辑视频

在“编辑视频”模式下，页面会调用视频编辑接口，基于原视频 URL 和提示词提交编辑任务。

编辑模式下会显示“原视频 URL”输入项，并隐藏不适用于编辑的生成参数。

### 图片上传

页面支持选择本地图片并上传：

- 首帧图片：上传后自动回填到“首帧图片 URL”
- 参考图片：支持多图上传，上传后的 URL 会追加到“参考图片 URL”

注意：`image` 和 `reference_images` 不能同时使用。

### 自动轮询任务进度

提交任务成功后，页面会自动读取返回的 `request_id`，并开始轮询任务结果。

用户不需要手动点击“查询进度”。任务完成后，页面会自动更新状态、视频预览、结果链接和 JSON 响应。

### 结果展示

右侧结果区域包含：

- 视频预览
- 当前模式
- 任务状态
- 结果链接列表
- 原始 JSON 响应

结果链接支持：

- 新页面打开
- 复制链接

JSON 响应支持一键复制。

### 本地缓存

页面会把常用配置保存到浏览器 `localStorage`：

- API Key
- 模式
- 模型
- 分辨率
- 画幅
- 时长
- 图片 URL
- 参考图片 URL
- 原视频 URL

点击“清除密钥”可以删除本地保存的 API Key。

## 使用的接口

当前页面直接请求 AnyAIGC API：

```text
POST https://anyaigc.com/v1/videos/generations
POST https://anyaigc.com/v1/videos/edits
GET  https://anyaigc.com/v1/videos/{request_id}
```

其中：

- `generations` 用于创建视频任务
- `edits` 用于编辑视频任务
- `GET /v1/videos/{request_id}` 用于查询任务进度和结果

## 使用方式

1. 打开 `index.html`
2. 填写 AnyAIGC API Key
3. 选择“创建视频”或“编辑视频”
4. 填写提示词和所需参数
5. 如需图片输入，先选择本地图片并点击上传
6. 点击“提交任务”
7. 等待页面自动轮询并展示结果

## 项目结构

```text
.
├── index.html   # 单页应用，包含页面、样式和请求逻辑
└── README.md    # 项目说明
```
