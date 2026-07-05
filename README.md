# CopyMind — AI 文案智能分析工具

一键分析营销文案的小程序 + 后端工具。支持小红书种草、电商商品、本地文旅、短视频脚本 4 个赛道，基于规则引擎做多维度评分和优化建议，无需 AI API Key 即可离线体验。

---

## 项目结构

```
├── backend/              # FastAPI 后端服务（Python 3.11+）
│   ├── app/
│   │   ├── routers/      # API 路由（分析、历史、反馈、OCR）
│   │   ├── services/
│   │   │   └── analysis/ # 规则驱动文案分析引擎（情绪词库 + 结构评分）
│   │   ├── models/       # SQLAlchemy 数据模型
│   │   ├── schemas/      # Pydantic 请求/响应模型
│   │   └── middleware/   # 限流、请求日志中间件
│   ├── tests/
│   └── main.py
├── miniapp/              # 微信小程序前端（原生 WXML + WXSS + JS）
│   ├── pages/
│   │   ├── index/        # 首页（文案录入 + 赛道选择）
│   │   ├── result/       # 分析结果（4 维评分 + 优化建议）
│   │   └── history/      # 历史记录
│   └── app.js / app.json
├── database/             # MySQL 建表脚本
└── docs/                 # 项目文档
```

---

## 快速开始

### 1. 启动后端

```bash
cd backend
pip install fastapi uvicorn sqlalchemy aiosqlite pydantic pydantic-settings httpx python-multipart
uvicorn main:app --reload --port 8000
```

默认使用 SQLite，开箱即用无需配置数据库。如需 MySQL，配置 `.env` 后会自动切换。

### 2. 运行小程序

用微信开发者工具打开 `miniapp/` 目录，勾选 **"不校验合法域名"**，编译即可直连本地后端。

---

## 分析维度

| 维度 | 说明 |
|------|------|
| 📝 标题吸引力 | 检测标题长度、数字、问句、emoji、钩子词 |
| 💬 情绪共鸣 | 情绪词库匹配（正向/共情/焦虑/信任词） |
| 📐 结构逻辑 | 段落数、句式变化、行动号召（CTA）检测 |
| 👥 人群匹配 | 赛道关键词、受众定位词、内容长度适配 |

每条分析附带 10 条优化建议（含标题改写、段落调整、情绪词建议）。

---

## API 接口

| 方法 | 路径 | 说明 |
|------|------|------|
| POST | `/api/v1/analyze` | 提交文案，返回评分 + 优化建议 |
| GET  | `/api/v1/history` | 历史记录 |
| POST | `/api/v1/feedback` | 提交反馈 |
| GET  | `/api/v1/health` | 健康检查 |

---

## 技术栈

- **前端**：微信小程序原生（WXML + WXSS + JS）
- **后端**：Python FastAPI + Uvicorn + SQLAlchemy
- **分析引擎**：规则驱动（情绪词库 + 结构评分），离线可用
- **数据库**：SQLite（默认）/ MySQL 8.0（可选）

---

## License

MIT
