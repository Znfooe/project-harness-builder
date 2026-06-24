---
name: "project-harness-builder"
description: "Builds complete project harness with all engineering specs through interactive Q&A. Invoke when starting a new large project, setting up comprehensive specifications, or initializing project documentation framework from scratch."
---

# Project Harness Builder

通过交互式问答，为大型长期项目构建完整的工程规范体系（harness）。**增量式生成**：每轮问答后立即生成对应规范文档，防止上下文过长。全部完成后生成"提示词"文件夹，包含多段开发提示词供后续分段开发使用。

## When to Use

**CRITICAL: Invoke this skill IMMEDIATELY when:**

- 用户要创建新项目并需要完整规范体系
- 用户说"构建项目规范"、"初始化 harness"、"搭建工程框架"
- 用户要为新项目生成所有工程文档（spec、ADR、设计令牌等）
- 用户要从零开始搭建大型长期项目的文档和规范基础

**DO NOT:**

- 不要在已有完整规范体系的项目上运行（会覆盖现有文件）
- 不要用于小型/临时项目（过度工程化）
- 不要跳过交互问答阶段直接生成（需要用户输入确定技术栈）

## Language Rule

**CRITICAL**: 检测用户输入语言。所有生成的内容 — 文档、注释、规范、提示词 — 必须使用与用户相同的语言。

- 用户用中文 → 所有生成文档用中文，技术术语保留英文
- 用户用英文 → 所有生成文档用英文
- 此规则覆盖下方所有中文模板

## Prerequisites

本 skill 目录下有以下参考文件，运行时必须读取：

1. **`checklist.md`** — 大项目规范完整清单（51 项），用于确定需要创建哪些规范
2. **`spec-templates.md`** — 各类规范的模板结构和内容指引

运行时先读取这两个文件，再开始交互问答。

---

## Workflow

### 核心原则：增量式生成

**传统方式的问题**：全部问完再一次性生成 → 上下文过长，后期生成时前面的回答可能被压缩或遗忘。

**本 skill 的方式**：每轮问答结束后，**立即生成该轮对应的规范文档**。这样：
- 每份文档生成时，该轮的回答在上下文中是最清晰的
- 文档落盘后，后续轮次不需要重复记住前面的细节
- 防止上下文窗口溢出导致生成质量下降

---

### Phase 1: 增量问答与生成

**核心原则：一次只问一轮，等用户回答后立即生成对应文档，再进入下一轮。** 使用 `AskUserQuestion` 工具进行结构化提问，普通开放问题直接用文本提问。

#### Round 1: 项目基础 → 生成基础文档

**询问**：

1. **项目名称** — "你的项目叫什么名字？"
2. **项目描述** — "用 1-2 句话描述项目做什么？"
3. **项目类型** — 用 AskUserQuestion:
   - Web 应用（前端 + 后端）
   - 仅前端应用（SPA / SSG）
   - 仅后端 API 服务
   - 移动端应用
   - 全栈应用（前端 + 后端 + 管理后台）
   - 库 / SDK
   - CLI 工具

**回答后立即生成**：
- `docs/TECH-STACK.md` — 技术栈总览（初版，记录项目名称、描述、类型）
- `CONTEXT.md` — 领域语言（基于项目描述提取核心术语）
- `docs/spec.md` — 功能规格文档（框架，用户后续填充细节）

**生成后简短汇报**："已生成 TECH-STACK.md（初版）、CONTEXT.md、spec.md。接下来了解技术栈。"

---

#### Round 2: 技术栈 → 更新技术栈文档 + 生成密钥管理

**询问**：

4. **前端框架** — 用 AskUserQuestion（根据项目类型提供选项）:
   - Flutter Web
   - React / Next.js
   - Vue 3 / Nuxt
   - Svelte / SvelteKit
   - Angular
   - 无前端

5. **后端框架** — 用 AskUserQuestion:
   - Node.js + Fastify / Express
   - Python + FastAPI / Django
   - Go + Gin / Echo
   - Java + Spring Boot
   - Rust + Axum
   - 无后端

6. **数据库** — 用 AskUserQuestion:
   - PostgreSQL
   - MySQL
   - MongoDB
   - SQLite
   - Redis（缓存）
   - 无数据库

7. **是否有管理后台？** — 是/否。如果是，用什么框架？（如 vue-vben-admin、react-admin 等）

8. **其他关键技术** — 开放问题："还有什么关键技术需要纳入？如 ORM、认证方式、第三方服务等"

**回答后立即生成/更新**：
- **更新** `docs/TECH-STACK.md` — 补充完整技术栈（前端/后端/数据库/管理后台/ORM/认证/第三方）
- **生成** `docs/secrets-management.md` — 敏感信息管理规范（根据技术栈定制三层密钥策略）

**生成后简短汇报**："已更新 TECH-STACK.md（完整版），生成 secrets-management.md。接下来了解设计偏好。"

---

#### Round 3: 设计与体验 → 生成设计规范（仅在有前端时）

这一轮收集设计偏好，用于生成有项目特色的 `design-tokens.md`、`layout-principles.md`、`animation-spec.md`。

**询问**：

9. **主题模式** — 用 AskUserQuestion:
   - 仅浅色主题
   - 仅深色主题
   - 浅色 + 深色双主题（推荐）
   - 跟随系统

10. **品牌主色** — 用 AskUserQuestion:
    - 蓝色系（专业/科技感，如 #2563EB）
    - 绿色系（健康/自然，如 #16A34A）
    - 紫色系（创意/年轻，如 #7C3AED）
    - 橙色系（活力/温暖，如 #EA580C）
    - 红色系（热情/警示，如 #DC2626）
    - 自定义（用户提供色值）

11. **视觉风格** — 用 AskUserQuestion:
    - 极简主义（大量留白、克制色彩、细线分割）
    - Material Design（Google 风格、elevation 层次、阴影）
    - 拟物/新拟态（soft UI、柔和阴影、立体感）
    - 玻璃拟态（glassmorphism、毛玻璃、半透明）
    - Bento Grid（网格卡片、模块化、信息密集）
    - 粗犷主义（brutalism、强对比、粗边框、反传统）
    - 尚未确定（由 skill 根据项目类型推荐）

12. **排版密度** — 用 AskUserQuestion:
    - 紧凑（信息密集型，如数据仪表盘）
    - 舒适（标准，适合大多数应用）
    - 宽松（大量留白，适合展示型/品牌型）

13. **字体偏好** — 用 AskUserQuestion:
    - 无衬线（Inter / system-ui，现代简洁）
    - 衬线 + 无衬线混搭（标题衬线 + 正文无衬线，编辑感）
    - 等宽强调（数据/代码为主，JetBrains Mono）
    - 自定义（用户提供字体名）

14. **动效风格** — 用 AskUserQuestion:
    - 极简动效（仅必要过渡，≤150ms，专业感）
    - 适度微交互（hover/active 反馈 + 页面过渡，推荐）
    - 丰富动效（逐字动画、弹性效果、装饰性动画）
    - 沉浸动效（全屏过渡、视差滚动、3D 效果）

15. **圆角偏好** — 用 AskUserQuestion:
    - 锐利（直角为主，2-4px，技术感/严肃）
    - 适中（8-12px，友好但不幼稚，推荐）
    - 圆润（16-24px，活泼/消费级）
    - 药丸形（全圆角，按钮/标签）

16. **是否有现成品牌规范？** — 是/否。如果是，询问：
    - Logo 文件位置
    - 品牌色色值
    - 字体规范
    - 任何视觉禁忌（不能用什么颜色/风格）

17. **设计参考** — 开放问题："有没有喜欢的设计参考？如某个网站的风格、某个产品的 UI。提供链接或描述即可，skill 会据此调整设计令牌。"

**回答后立即生成**（用设计偏好定制，非通用模板）：
- **生成** `docs/design-tokens.md` — 设计令牌
  - 品牌主色 → 生成 brand50-brand900 色阶
  - 主题模式 → 决定生成几套语义色映射
  - 排版密度 → 调整间距倍率（紧凑 0.75x / 舒适 1x / 宽松 1.25x）
  - 圆角偏好 → 调整 radiusSm/Md/Lg/Xl 具体值
  - 字体偏好 → 设置 fontSans/fontSerif/fontMono
  - 动效风格 → 调整 durationFast/Normal/Slow
  - 视觉风格 → 调整阴影风格
  - 如有设计参考链接 → 用 WebFetch 分析参考站点特征，融入令牌
- **生成** `docs/layout-principles.md` — 排版规范（根据视觉风格和排版密度定制）
- **生成** `docs/animation-spec.md` — 动效规范（根据动效风格定制时长基准和适用场景）

**生成后简短汇报**："已生成 design-tokens.md、layout-principles.md、animation-spec.md（均基于你的设计偏好定制）。接下来了解项目规模。"

---

#### Round 4: 规模与团队 → 记录优先级（不生成文档）

**询问**：

18. **预期团队规模** — 用 AskUserQuestion:
    - 个人项目（1 人）
    - 小团队（2-5 人）
    - 中团队（6-15 人）
    - 大团队（15+ 人）

19. **项目周期** — 用 AskUserQuestion:
    - 短期（< 3 个月）
    - 中期（3-12 个月）
    - 长期（1 年以上）

20. **性能敏感度** — 用 AskUserQuestion:
    - 不敏感（普通 CRUD 应用）
    - 中等（有实时性要求）
    - 极度敏感（如计时、游戏、高频交易）

21. **部署方式** — 用 AskUserQuestion:
    - 云平台（Vercel / Netlify / Cloudflare）
    - 自建服务器（Docker / K8s）
    - 混合部署
    - 尚未确定

**回答后不生成文档，但记录用于**：
- 过滤规范优先级（个人项目降 P2，短期项目只 P0，长期项目 P0+P1）
- 性能敏感 → performance-spec 提升到 P0
- 影响后续提示词的粒度（大团队/长期项目 → 提示词更多更细）

**简短确认**："了解。接下来了解特殊需求。"

---

#### Round 5: 特殊需求 → 生成按需规范

**询问**：

22. **是否需要多语言支持？** 是/否
23. **是否需要可访问性（a11y）规范？** 是/否
24. **是否有合规要求？**（GDPR、等保等）是/否
25. **还有什么特殊需求？** — 开放问题

**回答后立即生成**（按需）：
- 如需多语言 → **生成** `docs/i18n-spec.md` — 国际化规范
- 如需 a11y → **生成** `docs/accessibility-spec.md` — 可访问性规范
- 如需合规 → **生成** `docs/compliance-spec.md` — 合规规范
- 如有其他特殊需求 → 记录到 `docs/spec.md` 对应章节

**生成后简短汇报**："已生成特殊需求规范。接下来了解前后端与 API 细节。"

---

#### Round 6: 前后端与 API 细节 → 生成工程规范

这一轮收集工程细节偏好，用于生成有项目特色的 `frontend-spec.md`、`backend-spec.md`、`api-spec.md`。**仅当项目有对应端时询问相关子问题。**

**前端部分（如有前端）**：

26. **前端命名规范** — 用 AskUserQuestion:
    - 文件名 kebab-case + 组件 PascalCase（React/Vue 主流）
    - 文件名 snake_case + 组件 PascalCase（Flutter/Dart 主流）
    - 文件名 camelCase + 组件 PascalCase
    - 尚未确定（由 skill 根据框架推荐）

27. **组件粒度** — 用 AskUserQuestion:
    - 原子化（atoms/molecules/organisms，Atomic Design）
    - 功能化（页面/组件/布局三层，简单实用）
    - 领域化（按业务领域分组，适合大型项目）
    - 尚未确定

28. **状态管理细节** — 开放问题："状态管理有什么偏好？如是否用全局 store、是否用服务端状态缓存（React Query/SWR）、是否需要状态持久化？"

29. **前端性能策略** — 用 AskUserQuestion:
    - 代码分割 + 懒加载（默认）
    - 预加载关键路由
    - SSR/SSG（如框架支持）
    - 无特殊要求

**后端部分（如有后端）**：

30. **后端分层架构** — 用 AskUserQuestion:
    - 三层（Route → Service → Model，标准）
    - 四层（Route → Service → Repository → Model，领域复杂时）
    - DDD（Domain/Application/Infrastructure，大型项目）
    - 六边形架构（端口与适配器）
    - 尚未确定

31. **后端日志方案** — 用 AskUserQuestion:
    - 结构化 JSON 日志（pino/winston/zap，推荐）
    - 纯文本日志
    - 接入 ELK/Loki（后续）
    - 尚未确定

32. **后端错误处理策略** — 用 AskUserQuestion:
    - 统一错误类 + 全局异常中间件（推荐）
    - 每层 try/catch
    - Result/Either 模式（函数式）
    - 尚未确定

**API 部分（如有后端）**：

33. **API 响应格式** — 用 AskUserQuestion:
    - `{ code, message, data }` 包裹式（统一格式，推荐）
    - RESTful 原生（直接返回数据，用 HTTP 状态码）
    - GraphQL
    - 混合（列表用包裹式，详情用原生）

34. **API 版本策略** — 用 AskUserQuestion:
    - URL 路径版本（/api/v1/，简单明确，推荐）
    - Header 版本（Accept: application/vnd.api+json;version=1）
    - 查询参数版本（?version=1）
    - 无版本（小项目）

35. **API 认证方式** — 用 AskUserQuestion（可多选）:
    - JWT（Access + Refresh Token）
    - Session + Cookie
    - OAuth 2.0（GitHub/Google 等第三方）
    - API Key（仅内部/服务间）
    - 无认证（公开 API）

36. **API 文档方案** — 用 AskUserQuestion:
    - OpenAPI/Swagger 自动生成
    - 手写 Markdown
    - TypeDoc / 类型推导
    - 暂不需要

**回答后立即生成**（用工程偏好定制，非通用模板）：
- 如有前端 → **生成** `docs/frontend-spec.md` — 前端代码规范（命名/组件粒度/状态管理/性能策略）
- 如有后端 → **生成** `docs/backend-spec.md` — 后端代码规范（分层/日志/错误处理）
- 如有后端 → **生成** `docs/api-spec.md` — API 设计规范（响应格式/版本/认证/文档）

**生成后简短汇报**："已生成前端/后端/API 规范（均基于你的工程偏好定制）。接下来了解数据库与安全细节。"

---

#### Round 7: 数据库与安全细节 → 生成数据库和安全规范

**仅当项目有数据库/后端时询问。**

**数据库部分（如有数据库）**：

37. **数据库命名规范** — 用 AskUserQuestion:
    - snake_case 复数表名 + snake_case 列名（PostgreSQL 主流，推荐）
    - camelCase（部分 ORM 默认）
    - PascalCase（SQL Server 风格）
    - 尚未确定

38. **主键策略** — 用 AskUserQuestion:
    - 自增整数（BIGSERIAL/IDENTITY，简单）
    - UUID v4（分布式友好，无序）
    - UUID v7 / ULID（分布式 + 有序，推荐新项目）
    - 雪花算法（Snowflake，有序 + 分布式）

39. **软删除策略** — 用 AskUserQuestion:
    - 软删除（deleted_at 字段，可恢复）
    - 硬删除（直接 DELETE）
    - 混合（用户数据软删除，日志硬删除）
    - 尚未确定

40. **时间戳策略** — 用 AskUserQuestion:
    - UTC + TIMESTAMPTZ（推荐，时区安全）
    - 本地时区 + TIMESTAMP
    - Unix 毫秒时间戳（BIGINT）
    - 尚未确定

41. **迁移管理** — 用 AskUserQuestion:
    - ORM 内置迁移（Prisma Migrate / Alembic / Flyway）
    - 手写 SQL 迁移
    - 已有迁移工具（用户提供）
    - 尚未确定

**安全部分（如有后端）**：

42. **密码加密策略** — 用 AskUserQuestion:
    - bcrypt（saltRounds=12，主流推荐）
    - argon2id（更安全，新项目推荐）
    - scrypt
    - 尚未确定

43. **Token 存储位置** — 用 AskUserQuestion:
    - HttpOnly Cookie（防 XSS，推荐）
    - localStorage（简单但易受 XSS）
    - 内存 + Refresh Token in Cookie
    - 尚未确定

44. **CORS 策略** — 用 AskUserQuestion:
    - 白名单域名（推荐）
    - 同源（最严格）
    - 允许特定方法/头
    - 尚未确定（开发期宽松，生产期严格）

45. **限流策略** — 用 AskUserQuestion:
    - 按接口分级限流（登录/注册/查询分别限流，推荐）
    - 全局统一限流
    - 按用户限流
    - 暂不限流（小项目）

46. **审计日志** — 用 AskUserQuestion:
    - 记录所有写操作（增删改，推荐）
    - 仅记录敏感操作（登录/权限变更/数据导出）
    - 不记录
    - 尚未确定

47. **敏感数据脱敏** — 用 AskUserQuestion:
    - 邮箱/手机号/身份证自动脱敏（推荐）
    - 仅日志脱敏
    - 不脱敏
    - 尚未确定

**回答后立即生成**（用偏好定制，非通用模板）：
- 如有数据库 → **生成** `docs/database-spec.md` — 数据库规范（命名/主键/软删除/时间戳/迁移）
- 如有后端 → **生成** `docs/security-spec.md` — 安全规范（密码/Token/CORS/限流/审计/脱敏）

**生成后简短汇报**："已生成数据库和安全规范。接下来了解测试和运维细节。"

---

#### Round 8: 测试/CI/CD/部署/性能细节 → 生成质量运维规范

**测试部分**：

48. **测试覆盖率要求** — 用 AskUserQuestion:
    - 严格（Service ≥80%、组件 ≥60%、总体 ≥70%，推荐长期项目）
    - 标准（Service ≥60%、总体 ≥50%）
    - 宽松（仅核心逻辑测试，无覆盖率要求）
    - 尚未确定

49. **E2E 测试方案** — 用 AskUserQuestion:
    - Playwright（推荐，跨浏览器）
    - Cypress（仅 Chromium，开发体验好）
    - Selenium（传统，生态成熟）
    - 暂不需要 E2E（小项目）

50. **测试数据管理** — 用 AskUserQuestion:
    - Factory 模式 + 事务回滚（推荐，隔离性好）
    - 固定种子数据（简单但易耦合）
    - Mock 所有外部依赖（单元测试用）
    - 尚未确定

**CI/CD 部分**：

51. **CI/CD 平台** — 用 AskUserQuestion:
    - GitHub Actions（推荐，与 GitHub 集成）
    - GitLab CI
    - Jenkins
    - Drone / CircleCI
    - 暂不需要 CI/CD（小项目）

52. **部署触发方式** — 用 AskUserQuestion:
    - main 分支 push 自动部署（推荐）
    - Tag 发布后手动触发部署
    - PR 合并后自动部署
    - 仅手动部署

53. **制品管理** — 用 AskUserQuestion:
    - Docker 镜像 + Registry（推荐容器化项目）
    - 静态产物 + CDN（前端项目）
    - 源码直接部署（小项目）
    - 尚未确定

**部署部分**：

54. **环境划分** — 用 AskUserQuestion（可多选）:
    - local（本地开发）
    - development（开发联调）
    - staging（预发布）
    - production（生产）

55. **部署策略** — 用 AskUserQuestion:
    - 滚动部署（推荐，零停机）
    - 蓝绿部署（快速回滚，资源占用高）
    - 金丝雀发布（渐进式，大项目推荐）
    - 直接替换（小项目，有停机）

56. **回滚策略** — 用 AskUserQuestion:
    - 自动回滚（健康检查失败自动回滚，推荐）
    - 手动回滚（人工确认）
    - 保留最近 N 个版本（N=5）

**性能部分**：

57. **性能预算严格度** — 用 AskUserQuestion:
    - 严格（LCP ≤2.5s、FCP ≤1.8s、API P95 ≤200ms、FPS ≥60，推荐性能敏感项目）
    - 标准（LCP ≤4s、API P95 ≤500ms）
    - 宽松（无明确预算，尽力优化）
    - 尚未确定

58. **性能监控方案** — 用 AskUserQuestion（可多选）:
    - 前端 RUM（Sentry / Datadog RUM）
    - 后端 APM（Sentry / New Relic / Prometheus）
    - 合成监控（Lighthouse CI 定时跑）
    - 暂不监控（小项目）

59. **性能测试方案** — 用 AskUserQuestion:
    - Lighthouse CI（每次 PR 跑，前端）
    - k6 / autocannon（发布前压测，后端）
    - 两者都要（推荐全栈项目）
    - 暂不需要（小项目）

**回答后立即生成**（用偏好定制，非通用模板）：
- **生成** `docs/testing-spec.md` — 测试规范（覆盖率/E2E/测试数据）
- **生成** `docs/cicd-spec.md` — CI/CD 规范（平台/触发/制品）
- **生成** `docs/deployment-spec.md` — 部署规范（环境/策略/回滚）
- **生成** `docs/performance-spec.md` — 性能规范（预算/监控/测试）
- **生成** `docs/git-spec.md` — Git 规范（分支策略/提交信息/PR 规范）

**生成后简短汇报**："已生成测试/CI-CD/部署/性能/Git 规范。所有规范文档生成完毕，进入项目初始化阶段。"

---

### Phase 2: 补全与初始化

所有规范文档生成后，补全项目入口文件并初始化项目结构：

#### 1. 生成 CLAUDE.md（项目入口指南）

汇总所有已生成的规范文档，创建 `CLAUDE.md`：
- 项目名称和描述
- 必读文档清单（按优先级编号）
- 强制规则（技术栈/敏感信息/颜色/字号/间距/术语）
- 文档索引表

#### 2. 生成 ADR（架构决策记录）

- 创建 `docs/adr/` 目录
- 生成 `docs/adr/0001-technology-stack-selection.md` — 记录技术栈选型决策
- 如有设计决策 → 生成 `docs/adr/0002-design-decisions.md`
- 如有架构决策 → 生成 `docs/adr/0003-architecture-decisions.md`

#### 3. 生成 .gitignore

根据技术栈自动生成（参考 `spec-templates.md` 的 .gitignore 规则）：
- **Node.js**: `node_modules/`, `dist/`, `.env`
- **Flutter/Dart**: `.dart_tool/`, `.flutter-plugins`, `build/`, `*.g.dart`
- **Python**: `__pycache__/`, `.venv/`, `*.pyc`
- **Go**: `*.exe`, `*.dll`
- **Java**: `target/`, `*.class`, `.gradle/`
- **通用**: `.env`, `*.pem`, `*.key`, `.idea/`, `.vscode/`, `.DS_Store`, `Thumbs.db`
- **提示词**: `提示词/`（内部使用，不入库）

#### 4. 创建目录结构

根据项目类型创建标准目录：
- 全栈应用：`frontend/` + `backend/` + `admin/`（如有管理后台）
- 仅前端：`frontend/` 或项目根目录
- 仅后端：`backend/` 或项目根目录

#### 5. 初始化 Git（如尚未初始化）

```bash
git init
```

#### 6. 生成项目规范清单

- 创建 `docs/project-harness-checklist.md` — 复制本 skill 的 `checklist.md`，标记已创建的规范为 ✅

#### 7. 首次 Git 提交（询问用户）

```bash
git add .
git commit -m "chore: 初始化项目 harness 规范体系"
```

**初始化完成后汇报**："项目初始化完成。文件树如下：[展示文件树]。接下来生成开发提示词。"

---

### Phase 3: 开发提示词生成

**这是本 skill 的核心差异化功能**。全部规范生成完成后，在项目根目录生成 `提示词/` 文件夹，包含多段开发提示词，供用户后续分段发给 AI 进行开发。

#### 3.1 提示词设计原则

1. **质量优先，数量不限** — 根据项目规模决定提示词数量：
   - 小项目（仅前端或仅后端）：10-15 段
   - 中等项目（全栈）：15-25 段
   - 大型项目（全栈 + 管理后台 + 性能敏感）：25-40 段
   - 超大型项目（微服务/多端）：40+ 段
2. **每段提示词独立可执行** — 包含：角色设定、必读文档、前置条件、任务、步骤、验收标准、注意事项
3. **按依赖顺序编号** — 用户按编号顺序发给 AI，前一段完成后再发下一段
4. **标注并行可能性** — 互不依赖的阶段标注"可与阶段 X 并行"

#### 3.2 提示词生成流程

1. **分析项目规模和复杂度**
   - 读取 Round 4 的团队规模/项目周期/性能敏感度
   - 读取项目类型（全栈/仅前端/仅后端）
   - 确定提示词数量范围

2. **拆分开发阶段**
   按以下维度拆分（每个维度可能拆成多段）：
   - **地基搭建** — 每端一段（Flutter 地基、后端地基、管理后台地基）
   - **核心功能** — 每个核心功能一段（反应力测试、击杀测试、用户系统等）
   - **数据层** — 成绩提交、排行榜、趋势图各一段
   - **管理后台** — 用户管理、成绩管理、数据统计各一段
   - **质量保障** — 单元测试、集成测试、E2E 各一段
   - **性能优化** — 前端优化、后端优化各一段
   - **部署运维** — Docker、Nginx、CI/CD、监控各一段
   - **按需补充** — 多语言、a11y、合规等各一段

3. **生成使用说明**
   - 生成 `提示词/00-使用说明.md` — 说明使用方法、开发顺序、依赖关系、并行可能性

4. **逐段生成提示词**
   - 每段提示词保存为 `提示词/01-xxx.md`、`提示词/02-xxx.md`...
   - 每段包含完整结构（角色/必读文档/前置/任务/步骤/验收/注意事项）

5. **生成依赖关系图**
   - 在使用说明中用 ASCII 图展示阶段依赖关系
   - 标注哪些阶段可并行

#### 3.3 提示词模板结构

每段提示词必须包含以下结构：

```markdown
# 阶段 XX: [标题]

## 角色设定
你是 [项目名] 项目的 [角色]，负责 [职责]。

## 必读文档
开发前**必须**完整阅读以下文档（按优先级）：
1. `docs/xxx.md` — [说明]
2. `docs/yyy.md` — [说明]
...

## 前置条件
- 阶段 XX 已完成：[说明]
- [其他前置]

## 本阶段任务
[一句话概括目标]

## 具体步骤
### 1. [步骤标题]
[详细步骤，包含文件路径、代码结构]

### 2. [步骤标题]
...

## 验收标准
- [ ] [可验证的检查项]
- [ ] [可验证的检查项]
...

## 注意事项
1. [关键约束]
2. [常见陷阱]
...
```

#### 3.4 提示词生成检查清单

生成完成后，自检以下项目：
- [ ] `提示词/00-使用说明.md` 存在，包含开发顺序和依赖图
- [ ] 每段提示词编号连续（01, 02, 03...）
- [ ] 每段提示词包含完整的 7 个部分（角色/必读/前置/任务/步骤/验收/注意）
- [ ] 必读文档引用的文件确实存在于项目中
- [ ] 前置条件引用的阶段编号正确
- [ ] 验收标准可验证（非模糊描述）
- [ ] 提示词数量与项目规模匹配（小项目 10-15，大项目 25-40+）
- [ ] 依赖关系图正确标注并行可能性
- [ ] `.gitignore` 已包含 `提示词/`（内部使用不入库）

#### 3.5 完成汇报

生成完成后，向用户展示：
```
开发提示词已生成完毕！

## 提示词清单（共 N 段）

| 阶段 | 标题 | 范围 | 依赖 |
|------|------|------|------|
| 01 | xxx | xxx | 无 |
| 02 | xxx | xxx | 无（可与 01 并行） |
| 03 | xxx | xxx | 01 |
...

## 使用方法
1. 按 00-使用说明.md 的顺序，逐段复制提示词发给 AI
2. 每段完成后验证验收标准，再进入下一段
3. 标注"可并行"的阶段可同时进行（用不同 AI 会话）

## 依赖关系图
[ASCII 依赖图]

提示词文件夹已加入 .gitignore，不会提交到 Git。
```

---

## Output Format

### 交互问答阶段（增量式）
- 使用 `AskUserQuestion` 工具进行结构化问题
- 开放问题用文本提问，以"："结尾
- **每轮回答后立即生成对应文档**，简短汇报生成结果
- 不要长篇大论，汇报控制在 2-3 句

### 项目初始化阶段
- 展示创建的目录结构
- 询问是否进行首次 Git 提交

### 提示词生成阶段
- 展示提示词清单表格
- 展示依赖关系图
- 说明使用方法

---

## Critical Rules

1. **不要跳过问答** — 必须通过问答了解项目，不能假设技术栈
2. **一次一轮** — 不要一次性列出所有问题，逐轮进行
3. **增量生成** — 每轮问答后立即生成对应文档，不要全部问完再生成
4. **适应用户技术栈** — 不要硬套某个框架的规范，根据用户选择调整
5. **不生成无关规范** — 无前端不生成 frontend-spec，无数据库不生成 database-spec
6. **语言一致** — 用户用什么语言，生成的文档和提示词就用什么语言
7. **引用 checklist.md** — 规划阶段必须读取 checklist.md
8. **引用 spec-templates.md** — 生成阶段必须读取 spec-templates.md 获取模板
9. **进度透明** — 用 TodoWrite 跟踪，每轮生成后简短汇报
10. **不覆盖已有文件** — 如果文件已存在，询问用户是否覆盖
11. **设计定制不可跳过** — 有前端的项目必须完成 Round 3 设计问答；生成 design-tokens.md / layout-principles.md / animation-spec.md 时必须用设计偏好定制，不能套用通用模板值
12. **设计参考要分析** — 如用户提供设计参考链接，必须用 WebFetch 分析参考站点特征并融入令牌，不能只记录链接
13. **工程定制不可跳过** — 有前端必须完成 Round 6 前端部分；有后端必须完成 Round 6 后端+API 部分；有数据库/后端必须完成 Round 7；生成工程规范时必须用偏好定制，不能套用通用模板值
14. **按端过滤问题** — Round 6/7 的问题按项目类型过滤：无前端跳过前端部分，无后端跳过后端+API+安全部分，无数据库跳过数据库部分
15. **质量运维定制不可跳过** — 必须完成 Round 8；生成质量运维规范时必须用偏好定制，不能套用通用模板值
16. **小项目可简化** — 如用户选择"暂不需要 CI/CD""暂不监控""暂不需要 E2E"等，对应规范可简化为"本项目暂不采用 X，后续按需引入"，但仍需生成文件说明决策
17. **提示词质量优先** — 提示词数量根据项目规模决定（10-40+），每段必须独立可执行，包含完整的 7 个部分
18. **提示词加入 .gitignore** — `提示词/` 文件夹是内部开发工具，不提交 Git，生成 .gitignore 时必须包含
19. **增量生成防上下文溢出** — 每轮生成文档后，后续轮次不需要重复记住前面的细节，文档已落盘

---

## Example Session

```
用户: 我想创建一个新项目，需要完整的规范体系

Assistant: [调用本 skill，读取 checklist.md 和 spec-templates.md]
好的，我来帮你构建完整的项目规范体系。我会分轮询问，每轮问完立即生成对应文档。先了解项目基础。

[AskUserQuestion: 项目名称？项目描述？项目类型？]

用户: 项目叫 DataFlow，是一个数据分析平台，全栈应用

Assistant: 了解。立即生成基础文档...
[生成 docs/TECH-STACK.md（初版）、CONTEXT.md、docs/spec.md]
已生成 3 份基础文档。接下来了解技术栈。

[AskUserQuestion: 前端框架？后端框架？数据库？管理后台？]

用户: React + Node.js + PostgreSQL，需要管理后台用 vue-vben-admin

Assistant: 了解。立即更新技术栈文档并生成密钥管理规范...
[更新 docs/TECH-STACK.md（完整版）、生成 docs/secrets-management.md]
已生成 2 份文档。接下来了解设计偏好。

[AskUserQuestion: 主题模式？品牌主色？视觉风格？...]

用户: 双主题，蓝色系，极简主义，舒适密度，无衬线，适度微交互，适中圆角

Assistant: 了解。立即生成设计规范（基于你的偏好定制）...
[生成 docs/design-tokens.md（蓝色系色阶/双主题/适中圆角）、docs/layout-principles.md（极简/舒适）、docs/animation-spec.md（适度微交互）]
已生成 3 份设计文档。接下来了解项目规模。

[AskUserQuestion: 团队规模？项目周期？性能敏感度？部署方式？]

用户: 中团队，长期项目，中等性能要求，云部署

...（继续 Round 5-8，每轮生成对应文档）...

Assistant: 所有规范文档生成完毕（共 19 份）。进入项目初始化...
[生成 CLAUDE.md、ADR、.gitignore、目录结构、project-harness-checklist.md]
项目初始化完成。接下来生成开发提示词。

[分析项目规模：全栈 + 管理后台 + 长期项目 → 预计 25 段提示词]
[生成 提示词/00-使用说明.md、提示词/01-xxx.md ... 提示词/25-xxx.md]

开发提示词已生成完毕！共 25 段，按顺序发给 AI 即可分段开发。
[展示提示词清单表格和依赖关系图]
提示词文件夹已加入 .gitignore，不会提交到 Git。
```
