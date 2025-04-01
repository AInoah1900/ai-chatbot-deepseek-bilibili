# DeepSeek AI 聊天应用

基于DeepSeek大模型API的聊天应用，提供类似ChatGPT的交互体验。用户可以创建多个聊天会话，选择不同的模型进行对话，并查看历史聊天记录。

![DeepSeek AI Chat](https://example.com/screenshot.png)

## 主要功能

- **模型选择**：支持deepseek-v3和deepseek-r1两种大语言模型
- **多会话管理**：创建和管理多个独立的聊天会话
- **历史记录**：保存所有聊天历史，方便随时查看
- **用户认证**：基于Clerk的用户认证和授权系统
- **实时对话**：流式响应，实时获取AI回复
- **响应式设计**：适配各种屏幕尺寸的现代UI界面

## 技术栈

### 前端
- **框架**: [Next.js 15](https://nextjs.org/)
- **UI组件**: [Material UI](https://mui.com/)
- **样式**: [Tailwind CSS](https://tailwindcss.com/)
- **数据获取**: [TanStack Query](https://tanstack.com/query)
- **HTTP客户端**: [Axios](https://axios-http.com/)

### 后端
- **API路由**: Next.js App Router API Routes
- **认证**: [Clerk](https://clerk.com/)
- **数据库**: [PostgreSQL](https://www.postgresql.org/) (Supabase)
- **ORM**: [Drizzle ORM](https://orm.drizzle.team/)
- **AI集成**: [AI SDK](https://sdk.vercel.ai/docs) (@ai-sdk/deepseek)

## 快速开始

### 前提条件
- Node.js 18+ 
- PostgreSQL数据库 (推荐使用Supabase)
- DeepSeek API密钥
- Clerk账户

### 安装步骤

1. **克隆代码库**
   ```bash
   git clone https://github.com/yourusername/ai-chatbot-deepseek-bilibili.git
   cd ai-chatbot-deepseek-bilibili
   ```

2. **安装依赖**
   ```bash
   npm install
   ```

3. **配置环境变量**
   创建`.env`文件，参考以下模板：
   ```
   # Clerk认证
   NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
   CLERK_SECRET_KEY=your_clerk_secret_key
   NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
   
   # DeepSeek API
   DEEPSEEK_API_KEY=your_deepseek_api_key
   BASE_URL=https://dashscope.aliyuncs.com/compatible-mode/v1
   
   # 数据库连接
   DATABASE_URL=postgresql://postgres:password@aws-0-region.pooler.supabase.com:6543/postgres
   ```

4. **初始化数据库**
   ```bash
   npx drizzle-kit push
   ```

5. **启动开发服务器**
   ```bash
   npm run dev
   ```

6. **访问应用**
   打开浏览器访问 [http://localhost:3000](http://localhost:3000)

## 项目结构

```
├── src/
│   ├── app/                # Next.js App Router
│   │   ├── api/            # API路由
│   │   ├── chat/           # 聊天界面
│   │   ├── sign-in/        # 登录页面
│   │   ├── page.tsx        # 首页
│   │   └── layout.tsx      # 全局布局
│   ├── components/         # React组件
│   └── db/                 # 数据库相关
│       ├── index.ts        # 数据库操作
│       └── schema.ts       # 数据库模型
├── drizzle.config.ts       # Drizzle ORM配置
├── postcss.config.mjs      # PostCSS配置
├── tailwind.config.js      # Tailwind CSS配置
└── next.config.js          # Next.js配置
```

## 数据库模型

项目使用两个主要数据表:

1. **chats** - 存储聊天会话
   - `id`: 自增主键
   - `userId`: 用户ID (来自Clerk)
   - `title`: 聊天标题
   - `model`: 使用的模型类型 (deepseek-v3 或 deepseek-r1)

2. **messages** - 存储消息
   - `id`: 自增主键
   - `chatId`: 关联的聊天ID
   - `role`: 消息角色 (user 或 assistant)
   - `content`: 消息内容

## API端点

- `POST /api/create-chat`: 创建新聊天
- `POST /api/get-chats`: 获取用户所有聊天
- `POST /api/get-chat`: 获取单个聊天详情
- `POST /api/get-messages`: 获取聊天消息
- `POST /api/chat`: 与AI模型交互

## 部署

### Vercel部署

1. Fork该项目到您的GitHub账户
2. 在Vercel中导入项目
3. 配置环境变量
4. 点击部署

### 自托管
```bash
npm run build
npm start
```

## 问题排查

- **数据库连接问题**: 确保DATABASE_URL配置正确
- **验证错误**: 检查Clerk密钥是否正确配置
- **DeepSeek API错误**: 验证API密钥和BASE_URL设置

## 贡献指南

1. Fork项目
2. 创建功能分支 (`git checkout -b feature/amazing-feature`)
3. 提交更改 (`git commit -m 'Add some amazing feature'`)
4. 推送到分支 (`git push origin feature/amazing-feature`)
5. 开启Pull Request

## 许可证

MIT
