# 规范文档模板

> 本文件提供各类规范文档的模板结构。`project-harness-builder` skill 生成规范时读取此文件。
>
> 占位符说明：
> - `{{PROJECT_NAME}}` — 项目名称
> - `{{PROJECT_DESC}}` — 项目描述
> - `{{FRONTEND_FRAMEWORK}}` — 前端框架
> - `{{BACKEND_FRAMEWORK}}` — 后端框架
> - `{{DATABASE}}` — 数据库
> - `{{STATE_MGMT}}` — 状态管理方案
> - `{{ROUTER}}` — 路由方案
> - `{{HTTP_CLIENT}}` — HTTP 客户端
> - `{{ORM}}` — ORM/数据库访问层
> - `{{AUTH_METHOD}}` — 认证方式
> - `{{DEPLOY_TARGET}}` — 部署目标
> - `{{DATE}}` — 当前日期
>
> **设计偏好占位符**（来自 Round 3 问答，仅用于 design-tokens.md / layout-principles.md / animation-spec.md）：
> - `{{THEME_MODE}}` — 主题模式：仅浅色 / 仅深色 / 浅色+深色双主题 / 跟随系统
> - `{{BRAND_COLOR}}` — 品牌主色系：蓝色系 / 绿色系 / 紫色系 / 橙色系 / 红色系 / 自定义（含色值）
> - `{{BRAND_COLOR_HEX}}` — 品牌主色 HEX 值（如 #2563EB）
> - `{{VISUAL_STYLE}}` — 视觉风格：极简主义 / Material Design / 拟物新拟态 / 玻璃拟态 / Bento Grid / 粗犷主义
> - `{{LAYOUT_DENSITY}}` — 排版密度：紧凑 / 舒适 / 宽松
> - `{{FONT_PREFERENCE}}` — 字体偏好：无衬线 / 衬线+无衬线混搭 / 等宽强调 / 自定义
> - `{{ANIMATION_STYLE}}` — 动效风格：极简动效 / 适度微交互 / 丰富动效 / 沉浸动效
> - `{{CORNER_RADIUS}}` — 圆角偏好：锐利 / 适中 / 圆润 / 药丸形
> - `{{BRAND_GUIDELINES}}` — 现有品牌规范（如有，含 Logo 位置、品牌色、字体、视觉禁忌）
> - `{{DESIGN_REFERENCES}}` — 设计参考（链接或描述，skill 可用 WebFetch 分析）
>
> **工程偏好占位符**（来自 Round 6/7 问答，用于 frontend/backend/api/database/security-spec.md）：
> - `{{FE_NAMING}}` — 前端命名规范：kebab-case+PascalCase / snake_case+PascalCase / camelCase+PascalCase
> - `{{FE_COMPONENT_GRANULARITY}}` — 组件粒度：原子化 / 功能化 / 领域化
> - `{{FE_STATE_MGMT_DETAIL}}` — 状态管理细节（开放问题答案）
> - `{{FE_PERF_STRATEGY}}` — 前端性能策略：代码分割 / 预加载 / SSR/SSG / 无特殊
> - `{{BE_LAYERING}}` — 后端分层架构：三层 / 四层 / DDD / 六边形
> - `{{BE_LOGGING}}` — 后端日志方案：结构化JSON / 纯文本 / ELK/Loki
> - `{{BE_ERROR_HANDLING}}` — 后端错误处理：统一错误类 / 每层try-catch / Result模式
> - `{{API_RESPONSE_FORMAT}}` — API 响应格式：包裹式 / RESTful原生 / GraphQL / 混合
> - `{{API_VERSIONING}}` — API 版本策略：URL路径 / Header / 查询参数 / 无版本
> - `{{API_AUTH_METHOD}}` — API 认证方式：JWT / Session+Cookie / OAuth2.0 / API Key / 无
> - `{{API_DOC_TOOL}}` — API 文档方案：OpenAPI/Swagger / 手写Markdown / TypeDoc / 暂不需要
> - `{{DB_NAMING}}` — 数据库命名规范：snake_case / camelCase / PascalCase
> - `{{DB_PRIMARY_KEY}}` — 主键策略：自增整数 / UUID v4 / UUID v7/ULID / 雪花算法
> - `{{DB_SOFT_DELETE}}` — 软删除策略：软删除 / 硬删除 / 混合
> - `{{DB_TIMESTAMP}}` — 时间戳策略：UTC+TIMESTAMPTZ / 本地时区+TIMESTAMP / Unix毫秒
> - `{{DB_MIGRATION}}` — 迁移管理：ORM内置 / 手写SQL / 已有工具
> - `{{SEC_PASSWORD_HASH}}` — 密码加密：bcrypt / argon2id / scrypt
> - `{{SEC_TOKEN_STORAGE}}` — Token 存储：HttpOnly Cookie / localStorage / 内存+Refresh Cookie
> - `{{SEC_CORS}}` — CORS 策略：白名单 / 同源 / 特定方法头
> - `{{SEC_RATE_LIMIT}}` — 限流策略：分级限流 / 全局统一 / 按用户 / 暂不限
> - `{{SEC_AUDIT_LOG}}` — 审计日志：所有写操作 / 仅敏感操作 / 不记录
> - `{{SEC_DATA_MASKING}}` — 敏感数据脱敏：自动脱敏 / 仅日志脱敏 / 不脱敏
>
> **质量运维占位符**（来自 Round 8 问答，用于 testing/cicd/deployment/performance-spec.md）：
> - `{{TEST_COVERAGE}}` — 测试覆盖率要求：严格 / 标准 / 宽松
> - `{{TEST_E2E_TOOL}}` — E2E 测试方案：Playwright / Cypress / Selenium / 暂不需要
> - `{{TEST_DATA_MGMT}}` — 测试数据管理：Factory+事务回滚 / 固定种子 / Mock
> - `{{CICD_PLATFORM}}` — CI/CD 平台：GitHub Actions / GitLab CI / Jenkins / 暂不需要
> - `{{CICD_TRIGGER}}` — 部署触发方式：main push / Tag手动 / PR合并 / 仅手动
> - `{{CICD_ARTIFACT}}` — 制品管理：Docker镜像 / 静态产物+CDN / 源码直接
> - `{{DEPLOY_ENVIRONMENTS}}` — 环境划分（多选）：local / development / staging / production
> - `{{DEPLOY_STRATEGY}}` — 部署策略：滚动 / 蓝绿 / 金丝雀 / 直接替换
> - `{{DEPLOY_ROLLBACK}}` — 回滚策略：自动 / 手动 / 保留N版本
> - `{{PERF_BUDGET_STRICTNESS}}` — 性能预算严格度：严格 / 标准 / 宽松
> - `{{PERF_MONITORING}}` — 性能监控方案（多选）：前端RUM / 后端APM / 合成监控 / 暂不
> - `{{PERF_TESTING}}` — 性能测试方案：Lighthouse CI / k6 / 两者都要 / 暂不需要

---

## 1. TECH-STACK.md 模板

```markdown
# {{PROJECT_NAME}} — 技术栈总览

> 本文件是 {{PROJECT_NAME}} 技术栈的唯一权威来源。所有技术选型以此文件为准。
> 最后更新：{{DATE}}

## 架构

{{根据项目类型生成架构图，例如：}}

{{PROJECT_NAME}} 采用 {{N}} 端架构：

| 端 | 技术 | 职责 |
|----|------|------|
| 前端 | {{FRONTEND_FRAMEWORK}} | 用户界面 |
| 后端 | {{BACKEND_FRAMEWORK}} | API 服务 |
| 数据库 | {{DATABASE}} | 数据持久化 |

## 依赖版本约束

### 前端
| 依赖 | 版本 | 用途 |
|------|------|------|
| {{FRONTEND_FRAMEWORK}} | {{VERSION}} | UI 框架 |
| {{STATE_MGMT}} | {{VERSION}} | 状态管理 |
| {{ROUTER}} | {{VERSION}} | 路由 |
| {{HTTP_CLIENT}} | {{VERSION}} | HTTP 客户端 |

### 后端
| 依赖 | 版本 | 用途 |
|------|------|------|
| {{BACKEND_FRAMEWORK}} | {{VERSION}} | Web 框架 |
| {{ORM}} | {{VERSION}} | ORM |
| {{AUTH_METHOD}} | {{VERSION}} | 认证 |

## 工具链位置

{{根据实际环境填写}}

## 环境约束

{{根据实际约束填写}}
```

---

## 2. CONTEXT.md 模板

```markdown
# {{PROJECT_NAME}} — 领域语言

> 本文件定义 {{PROJECT_NAME}} 的领域术语。所有文档和代码必须使用本文档中的术语。

## 项目边界

{{PROJECT_NAME}} 是 {{PROJECT_DESC}}。

## 核心术语

| 术语 | 英文 | 定义 |
|------|------|------|
| {{术语1}} | {{Term1}} | {{定义}} |
| {{术语2}} | {{Term2}} | {{定义}} |

## 通用语言规则

- 使用本文档定义的术语，禁止自造词汇
- 代码中的类名、变量名使用英文对应词
- 文档和 UI 文案使用中文术语
```

---

## 3. spec.md 模板

```markdown
# {{PROJECT_NAME}} — 功能规格文档

> 版本：1.0 | 最后更新：{{DATE}}

## 1. 项目概述

{{PROJECT_DESC}}

### 目标用户

{{目标用户描述}}

### 核心价值

{{核心价值描述}}

## 2. 功能列表

| 功能 | 优先级 | 状态 | 说明 |
|------|--------|------|------|
| {{功能1}} | P0 | 待开发 | {{说明}} |
| {{功能2}} | P1 | 待开发 | {{说明}} |

## 3. 技术栈

详见 `docs/TECH-STACK.md`。

## 4. 目录结构

{{根据技术栈生成目录结构}}

## 5. 用户流程

{{核心用户流程描述}}
```

---

## 4. secrets-management.md 模板

```markdown
# {{PROJECT_NAME}} — 敏感信息管理规范

> 最后更新：{{DATE}}

## 1. 核心原则

| 原则 | 说明 |
|------|------|
| **前端无密钥** | {{如有前端}}前端代码可被用户查看，任何硬编码值都可被提取 |
| **密钥在后端** | 所有密钥只存在于后端 .env |
| **.env 不入库** | .env 文件永远不提交 Git，只提交 .env.example |
| **启动校验** | 后端启动时校验所有必需环境变量 |

## 2. 密钥分布

{{根据架构生成密钥分布图}}

## 3. 各端配置方式

### 前端（{{FRONTEND_FRAMEWORK}}）
{{根据前端框架生成环境变量注入方式}}

### 后端（{{BACKEND_FRAMEWORK}}）
{{根据后端框架生成 .env 加载和校验方式}}

## 4. 密钥轮换

| 密钥类型 | 轮换周期 | 轮换方式 |
|----------|----------|----------|
| {{密钥类型}} | {{周期}} | {{方式}} |

## 5. 泄露应急流程

1. 立即吊销泄露的密钥
2. 生成新密钥并更新所有环境
3. 检查日志确认未被滥用
4. 通知团队成员
5. 复盘泄露原因
```

---

## 5. frontend-spec.md 模板

```markdown
# {{PROJECT_NAME}} — 前端代码规范

> 所有前端代码开发**必须**遵循本规范。
> 最后更新：{{DATE}}

## 0. 工程定位

| 维度 | 选择 | 说明 |
|------|------|------|
| 命名规范 | {{FE_NAMING}} | {{根据选择说明：kebab-case+PascalCase 适合 React/Vue；snake_case+PascalCase 适合 Flutter/Dart}} |
| 组件粒度 | {{FE_COMPONENT_GRANULARITY}} | {{根据粒度说明目录结构：原子化=atoms/molecules/organisms；功能化=pages/components/layouts；领域化=按业务领域分组}} |
| 状态管理 | {{FE_STATE_MGMT_DETAIL}} | {{根据用户回答生成具体状态管理规范}} |
| 性能策略 | {{FE_PERF_STRATEGY}} | {{根据策略说明：代码分割=路由级懒加载；预加载=关键路由 prefetch；SSR/SSG=服务端渲染}} |

## 1. 技术栈

| 类别 | 选择 | 版本 |
|------|------|------|
| 框架 | {{FRONTEND_FRAMEWORK}} | {{VERSION}} |
| 状态管理 | {{STATE_MGMT}} | {{VERSION}} |
| 路由 | {{ROUTER}} | {{VERSION}} |
| HTTP | {{HTTP_CLIENT}} | {{VERSION}} |

## 2. 命名规范（{{FE_NAMING}}）

{{根据 FE_NAMING 生成命名规范表。例如 kebab-case+PascalCase：}}

| 对象 | 规则 | 示例 |
|------|------|------|
| 文件名 | kebab-case | user-profile.tsx / user-profile.vue |
| 组件文件名 | PascalCase | UserProfile.tsx |
| 类名 | PascalCase | UserService |
| 函数/方法 | camelCase | getUserById |
| 变量 | camelCase | userId |
| 常量 | UPPER_SNAKE_CASE | MAX_RETRY |
| 组件 | PascalCase | <UserProfile /> |
| CSS 类 | kebab-case | .user-profile-card |
| Hook/Composable | use + camelCase | useUser / useUserStore |

{{如 FE_NAMING 为 snake_case+PascalCase（Flutter/Dart）：}}

| 对象 | 规则 | 示例 |
|------|------|------|
| 文件名 | snake_case | user_profile.dart |
| 类名 | PascalCase | UserProfile |
| 函数/方法 | camelCase | getUserById |
| 变量 | camelCase | userId |
| 常量 | lowerCamelCase | maxRetry |
| 组件 | PascalCase | UserProfile widget |

## 3. 组件规范（{{FE_COMPONENT_GRANULARITY}} 粒度）

{{根据 FE_COMPONENT_GRANULARITY 生成组件规范和目录结构：}}

### 原子化（Atomic Design）
```
components/
├── atoms/          # 最小单元（按钮、输入框、标签）
├── molecules/      # 原子组合（搜索框=输入框+按钮）
├── organisms/      # 复杂组件（导航栏、卡片列表）
└── templates/      # 页面骨架
```

### 功能化（推荐，简单实用）
```
components/         # 可复用组件
layouts/            # 布局组件
pages/              # 页面组件
```

### 领域化（大型项目）
```
features/
├── user/           # 用户领域
│   ├── components/
│   ├── hooks/
│   └── api/
├── order/          # 订单领域
└── shared/         # 跨领域共享
```

| 规则 | 说明 |
|------|------|
| 单一职责 | 一个组件只做一件事 |
| 不可变优先 | {{根据框架}} |
| 分离 UI 与逻辑 | UI 组件只做渲染，业务逻辑在 Service/Store 层 |
| 设计令牌引用 | 禁止硬编码颜色/字号/间距 |

## 4. 状态管理规范（{{FE_STATE_MGMT_DETAIL}}）

{{根据 FE_STATE_MGMT_DETAIL 开放问题答案生成具体规范。常见模式：}}

- **全局 store**：用户信息、主题、语言等全局状态
- **服务端状态缓存**：用 React Query/SWR/Riverpod AsyncValue 管理服务端数据，避免手动管理 loading/error
- **局部状态**：表单、UI 开关等用组件局部状态
- **状态持久化**：需要持久化的状态（如主题、token）用 localStorage/SharedPreferences

## 5. 性能策略（{{FE_PERF_STRATEGY}}）

{{根据 FE_PERF_STRATEGY 生成性能规范：}}

- **代码分割 + 懒加载**：路由级 lazy import，组件按需加载
- **预加载关键路由**：首屏加载后 prefetch 用户大概率访问的路由
- **SSR/SSG**：如框架支持，首屏用 SSR/SSG 提升首屏性能和 SEO
- **无特殊要求**：遵循性能规范文档即可

## 6. 目录结构

{{根据 FE_COMPONENT_GRANULARITY 和框架生成标准目录结构}}

## 7. 运行命令

{{根据框架生成开发/构建/测试命令}}
```

---

## 6. backend-spec.md 模板

```markdown
# {{PROJECT_NAME}} — 后端代码规范

> 所有后端代码开发**必须**遵循本规范。
> 最后更新：{{DATE}}

## 0. 工程定位

| 维度 | 选择 | 说明 |
|------|------|------|
| 分层架构 | {{BE_LAYERING}} | {{根据架构说明：三层=Route/Service/Model；四层=加 Repository；DDD=Domain/Application/Infrastructure；六边形=端口与适配器}} |
| 日志方案 | {{BE_LOGGING}} | {{根据方案说明：结构化JSON=pino/winston/zap；纯文本=简单但难检索；ELK/Loki=集中式日志}} |
| 错误处理 | {{BE_ERROR_HANDLING}} | {{根据策略说明：统一错误类+全局中间件=推荐；每层try-catch=冗余；Result模式=函数式}} |

## 1. 技术栈

| 类别 | 选择 | 理由 |
|------|------|------|
| 运行时 | {{RUNTIME}} | {{理由}} |
| 框架 | {{BACKEND_FRAMEWORK}} | {{理由}} |
| 数据库 | {{DATABASE}} | {{理由}} |
| ORM | {{ORM}} | {{理由}} |
| 认证 | {{AUTH_METHOD}} | {{理由}} |
| 参数校验 | {{VALIDATION_LIB}} | {{理由}} |

## 2. 分层架构（{{BE_LAYERING}}）

{{根据 BE_LAYERING 生成架构图。例如三层：}}

```
Route (路由层) → 参数校验、认证、响应格式化
  ↓ 只调用 Service
Service (业务层) → 业务逻辑、事务、数据组装
  ↓ 只调用 Model
Model (数据层) → 数据库操作
```

{{如 BE_LAYERING 为四层：}}

```
Route (路由层) → 参数校验、认证、响应格式化
  ↓ 只调用 Service
Service (业务层) → 业务逻辑、事务编排
  ↓ 只调用 Repository
Repository (数据访问层) → 数据库操作、查询封装
  ↓ 只调用 Model
Model (数据层) → 实体定义
```

{{如 BE_LAYERING 为 DDD：}}

```
Interface (接口层) → Controller、Route、DTO
  ↓
Application (应用层) → 用例编排、事务
  ↓
Domain (领域层) → 实体、值对象、领域服务
  ↓
Infrastructure (基础设施层) → Repository 实现、外部服务
```

**禁止跨层调用。**

## 3. 目录结构

{{根据 BE_LAYERING 和框架生成目录结构}}

## 4. 错误处理（{{BE_ERROR_HANDLING}}）

{{根据 BE_ERROR_HANDLING 生成错误处理规范：}}

### 统一错误类 + 全局异常中间件（推荐）
- Service 层抛出统一错误类（如 AppError）
- 全局异常中间件捕获所有未处理错误，转为标准响应
- 禁止向客户端暴露堆栈信息
- 错误类包含：code、message、httpStatus、details

### 每层 try/catch
- 每层自行捕获和处理错误
- 注意：容易导致错误处理代码重复

### Result/Either 模式（函数式）
- 函数返回 Result<T, E> 而非抛异常
- 调用方必须显式处理错误
- 适合函数式语言/风格

## 5. 日志规范（{{BE_LOGGING}}）

{{根据 BE_LOGGING 生成日志规范：}}

| 规则 | 说明 |
|------|------|
| 结构化日志 | {{如 JSON：每条日志含 level/timestamp/msg/requestId 等字段}} |
| 禁止 console.log | 使用框架 logger |
| 敏感数据 | 密码、Token 不落日志 |
| 请求追踪 | 每个请求分配 requestId，贯穿全链路 |
| 日志级别 | error > warn > info > debug，生产环境只输出 info+ |

## 6. 环境变量

- 所有敏感配置走 .env
- .env.example 列出所有必需变量
- 启动时校验，缺失必需变量直接报错退出

## 7. 安全相关

| 规则 | 说明 |
|------|------|
| 密码 | {{SEC_PASSWORD_HASH}} 加密 |
| {{AUTH_METHOD}} | {{具体配置}} |
| 限流 | 见 security-spec.md |
| SQL 注入 | {{ORM}} 参数化查询 |
```

---

## 7. api-spec.md 模板

```markdown
# {{PROJECT_NAME}} — API 设计规范

> 所有后端 API 开发**必须**遵循本规范。
> 最后更新：{{DATE}}

## 0. 工程定位

| 维度 | 选择 | 说明 |
|------|------|------|
| 响应格式 | {{API_RESPONSE_FORMAT}} | {{根据格式说明：包裹式=统一 code/message/data；RESTful原生=HTTP状态码+数据；GraphQL=Schema驱动；混合=列表包裹详情原生}} |
| 版本策略 | {{API_VERSIONING}} | {{根据策略说明：URL路径=/api/v1/；Header=Accept头；查询参数=?version=1；无版本=小项目}} |
| 认证方式 | {{API_AUTH_METHOD}} | {{根据方式说明：JWT=无状态；Session=有状态；OAuth2.0=第三方；API Key=内部；无=公开}} |
| 文档方案 | {{API_DOC_TOOL}} | {{根据方案说明：OpenAPI=自动生成交互文档；手写MD=简单；TypeDoc=类型推导；暂不需要}} |

## 1. URL 规范

| 规则 | 示例 |
|------|------|
| 基础路径 /api/v1 | /api/v1/{{resource}}（{{API_VERSIONING}} 为 URL 路径版本时） |
| 资源用复数名词 | /users、/scores |
| 嵌套资源最多 2 层 | /users/:id/scores |
| 查询参数用 camelCase | ?pageSize=10 |
| 路径参数用 kebab-case | /leader-boards |

## 2. 请求/响应格式（{{API_RESPONSE_FORMAT}}）

{{根据 API_RESPONSE_FORMAT 生成响应格式规范：}}

### 包裹式（{ code, message, data }）

成功响应：
```json
{
  "code": 0,
  "message": "success",
  "data": { ... }
}
```

列表响应：
```json
{
  "code": 0,
  "message": "success",
  "data": {
    "items": [...],
    "total": 100,
    "page": 1,
    "pageSize": 20
  }
}
```

错误响应：
```json
{
  "code": 40001,
  "message": "Invalid format",
  "data": null
}
```

### RESTful 原生
- 成功：HTTP 2xx + 数据体
- 错误：HTTP 4xx/5xx + `{ "message": "...", "details": {...} }`
- 列表分页用响应头：`X-Total-Count`、`X-Page`

### GraphQL
- 单一端点 POST /graphql
- Schema 定义类型和查询
- 错误用 errors 数组

## 3. 错误码体系

{{根据 API_RESPONSE_FORMAT 生成错误码体系。包裹式用业务错误码，RESTful 用 HTTP 状态码：}}

### 包裹式业务错误码
| 范围 | 含义 |
|------|------|
| 0 | 成功 |
| 40000-40099 | 参数校验错误 |
| 40100-40199 | 认证错误 |
| 40300-40399 | 权限错误 |
| 40400-40499 | 资源不存在 |
| 50000-50099 | 服务端错误 |

### RESTful HTTP 状态码
| 状态码 | 含义 |
|--------|------|
| 200 | 成功 |
| 201 | 创建成功 |
| 204 | 无内容（删除成功） |
| 400 | 参数错误 |
| 401 | 未认证 |
| 403 | 无权限 |
| 404 | 不存在 |
| 429 | 限流 |
| 500 | 服务端错误 |

## 4. HTTP 方法

| 操作 | 方法 | 示例 |
|------|------|------|
| 查询列表 | GET | GET /api/v1/users |
| 查询详情 | GET | GET /api/v1/users/:id |
| 创建 | POST | POST /api/v1/users |
| 更新 | PUT | PUT /api/v1/users/:id |
| 部分更新 | PATCH | PATCH /api/v1/users/:id |
| 删除 | DELETE | DELETE /api/v1/users/:id |

## 5. 认证（{{API_AUTH_METHOD}}）

{{根据 API_AUTH_METHOD 生成认证规范：}}

### JWT（Access + Refresh Token）
- 除公开接口外，所有请求携带 Authorization: Bearer <accessToken>
- Access Token 有效期 15 分钟
- Refresh Token 有效期 7 天
- Token 过期返回 401（或业务码 40102），前端自动刷新

### Session + Cookie
- 登录后设置 HttpOnly Cookie
- 每个请求自动携带 Cookie
- 服务端校验 Session

### OAuth 2.0
- 第三方登录跳转授权
- 回调获取 authorization code
- 换取 access_token 和用户信息
- 绑定到本地用户

### API Key
- 请求头 X-API-Key: <key>
- 仅用于内部服务间调用
- 定期轮换

## 6. 分页参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| page | 1 | 当前页码 |
| pageSize | 20 | 每页数量，最大 100 |
| sortBy | - | 排序字段 |
| sortOrder | desc | asc / desc |

## 7. API 文档（{{API_DOC_TOOL}}）

{{根据 API_DOC_TOOL 生成文档规范：}}

### OpenAPI/Swagger
- 用注解/装饰器标注每个接口
- 自动生成 /docs 交互文档
- Schema 定义请求/响应类型
- 每次变更同步更新注解

### 手写 Markdown
- 每个资源一个 .md 文件
- 含请求/响应示例
- 放在 docs/api/ 目录

### TypeDoc / 类型推导
- 从 TypeScript 类型自动推导
- 无需额外注解
- 生成类型参考文档
```

---

## 8. database-spec.md 模板

```markdown
# {{PROJECT_NAME}} — 数据库规范

> 所有数据库设计**必须**遵循本规范。
> 最后更新：{{DATE}}

## 0. 工程定位

| 维度 | 选择 | 说明 |
|------|------|------|
| 命名规范 | {{DB_NAMING}} | {{根据规范说明：snake_case=PostgreSQL主流；camelCase=部分ORM默认；PascalCase=SQL Server风格}} |
| 主键策略 | {{DB_PRIMARY_KEY}} | {{根据策略说明：自增整数=简单；UUID v4=分布式友好无序；UUID v7/ULID=分布式+有序推荐；雪花=有序+分布式}} |
| 软删除 | {{DB_SOFT_DELETE}} | {{根据策略说明：软删除=可恢复；硬删除=直接DELETE；混合=用户数据软删除日志硬删除}} |
| 时间戳 | {{DB_TIMESTAMP}} | {{根据策略说明：UTC+TIMESTAMPTZ=时区安全推荐；本地时区=简单但易错；Unix毫秒=跨语言友好}} |
| 迁移管理 | {{DB_MIGRATION}} | {{根据方案说明：ORM内置=Prisma Migrate/Alembic/Flyway；手写SQL=灵活但易错；已有工具=用户提供}} |

## 1. 命名规范（{{DB_NAMING}}）

{{根据 DB_NAMING 生成命名规范表。例如 snake_case：}}

| 对象 | 规则 | 示例 |
|------|------|------|
| 表名 | snake_case 复数 | users、scores |
| 列名 | snake_case | created_at |
| 主键 | id | id |
| 外键 | {关联表单数}_id | user_id |
| 索引 | idx_{表}_{列} | idx_scores_user_id |
| 唯一索引 | uk_{表}_{列} | uk_users_email |
| 关联表 | {表A}_{表B} | user_roles |

{{如 DB_NAMING 为 camelCase：}}

| 对象 | 规则 | 示例 |
|------|------|------|
| 表名 | camelCase 复数 | users、userScores |
| 列名 | camelCase | createdAt |
| 主键 | id | id |
| 外键 | {关联表单数}Id | userId |

## 2. 通用列（基于 {{DB_PRIMARY_KEY}} 和 {{DB_TIMESTAMP}}）

{{根据 DB_PRIMARY_KEY 生成主键列定义：}}

### 自增整数
| 列名 | 类型 | 说明 |
|------|------|------|
| id | BIGSERIAL PRIMARY KEY | 自增主键 |

### UUID v4
| 列名 | 类型 | 说明 |
|------|------|------|
| id | UUID PRIMARY KEY DEFAULT gen_random_uuid() | UUID 主键 |

### UUID v7 / ULID（推荐新项目）
| 列名 | 类型 | 说明 |
|------|------|------|
| id | UUID PRIMARY KEY | UUID v7（有序，应用层生成） |

### 雪花算法
| 列名 | 类型 | 说明 |
|------|------|------|
| id | BIGINT PRIMARY KEY | 雪花 ID（应用层生成） |

{{根据 DB_TIMESTAMP 生成时间戳列定义：}}

### UTC + TIMESTAMPTZ（推荐）
| 列名 | 类型 | 说明 |
|------|------|------|
| created_at | TIMESTAMPTZ DEFAULT NOW() | 创建时间（UTC） |
| updated_at | TIMESTAMPTZ DEFAULT NOW() | 更新时间（UTC） |

### Unix 毫秒时间戳
| 列名 | 类型 | 说明 |
|------|------|------|
| created_at | BIGINT | 创建时间（Unix 毫秒） |
| updated_at | BIGINT | 更新时间（Unix 毫秒） |

{{根据 DB_SOFT_DELETE 决定是否包含 deleted_at 列：}}

### 软删除（如 DB_SOFT_DELETE 包含软删除）
| 列名 | 类型 | 说明 |
|------|------|------|
| deleted_at | TIMESTAMPTZ NULL | 软删除时间，NULL 表示未删除 |

## 3. 核心表结构

{{根据项目功能生成表结构，遵循上述命名/主键/时间戳/软删除策略}}

## 4. 索引策略

{{根据查询模式生成索引}}

## 5. 迁移管理（{{DB_MIGRATION}}）

{{根据 DB_MIGRATION 生成迁移规范：}}

### ORM 内置迁移（如 Prisma Migrate / Alembic / Flyway）
- 使用 {{ORM}} 管理迁移
- 每次迁移生成一个文件，不可修改已有迁移
- 迁移前必须备份数据库
- 迁移文件纳入版本控制
- 生产环境迁移用 `migrate deploy`（非 `migrate dev`）

### 手写 SQL 迁移
- 迁移文件命名：`V{版本号}__{描述}.sql`
- 每个迁移文件含 up 和 down 两部分
- 不可修改已执行的迁移文件

## 6. 软删除查询规范（如 {{DB_SOFT_DELETE}} 包含软删除）

- 所有查询默认过滤 `WHERE deleted_at IS NULL`
- ORM 层配置全局软删除过滤
- 需要查询已删除数据时显式 `includeDeleted: true`
- 唯一索引需配合软删除：`UNIQUE (email, deleted_at)` 或部分索引 `WHERE deleted_at IS NULL`

## 7. 备份与还原

### 自动备份

| 策略 | 频率 | 保留期 | 工具 |
|------|------|--------|------|
| 全量备份 | 每天凌晨 3:00 | 30 天 | pg_dump + cron |
| WAL 归档 | 实时 | 7 天 | PostgreSQL WAL |

### 还原流程

1. 停止应用服务
2. 恢复备份
3. 验证数据完整性
4. 重启应用
```

---

## 9. design-tokens.md 模板

```markdown
# {{PROJECT_NAME}} — 设计令牌规范

> 本文档是色彩、排版、间距、圆角、阴影的唯一权威来源。
> 任何组件或页面的视觉属性必须引用本文档中的令牌，禁止使用硬编码值。
> 最后更新：{{DATE}}

## 0. 设计定位

| 维度 | 选择 | 说明 |
|------|------|------|
| 主题模式 | {{THEME_MODE}} | {{根据选择说明：双主题需同时维护两套映射；仅浅色/仅深色只生成一套}} |
| 品牌主色 | {{BRAND_COLOR}} ({{BRAND_COLOR_HEX}}) | {{根据色系说明情感定位，如"蓝色系 — 专业/科技感"}} |
| 视觉风格 | {{VISUAL_STYLE}} | {{根据风格说明设计语言，如"极简主义 — 大量留白、克制色彩、细线分割"}} |
| 排版密度 | {{LAYOUT_DENSITY}} | {{根据密度说明间距倍率，紧凑=0.75x、舒适=1x、宽松=1.25x}} |
| 字体偏好 | {{FONT_PREFERENCE}} | {{根据字体偏好设置 fontSans/fontSerif/fontMono}} |
| 圆角偏好 | {{CORNER_RADIUS}} | {{根据圆角偏好调整 radiusSm/Md/Lg/Xl 的具体值}} |

{{如有 BRAND_GUIDELINES，在此追加"品牌规范约束"小节，列出 Logo 位置、品牌色、字体、视觉禁忌}}
{{如有 DESIGN_REFERENCES，在此追加"设计参考分析"小节，说明从参考站点提取的特征如何融入令牌}}

## 1. 令牌架构

```
原始色 (Primitive) ← 固定色值池，永不直接使用
       ↓ 映射
语义色 (Semantic)   ← 每个主题不同映射
       ↓ 引用
组件色 (Component)  ← 引用语义色，自动跟随主题
```

{{根据前端框架生成令牌实现方式：
- Flutter: ThemeData + ColorScheme + ThemeExtension
- React/Vue: CSS 变量 / Tailwind 配置
- Svelte: CSS 变量
}}

## 2. 原始色板

### 灰度
| 令牌 | 色值 |
|------|------|
| gray50 | #F9FAFB |
| gray100 | #F3F4F6 |
| ... | ... |
| gray950 | #0A0A0A |

### 品牌主色（{{BRAND_COLOR}}）
{{根据 BRAND_COLOR_HEX 生成 50-950 的色阶。例如蓝色系 #2563EB：}}

| 令牌 | 色值 | 用途 |
|------|------|------|
| brand50 | #EFF6FF | 主色浅底 |
| brand100 | #DBEAFE | 主色 hover 浅 |
| brand500 | {{BRAND_COLOR_HEX}} | 主色基准 |
| brand600 | #1D4ED8 | 主色 hover |
| brand700 | #1E40AF | 主色 active |
| brand900 | #1E3A8A | 主色深色 |

### 功能色
| 令牌 | 色值 | 用途 |
|------|------|------|
| success | #16A34A | 成功 |
| warning | #EA580C | 警告 |
| error | #DC2626 | 错误 |
| info | #0EA5E9 | 信息 |

## 3. 语义色

{{根据 THEME_MODE 生成语义色映射表。如果是双主题，必须同时给出浅色和深色两套映射：}}

### 浅色主题
| 语义令牌 | 引用 | 用途 |
|----------|------|------|
| bgPrimary | gray50 | 页面背景 |
| bgSecondary | white | 卡片背景 |
| textPrimary | gray900 | 主文字 |
| textSecondary | gray500 | 次文字 |
| accent | brand500 | 强调色 |
| border | gray200 | 分割线 |

### 深色主题（如 {{THEME_MODE}} 包含深色）
| 语义令牌 | 引用 | 用途 |
|----------|------|------|
| bgPrimary | gray950 | 页面背景 |
| bgSecondary | gray900 | 卡片背景 |
| textPrimary | gray50 | 主文字 |
| textSecondary | gray400 | 次文字 |
| accent | brand400 | 强调色（深色背景上提亮一档） |
| border | gray800 | 分割线 |

## 4. 组件色

{{根据组件类型生成组件色映射表，全部引用语义色}}

## 5. 排版令牌

### 字体族（基于 {{FONT_PREFERENCE}}）
{{根据字体偏好生成字体族表。例如：}}

| 偏好 | 令牌 | 值 |
|------|------|-----|
| 无衬线 | fontSans | Inter, system-ui, sans-serif |
| 衬线+无衬线混搭 | fontSerif | Georgia, serif（标题用） |
| 等宽强调 | fontMono | JetBrains Mono, Consolas, monospace |

### 字号
| 令牌 | 字号 | 行高 | 用途 |
|------|------|------|------|
| textXs | 12px | 16px | 辅助标注 |
| textSm | 14px | 20px | 次要文字 |
| textBase | 16px | 24px | 正文 |
| textLg | 18px | 28px | 小标题 |
| textXl | 20px | 28px | 区块标题 |
| text2xl | 24px | 32px | 页面标题 |
| text3xl | 30px | 36px | 大标题 |
| text4xl | 36px | 40px | 首屏标题 |

## 6. 间距令牌（基于 {{LAYOUT_DENSITY}}）

{{根据排版密度调整间距倍率：紧凑=0.75x、舒适=1x、宽松=1.25x。以舒适为基准：}}

| 令牌 | 紧凑 | 舒适 | 宽松 | 用途 |
|------|------|------|------|------|
| space1 | 3px | 4px | 5px | 图标与文字间距 |
| space2 | 6px | 8px | 10px | 紧凑内边距 |
| space3 | 9px | 12px | 15px | 默认内边距 |
| space4 | 12px | 16px | 20px | 卡片内边距 |
| space6 | 18px | 24px | 30px | 大区块间距 |
| space8 | 24px | 32px | 40px | 页面边距 |
| space10 | 30px | 40px | 50px | 大留白 |

## 7. 圆角令牌（基于 {{CORNER_RADIUS}}）

{{根据圆角偏好调整圆角值：}}

| 偏好 | radiusSm | radiusMd | radiusLg | radiusXl | radiusFull |
|------|----------|----------|----------|----------|------------|
| 锐利 | 2px | 4px | 6px | 8px | 9999px |
| 适中 | 4px | 8px | 12px | 16px | 9999px |
| 圆润 | 8px | 16px | 24px | 32px | 9999px |
| 药丸形 | 9999px | 9999px | 9999px | 9999px | 9999px |

**本项目采用 {{CORNER_RADIUS}} 偏好。**

## 8. 阴影令牌

{{根据 VISUAL_STYLE 调整阴影风格：}}
- 极简主义：阴影极轻或无阴影，用边框分割
- Material Design：标准 elevation 阴影
- 拟物新拟态：柔和双向阴影（亮顶+暗底）
- 玻璃拟态：彩色半透明阴影

| 令牌 | 浅色主题 | 深色主题 |
|------|----------|----------|
| shadowSm | 0 1px 2px rgba(0,0,0,0.05) | 0 1px 2px rgba(0,0,0,0.3) |
| shadowMd | 0 4px 6px rgba(0,0,0,0.07) | 0 4px 6px rgba(0,0,0,0.4) |
| shadowLg | 0 10px 15px rgba(0,0,0,0.1) | 0 10px 15px rgba(0,0,0,0.5) |

## 9. 动效令牌（基于 {{ANIMATION_STYLE}}）

{{根据动效风格调整持续时间和缓动：}}

| 风格 | durationFast | durationNormal | durationSlow | 说明 |
|------|--------------|----------------|--------------|------|
| 极简动效 | 100ms | 200ms | 400ms | 仅必要过渡，无装饰动画 |
| 适度微交互 | 150ms | 300ms | 600ms | hover/active 反馈 + 页面过渡 |
| 丰富动效 | 200ms | 400ms | 800ms | 逐字动画、弹性效果 |
| 沉浸动效 | 300ms | 600ms | 1200ms | 全屏过渡、视差、3D |

**本项目采用 {{ANIMATION_STYLE}} 风格。**

| 令牌 | 值 | 用途 |
|------|-----|------|
| durationFast | {{根据风格}} | 微交互 |
| durationNormal | {{根据风格}} | 页面过渡 |
| durationSlow | {{根据风格}} | 加载动画 |
| curveEase | ease-out | 默认缓动 |
| curveSpring | spring | 弹性效果（仅丰富/沉浸动效） |
```

---

## 10. layout-principles.md 模板

```markdown
# {{PROJECT_NAME}} — 排版规范

> 本文档规定排版原则与令牌映射，开发者必须遵守。
> 最后更新：{{DATE}}

## 0. 设计定位

| 维度 | 选择 | 对排版的影响 |
|------|------|--------------|
| 视觉风格 | {{VISUAL_STYLE}} | {{根据风格说明排版倾向，如"极简主义 — 大量留白、克制分割线、信息层次靠字号字重"}} |
| 排版密度 | {{LAYOUT_DENSITY}} | {{根据密度说明：紧凑=信息密集、舒适=标准、宽松=展示型}} |

## 1. 不对称美感
- 不对称 ≠ 不平衡，视觉重心通过大小/色重/留白平衡
- 对称仅用于数据表格等需要精确对比的场景
{{如 VISUAL_STYLE 为极简主义/Bento Grid，追加风格特定说明：}}
{{- 极简主义：不对称是核心，避免居中堆叠的呆板感}}
{{- Bento Grid：通过网格大小变化实现不对称，每个网格承载一类信息}}

## 2. 对齐
- 全局 8px 网格对齐
- 左对齐为默认，右对齐仅用于数字数据
{{如 LAYOUT_DENSITY 为紧凑，追加："紧凑模式下可使用 4px 子网格对齐图标与文字"}}

## 3. 对比
- 核心信息与辅助信息至少 3 级字号差
- 主色元素与背景必须醒目区分
{{如 VISUAL_STYLE 为粗犷主义，追加："粗犷主义鼓励强对比，可用 5 级字号差和黑白对比"}}

## 4. 重复
- 相同功能的元素使用相同的视觉处理
- 一致性降低认知负担

## 5. 亲密
- 相关元素靠近，无关元素远离
- 间距量与关系强度成反比
{{根据 LAYOUT_DENSITY 调整亲密性间距基准：紧凑=6px/12px/18px、舒适=8px/16px/24px、宽松=12px/24px/40px}}

## 6. 留白
- 留白量与信息重要性成正比
- 页面内容最大宽度 1200px，两侧自动留白
{{如 LAYOUT_DENSITY 为宽松，追加："宽松模式下首屏留白占比可达 40%，用于展示型/品牌型页面"}}
{{如 LAYOUT_DENSITY 为紧凑，追加："紧凑模式下留白最小化，信息密度优先，适合数据仪表盘"}}

## 7. 层次感
- Z 轴层次：通过阴影和背景色差模拟深度
- 信息层次：通过字号、字重、色重引导视线
{{如 VISUAL_STYLE 为玻璃拟态，追加："玻璃拟态通过半透明和模糊背景营造层次，避免过多层级导致视觉混乱"}}
{{如 VISUAL_STYLE 为拟物新拟态，追加："新拟态通过柔和双向阴影表现凹凸，层次感来自立体而非颜色对比"}}

## 8. 风格特定排版指引（{{VISUAL_STYLE}}）

{{根据 VISUAL_STYLE 生成风格特定的排版指引：}}

- **极简主义**：少即是多，一个页面一个视觉焦点，用留白和字号引导视线，避免装饰性元素
- **Material Design**：遵循 Material elevation，卡片有明确阴影，使用 FAB 和 AppBar 等标准组件
- **拟物新拟态**：柔和阴影 + 单色背景，元素凹凸分明，避免强对比色，圆角统一
- **玻璃拟态**：半透明卡片 + 背景模糊，彩色渐变背景，卡片内信息层次清晰
- **Bento Grid**：网格化布局，每个网格独立信息单元，网格大小不等形成节奏感
- **粗犷主义**：强对比、粗边框、单色块，反传统排版，可用大字号和不对称布局制造冲击力

{{根据前端框架生成具体实现代码示例}}
```

---

## 11. security-spec.md 模板

```markdown
# {{PROJECT_NAME}} — 安全规范

> 所有开发**必须**遵循本规范。安全漏洞为最高优先级修复项。
> 最后更新：{{DATE}}

## 0. 工程定位

| 维度 | 选择 | 说明 |
|------|------|------|
| 密码加密 | {{SEC_PASSWORD_HASH}} | {{根据算法说明：bcrypt=主流推荐；argon2id=更安全新项目推荐；scrypt=高内存成本}} |
| Token 存储 | {{SEC_TOKEN_STORAGE}} | {{根据位置说明：HttpOnly Cookie=防XSS推荐；localStorage=简单但易XSS；内存+Refresh Cookie=平衡}} |
| CORS 策略 | {{SEC_CORS}} | {{根据策略说明：白名单=推荐；同源=最严格；特定方法头=精细控制}} |
| 限流策略 | {{SEC_RATE_LIMIT}} | {{根据策略说明：分级=推荐；全局=简单；按用户=精准；暂不限=小项目}} |
| 审计日志 | {{SEC_AUDIT_LOG}} | {{根据策略说明：所有写操作=完整可追溯；仅敏感=轻量；不记录=小项目}} |
| 数据脱敏 | {{SEC_DATA_MASKING}} | {{根据策略说明：自动脱敏=推荐；仅日志=部分；不脱敏=风险}} |

## 1. 认证与授权
| 领域 | 规范 |
|------|------|
| {{AUTH_METHOD}} | {{根据 API_AUTH_METHOD 生成具体规范}} |
| Access Token | 15 分钟有效期 |
| Refresh Token | 7 天有效期 |
| 密码存储 | {{SEC_PASSWORD_HASH}}{{如 bcrypt: saltRounds=12}}{{如 argon2id: memoryCost=19456, timeCost=2, parallelism=1}} |
| 密码规则 | 最小 8 位，含字母+数字 |
| 登录失败 | 5 次失败锁定 15 分钟 |
| Token 存储 | {{SEC_TOKEN_STORAGE}}{{如 HttpOnly Cookie: Secure+HttpOnly+SameSite=Strict}}{{如 localStorage: 前端需防 XSS}} |

## 2. 输入安全
| 领域 | 规范 |
|------|------|
| XSS | 服务端转义，前端不用 innerHTML 等价物 |
| SQL 注入 | {{ORM}} 参数化查询 |
| 输入校验 | Route 层校验，拒绝超长/非法字符 |
| 文件上传 | 白名单扩展名，大小限制 |

## 3. 传输安全
| 领域 | 规范 |
|------|------|
| HTTPS | 生产环境强制 HTTPS + HSTS |
| CORS | {{SEC_CORS}}{{如白名单: 列出允许的域名，禁止 *}}{{如同源: credentials=true, origin=同源}} |
| CSRF | SameSite Cookie + Origin 校验 |
| WebSocket | WSS only（如需） |

## 4. 速率限制（{{SEC_RATE_LIMIT}}）

{{根据 SEC_RATE_LIMIT 生成限流规范：}}

### 分级限流（推荐）
| 接口 | 限制 | 说明 |
|------|------|------|
| 全局 | 100 req/min/IP | 通用限流 |
| 登录 | 5 次/min/IP | 防暴力破解 |
| 注册 | 3 次/hour/IP | 防批量注册 |
| 写操作 | 10 次/min/user | 防刷 |
| 查询 | 30 次/min/user | 防爬取 |

### 全局统一限流
| 接口 | 限制 |
|------|------|
| 全局 | 100 req/min/IP |

### 按用户限流
| 接口 | 限制 |
|------|------|
| 所有接口 | 100 req/min/user |

## 5. 敏感数据（{{SEC_DATA_MASKING}}）

{{根据 SEC_DATA_MASKING 生成脱敏规范：}}

### 自动脱敏（推荐）
- 密码不落日志
- 密钥走环境变量
- 邮箱脱敏：`u***@example.com`
- 手机号脱敏：`138****8888`
- 身份证脱敏：`110***********1234`
- API 响应中敏感字段自动脱敏

### 仅日志脱敏
- 密码不落日志
- 密钥走环境变量
- 日志中邮箱/手机号脱敏
- API 响应不脱敏（前端按需展示）

## 6. 审计日志（{{SEC_AUDIT_LOG}}）

{{根据 SEC_AUDIT_LOG 生成审计规范：}}

### 所有写操作（推荐）
- 记录所有增删改操作
- 含：操作人、操作时间、操作类型、目标对象、变更前后值
- 审计日志独立表，不可修改，保留 1 年
- 支持按操作人/时间/类型查询

### 仅敏感操作
- 记录：登录/登出、权限变更、数据导出、敏感数据访问
- 含：操作人、操作时间、操作类型、IP、User-Agent

## 7. HTTP 安全头
```
X-Content-Type-Options: nosniff
X-Frame-Options: DENY
X-XSS-Protection: 1; mode=block
Content-Security-Policy: default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'
Strict-Transport-Security: max-age=31536000; includeSubDomains
Referrer-Policy: strict-origin-when-cross-origin
```

## 8. 依赖安全
- 每周审计依赖漏洞（npm audit / pip audit / go vet）
- 高危 24h 内修复
- 中危 7 天内修复
- 低危下次迭代修复
- 锁定版本，禁止浮动版本号
```

---

## 12. testing-spec.md 模板

```markdown
# {{PROJECT_NAME}} — 测试规范

> 所有测试开发**必须**遵循本规范。
> 最后更新：{{DATE}}

## 0. 工程定位

| 维度 | 选择 | 说明 |
|------|------|------|
| 覆盖率要求 | {{TEST_COVERAGE}} | {{根据严格度说明：严格=长期项目推荐；标准=中等；宽松=仅核心逻辑}} |
| E2E 方案 | {{TEST_E2E_TOOL}} | {{根据工具说明：Playwright=跨浏览器推荐；Cypress=开发体验好；Selenium=传统；暂不需要=小项目}} |
| 测试数据 | {{TEST_DATA_MGMT}} | {{根据方案说明：Factory+事务回滚=隔离性好推荐；固定种子=简单易耦合；Mock=单元测试用}} |

## 1. 测试分层

| 层级 | 范围 | 工具 | 速度 |
|------|------|------|------|
| 单元测试 | 函数/类逻辑 | {{根据语言}} | 极快 |
| 组件测试 | 单个组件渲染 | {{根据框架}} | 快 |
| 集成测试 | 多组件协作 | {{根据框架}} | 中 |
| E2E 测试 | 完整用户流程 | {{TEST_E2E_TOOL}}{{如暂不需要则标注"本项目暂不采用 E2E"}} | 慢 |

## 2. 前端测试

{{根据前端框架生成测试规范：
- Flutter: flutter_test, integration_test
- React: vitest + testing-library + {{TEST_E2E_TOOL}}
- Vue: vitest + vue-test-utils + {{TEST_E2E_TOOL}}
}}

## 3. 后端测试

{{根据后端框架生成测试规范：
- Node.js: vitest + supertest/fastify.inject
- Python: pytest + httpx
- Go: testing + httptest
}}

## 4. 覆盖率要求（{{TEST_COVERAGE}}）

{{根据 TEST_COVERAGE 生成覆盖率要求表：}}

### 严格（推荐长期项目）
| 层级 | 最低覆盖率 |
|------|-----------|
| 后端 Service 层 | ≥ 80% |
| 前端逻辑层 | ≥ 80% |
| 组件层 | ≥ 60% |
| 总体 | ≥ 70% |

### 标准
| 层级 | 最低覆盖率 |
|------|-----------|
| 后端 Service 层 | ≥ 60% |
| 前端逻辑层 | ≥ 60% |
| 总体 | ≥ 50% |

### 宽松
- 仅核心业务逻辑需测试
- 无强制覆盖率要求
- 建议关键路径有测试覆盖

## 5. 测试数据管理（{{TEST_DATA_MGMT}}）

{{根据 TEST_DATA_MGMT 生成测试数据规范：}}

### Factory 模式 + 事务回滚（推荐）
- 用 factory 模式生成测试数据（如 `userFactory.build()`）
- 数据库测试用 transaction rollback，每个测试后回滚
- 禁止测试间共享状态
- Factory 集中管理，避免散落的测试数据构造代码

### 固定种子数据
- 数据库预置固定种子数据
- 测试依赖种子数据存在
- 注意：测试间易耦合，修改种子数据可能破坏多个测试

### Mock 所有外部依赖
- 单元测试 Mock 所有外部依赖（数据库、API、文件系统）
- 集成测试用真实依赖
- 注意：Mock 过多会导致测试与实现强耦合

## 6. CI 中的测试
- PR 提交：单元测试 + 组件测试
- 合并 develop：集成测试 + E2E（如采用）
- 测试失败阻止合并
- 覆盖率低于阈值阻止合并（如采用覆盖率要求）

## 7. 测试命名规范
- 单元测试：`describe('UserService', () => it('should create user'))`
- E2E 测试：`test('用户登录成功跳转首页')`
- 文件命名：`*.test.ts` / `*.spec.ts` / `*_test.dart`
```

---

## 13. performance-spec.md 模板

```markdown
# {{PROJECT_NAME}} — 性能规范

> 所有性能优化**必须**遵循本规范。
> 最后更新：{{DATE}}

## 0. 工程定位

| 维度 | 选择 | 说明 |
|------|------|------|
| 预算严格度 | {{PERF_BUDGET_STRICTNESS}} | {{根据严格度说明：严格=性能敏感项目推荐；标准=普通应用；宽松=无明确预算}} |
| 监控方案 | {{PERF_MONITORING}} | {{根据方案说明：前端RUM=真实用户监控；后端APM=应用性能监控；合成监控=定时跑Lighthouse}} |
| 性能测试 | {{PERF_TESTING}} | {{根据方案说明：Lighthouse CI=前端每次PR；k6=后端发布前压测；两者都要=全栈推荐}} |

## 1. 性能预算（{{PERF_BUDGET_STRICTNESS}}）

{{根据 PERF_BUDGET_STRICTNESS 生成性能预算表：}}

### 严格（推荐性能敏感项目）
| 场景 | 指标 | 预算 |
|------|------|------|
| 首屏加载 | LCP | ≤ 2.5s |
| 首屏加载 | FCP | ≤ 1.8s |
| 可交互 | TTI | ≤ 3.5s |
| 页面切换 | 路由过渡 | ≤ 300ms |
| API 响应 | P95 延迟 | ≤ 200ms |
| 渲染 | FPS | ≥ 60fps |

### 标准
| 场景 | 指标 | 预算 |
|------|------|------|
| 首屏加载 | LCP | ≤ 4s |
| API 响应 | P95 延迟 | ≤ 500ms |
| 渲染 | FPS | ≥ 30fps |

### 宽松
- 无明确性能预算
- 尽力优化，以用户体感为准
- 出现明显卡顿再优化

## 2. 前端性能

{{根据前端框架生成性能优化规范}}

## 3. 后端性能

- API P95 ≤ {{根据严格度 200ms/500ms}}
- 数据库查询用索引
- 禁止 N+1 查询
- 分页必须用游标或 offset
- 耗时操作异步化（队列/定时任务）

## 4. 缓存策略

| 数据 | 缓存层 | TTL | 失效策略 |
|------|--------|-----|----------|
| {{数据类型}} | {{缓存层}} | {{TTL}} | {{策略}} |

## 5. 性能监控（{{PERF_MONITORING}}）

{{根据 PERF_MONITORING 生成监控规范：}}

### 前端 RUM（如选中）
- 工具：Sentry / Datadog RUM
- 采集：LCP、FCP、CLS、FID、TTFB
- 采样率：生产环境 10%
- 告警：LCP > 4s

### 后端 APM（如选中）
- 工具：Sentry / New Relic / Prometheus
- 采集：API 响应时间、错误率、吞吐量
- 采样率：100%（错误）/ 10%（正常）
- 告警：API P95 > 1s、错误率 > 1%

### 合成监控（如选中）
- 工具：Lighthouse CI 定时跑
- 频率：每小时跑一次关键页面
- 告警：性能分数 < 80

### 暂不监控（如选中）
- 本项目暂不接入性能监控
- 后续按需引入

## 6. 性能测试（{{PERF_TESTING}}）

{{根据 PERF_TESTING 生成性能测试规范：}}

### Lighthouse CI（如选中）
- 每次 PR 运行 Lighthouse CI
- 检查关键页面的性能分数
- 性能分数 < 80 阻止合并

### k6 / autocannon（如选中）
- 发布前用 k6 压测后端 API
- 压测场景：正常负载、峰值负载、持续负载
- 通过标准：P95 ≤ 预算、错误率 < 0.1%

### 暂不需要（如选中）
- 本项目暂不进行性能测试
- 后续按需引入
```

---

## 14. cicd-spec.md 模板

```markdown
# {{PROJECT_NAME}} — CI/CD 规范

> 所有 CI/CD 配置**必须**遵循本规范。
> 最后更新：{{DATE}}

## 0. 工程定位

| 维度 | 选择 | 说明 |
|------|------|------|
| CI/CD 平台 | {{CICD_PLATFORM}} | {{根据平台说明：GitHub Actions=与GitHub集成推荐；GitLab CI=GitLab集成；Jenkins=自建；暂不需要=小项目}} |
| 部署触发 | {{CICD_TRIGGER}} | {{根据触发说明：main push=自动部署推荐；Tag手动=可控；PR合并=持续部署；仅手动=小项目}} |
| 制品管理 | {{CICD_ARTIFACT}} | {{根据制品说明：Docker镜像=容器化推荐；静态产物+CDN=前端；源码直接=小项目}} |

{{如 CICD_PLATFORM 为"暂不需要 CI/CD"，本规范简化为"本项目暂不采用 CI/CD，后续按需引入"，并给出引入建议。}}

## 1. 平台
- CI/CD 平台：{{CICD_PLATFORM}}
- Runner：{{根据平台，如 ubuntu-latest}}
- 配置文件位置：{{根据平台，如 .github/workflows/}}

## 2. Pipeline 总览

```
Push/PR → Lint → Test → Build → Deploy（{{CICD_TRIGGER}}）
```

## 3. 阶段定义

| 阶段 | 触发 | 内容 | 失败处理 |
|------|------|------|----------|
| Lint | 所有 push/PR | 代码质量检查 | 阻止合并 |
| Test | 所有 push/PR | 单元+组件测试 | 阻止合并 |
| Build | 所有 push/PR | 构建产物（{{CICD_ARTIFACT}}） | 阻止合并 |
| E2E | develop/main | 集成+E2E 测试（如采用） | 阻止部署 |
| Deploy | {{CICD_TRIGGER}} | 部署到对应环境 | 回滚 |

## 4. 分支触发规则

{{根据 CICD_TRIGGER 生成触发规则表：}}

### main 分支 push 自动部署（推荐）
| 分支 | 触发 | 部署 |
|------|------|------|
| feat/*、fix/* | PR CI | 无 |
| develop | push CI + E2E | staging |
| main | push CI + E2E + Deploy | production |

### Tag 发布后手动触发
| 分支 | 触发 | 部署 |
|------|------|------|
| feat/*、fix/* | PR CI | 无 |
| develop | push CI | development |
| main | tag push | production（手动确认） |

## 5. 制品管理（{{CICD_ARTIFACT}}）

{{根据 CICD_ARTIFACT 生成制品管理规范：}}

### Docker 镜像 + Registry（推荐容器化项目）
- 构建多阶段 Docker 镜像
- 推送到 Registry（GHCR / Docker Hub / 私有 Registry）
- 镜像标签：`{repo}:{branch}-{sha}` + `{repo}:latest`
- 保留最近 10 个版本

### 静态产物 + CDN（前端项目）
- 构建静态文件（dist/、build/web/）
- 上传到 CDN / 对象存储
- 版本号用 commit sha
- 保留最近 10 个版本

### 源码直接部署（小项目）
- 服务器 git pull
- 本地构建
- 重启服务
- 注意：不推荐生产环境

## 6. 缓存策略
{{根据包管理器生成缓存配置}}

## 7. 安全
- Secrets 通过 {{CICD_PLATFORM}} Secrets 注入
- Fork PR 不触发部署
- 依赖审计每周执行
- 制品签名（如采用 Docker）
```

---

## 15. deployment-spec.md 模板

```markdown
# {{PROJECT_NAME}} — 部署规范

> 所有部署操作**必须**遵循本规范。
> 最后更新：{{DATE}}

## 0. 工程定位

| 维度 | 选择 | 说明 |
|------|------|------|
| 环境划分 | {{DEPLOY_ENVIRONMENTS}} | {{根据选择说明：4环境=长期项目推荐；3环境=标准；2环境=小项目}} |
| 部署策略 | {{DEPLOY_STRATEGY}} | {{根据策略说明：滚动=零停机推荐；蓝绿=快速回滚；金丝雀=渐进式大项目；直接替换=小项目有停机}} |
| 回滚策略 | {{DEPLOY_ROLLBACK}} | {{根据策略说明：自动=健康检查失败自动回滚推荐；手动=人工确认；保留N版本=版本管理}} |

## 1. 环境划分（{{DEPLOY_ENVIRONMENTS}}）

{{根据 DEPLOY_ENVIRONMENTS 生成环境划分表：}}

### 4 环境（推荐长期项目）
| 环境 | 用途 | 分支 | 访问 |
|------|------|------|------|
| local | 本地开发 | feat/* | 开发者 |
| development | 开发联调 | develop | 团队 |
| staging | 预发布 | develop(tag) | 团队 |
| production | 生产 | main | 公开 |

### 3 环境（标准）
| 环境 | 用途 | 分支 | 访问 |
|------|------|------|------|
| local | 本地开发 | feat/* | 开发者 |
| staging | 预发布 | develop | 团队 |
| production | 生产 | main | 公开 |

### 2 环境（小项目）
| 环境 | 用途 | 分支 | 访问 |
|------|------|------|------|
| local | 本地开发 | feat/* | 开发者 |
| production | 生产 | main | 公开 |

## 2. 部署架构

{{根据架构生成部署架构图}}

## 3. 前端部署
{{根据前端框架生成部署方式}}

## 4. 后端部署
{{根据后端框架生成部署方式，含 Dockerfile 示例}}

## 5. 数据库部署
- 版本：{{DATABASE_VERSION}}
- 迁移：部署时自动执行
- 备份：见 database-spec.md

## 6. 部署流程（{{DEPLOY_STRATEGY}}）

{{根据 DEPLOY_STRATEGY 生成部署流程：}}

### 滚动部署（推荐，零停机）
1. CI 构建产物
2. 拉取最新镜像/产物
3. 执行数据库迁移
4. 逐个实例替换（旧实例处理完请求后下线，新实例上线）
5. 健康检查
6. 全部实例替换完成

### 蓝绿部署（快速回滚）
1. CI 构建产物
2. 部署到绿色环境（当前不接收流量）
3. 执行数据库迁移
4. 健康检查
5. 流量从蓝色切换到绿色
6. 蓝色环境保留作为回滚

### 金丝雀发布（渐进式，大项目推荐）
1. CI 构建产物
2. 部署到金丝雀实例（接收 5% 流量）
3. 监控指标 30 分钟
4. 逐步扩大流量（5% → 25% → 50% → 100%）
5. 每阶段健康检查通过才继续
6. 异常自动回滚

### 直接替换（小项目，有停机）
1. CI 构建产物
2. 停止服务
3. 替换产物
4. 执行数据库迁移
5. 重启服务
6. 健康检查

## 7. 回滚策略（{{DEPLOY_ROLLBACK}}）

{{根据 DEPLOY_ROLLBACK 生成回滚规范：}}

### 自动回滚（推荐）
- 健康检查连续 3 次失败自动回滚
- 回滚到上一个健康版本
- 回滚后通知团队
- 数据库迁移不可自动回滚（需手动处理）

### 手动回滚
- 人工确认后执行回滚
- 回滚命令：`deploy rollback --to {version}`
- 回滚前需确认数据库兼容性

### 保留最近 N 个版本
- 后端：保留最近 5 个镜像版本
- 前端：保留最近 10 个产物版本
- 数据库：见 database-spec.md

## 8. 健康检查

| 服务 | 端点 | 预期 | 频率 |
|------|------|------|------|
| API | GET /api/v1/health | 200 | 10s |
| 前端 | GET / | 200 | 60s |
| 数据库 | TCP 连接 | 成功 | 30s |
```

---

## 16. git-spec.md 模板

```markdown
# {{PROJECT_NAME}} — Git 规范

> 所有 Git 操作**必须**遵循本规范。
> 最后更新：{{DATE}}

## 1. 分支策略

| 分支 | 用途 | 命名 | 保护 |
|------|------|------|------|
| main | 生产 | - | 禁止直接 push |
| develop | 开发集成 | - | 禁止 force push |
| 功能分支 | 新功能 | feat/描述 | 无 |
| 修复分支 | Bug 修复 | fix/描述 | 无 |
| 热修复 | 紧急修复 | hotfix/描述 | 无 |

## 2. 提交信息格式

```
<type>(<scope>): <description>
```

### Type 列表
| type | 说明 |
|------|------|
| feat | 新功能 |
| fix | Bug 修复 |
| docs | 文档变更 |
| style | 格式调整 |
| refactor | 重构 |
| perf | 性能优化 |
| test | 测试 |
| chore | 构建/工具 |

## 3. PR 规范
- 标题同 commit 格式
- 必须关联 issue
- 至少 1 人 review
- CI 通过才能合并
- 使用 squash merge

## 4. .gitignore 必须包含

{{根据技术栈生成 .gitignore 内容}}
```

---

## 17. animation-spec.md 模板

```markdown
# {{PROJECT_NAME}} — 动效规范

> 所有动画/过渡效果**必须**遵循本规范。
> 最后更新：{{DATE}}

## 0. 动效定位

| 维度 | 选择 | 说明 |
|------|------|------|
| 动效风格 | {{ANIMATION_STYLE}} | {{根据风格说明：极简动效=仅必要过渡；适度微交互=hover/active+页面过渡；丰富动效=逐字动画+弹性；沉浸动效=全屏过渡+视差+3D}} |

{{根据 ANIMATION_STYLE 生成动效强度基准：}}

| 风格 | 微交互时长 | 页面过渡时长 | 加载动画时长 | 装饰性动画 | 弹性效果 |
|------|-----------|-------------|-------------|-----------|---------|
| 极简动效 | 100ms | 200ms | 400ms | 禁用 | 禁用 |
| 适度微交互 | 150ms | 300ms | 600ms | 慎用 | 慎用 |
| 丰富动效 | 200ms | 400ms | 800ms | 鼓励 | 鼓励 |
| 沉浸动效 | 300ms | 600ms | 1200ms | 核心特色 | 核心特色 |

**本项目采用 {{ANIMATION_STYLE}} 风格，所有动效时长以上表为准。**

## 1. 加载动画
| 场景 | 动画 | 规格 |
|------|------|------|
| 页面加载 | Logo 脉冲 | 渐显+缩放，{{根据风格 400-1200ms}} |
| 数据加载 | 骨架屏 | 扫光循环，1.5s |
| 按钮提交 | Spinner | 16px，无限循环 |

{{如 ANIMATION_STYLE 为极简动效，追加："极简风格下页面加载仅用渐显，不加缩放；数据加载用线性进度条替代骨架屏扫光"}}
{{如 ANIMATION_STYLE 为沉浸动效，追加："沉浸风格下页面加载可加入品牌 Logo 的故事性动画，时长可达 2s"}}

## 2. 页面过渡
| 场景 | 动画 | 规格 |
|------|------|------|
| 页面进入 | 淡入+上移 | {{根据风格 200-600ms}} |
| 页面离开 | 淡出 | {{根据风格 150-400ms}} |
| 模态框弹出 | 缩放+淡入 | {{根据风格 200-600ms}} |

{{如 ANIMATION_STYLE 为极简动效，追加："极简风格仅用淡入淡出，不加位移和缩放"}}
{{如 ANIMATION_STYLE 为沉浸动效，追加："沉浸风格可用全屏过渡（如共享元素过渡、视差滚动）"}}

## 3. 微交互
| 场景 | 动画 | 规格 |
|------|------|------|
| 按钮 hover | 背景渐变 | {{根据风格 100-300ms}} |
| 按钮 active | 缩小 | scale 0.97, {{根据风格 80-200ms}} |
| 卡片 hover | 阴影加深 | {{根据风格 150-300ms}} |

{{如 ANIMATION_STYLE 为极简动效，追加："极简风格仅保留 active 反馈，hover 仅用颜色变化不用位移"}}
{{如 ANIMATION_STYLE 为丰富/沉浸动效，追加："丰富动效鼓励加入弹性回弹、逐字动画、装饰性微交互"}}

## 4. 装饰性动画（仅 {{ANIMATION_STYLE}} 为丰富/沉浸时适用）
{{如 ANIMATION_STYLE 为极简/适度，本节标注"本项目不使用装饰性动画"}}
{{如 ANIMATION_STYLE 为丰富/沉浸：}}

| 场景 | 动画 | 规格 |
|------|------|------|
| 标题入场 | 逐字浮现 | 每字 50ms 延迟，弹性缓动 |
| 数据更新 | 数字滚动 | 600ms，ease-out |
| 成功反馈 | 礼花/对勾动画 | 800ms，一次性 |
| 背景装饰 | 浮动粒子/渐变流动 | 持续循环，opacity ≤ 0.3 |

## 5. 性能约束
- 优先用 transform/opacity（GPU 合成层）
- 动画帧率 ≥ 30fps
- 尊重 prefers-reduced-motion
{{如 ANIMATION_STYLE 为沉浸动效，追加："沉浸动效必须用 RepaintBoundary/will-change 隔离合成层，避免主线程阻塞"}}
{{如 ANIMATION_STYLE 为极简动效，追加："极简动效本身性能开销极低，无需额外优化"}}

{{根据前端框架生成具体实现方式：
- Flutter: AnimationController + Tween + CurvedAnimation，性能敏感处用 RepaintBoundary
- React: framer-motion / CSS transition，用 will-change 提示合成层
- Vue: CSS transition / transition-group
}}
```

---

## 18. CLAUDE.md 模板

```markdown
## Project: {{PROJECT_NAME}}

{{PROJECT_DESC}}。开发前**必须**阅读以下文档：

### 必读文档（按优先级）

1. **`docs/TECH-STACK.md`** — 技术栈总览。**所有技术选型以此文件为准。**
2. **`docs/secrets-management.md`** — 敏感信息管理。**禁止将密钥提交 Git。**
3. **`CONTEXT.md`** — 领域语言，术语定义。
4. **`docs/spec.md`** — 功能规格文档。
5. **`docs/design-tokens.md`** — 设计令牌。**禁止硬编码值。**
6. **`docs/layout-principles.md`** — 排版规范。
7. **`docs/api-spec.md`** — API 设计规范。
8. **`docs/database-spec.md`** — 数据库规范。
9. **`docs/backend-spec.md`** — 后端代码规范。
10. **`docs/frontend-spec.md`** — 前端代码规范。
11. **`docs/security-spec.md`** — 安全规范。
12. **`docs/testing-spec.md`** — 测试规范。
13. **`docs/performance-spec.md`** — 性能规范。
14. **`docs/cicd-spec.md`** — CI/CD 规范。
15. **`docs/deployment-spec.md`** — 部署规范。
16. **`docs/animation-spec.md`** — 动效规范。
17. **`docs/git-spec.md`** — Git 规范。
18. **`docs/adr/`** — 架构决策记录。
19. **`docs/project-harness-checklist.md`** — 规范覆盖度清单。

### 强制规则

- **技术栈**：{{根据用户选择生成}}
- **敏感信息**：密钥只放后端 .env，禁止提交 Git
- **颜色**：{{根据前端框架}}，禁止硬编码色值
- **间距**：使用设计令牌间距值，所有尺寸为 8 的倍数
- **术语**：使用 CONTEXT.md 中定义的术语
- **文件操作**：仅允许在项目目录内操作

### 文档索引

| 文件 | 内容 |
|------|------|
{{所有文档的索引表}}
```

---

## 19. ADR 模板

```markdown
# ADR 0001: {{决策标题}}

## 状态

已接受 — {{DATE}}

## 上下文

{{描述需要做决策的背景和问题}}

## 决策

{{描述做出的决策}}

## 后果

### 正面
- {{优点1}}
- {{优点2}}

### 负面
- {{缺点1}}
- {{风险1}}

### 中性
- {{中性影响}}
```

---

## 模板适配规则

生成规范时，根据用户的技术栈选择适配：

### 前端框架适配

| 框架 | 状态管理 | 路由 | HTTP | 样式方案 |
|------|----------|------|------|----------|
| Flutter | Riverpod | go_router | dio | ThemeData |
| React | Zustand/Redux | React Router | axios/fetch | Tailwind/CSS-in-JS |
| Vue 3 | Pinia | Vue Router | axios | CSS 变量/Tailwind |
| Svelte | Svelte Stores | SvelteKit | fetch | CSS 变量 |
| Angular | NgRx/Services | Angular Router | HttpClient | CSS/SCSS |

### 后端框架适配

| 框架 | ORM | 校验 | 日志 | 测试 |
|------|-----|------|------|------|
| Fastify | Prisma | zod | pino | vitest |
| Express | Prisma/TypeORM | zod/joi | winston | jest/vitest |
| FastAPI | SQLAlchemy | pydantic | logging | pytest |
| Django | Django ORM | Django Forms | logging | pytest |
| Spring Boot | JPA/Hibernate | Bean Validation | SLF4J | JUnit |
| Gin | GORM | go-playground/validator | zap | testing |

### 数据库适配

| 数据库 | 迁移工具 | 备份命令 |
|--------|----------|----------|
| PostgreSQL | Prisma Migrate / pg_dump | pg_dump -Fc |
| MySQL | Prisma Migrate / mysqldump | mysqldump |
| MongoDB | mongock / mongodump | mongodump |
| SQLite | Prisma Migrate | cp database.db |
```

