# 学习计划管理系统 (MyStudyPlanSystem)

一个基于 ASP.NET Core 的学习计划管理系统，支持学生、教师和管理员三种角色，提供课程管理、学习计划制定、消息通知等功能。

## 功能特性

### 学生功能
- 浏览和查看课程详情
- 创建和管理个人学习计划
- 跟踪学习任务进度
- 查看和回复消息

### 教师功能
- 创建和管理课程
- 添加课程任务和资源
- 查看学生学习进度报告
- 发送消息给学生

### 管理员功能
- 用户管理（查看、管理所有用户）
- 系统设置
- 管理公告

## 技术栈

- **框架**: ASP.NET Core 8.0 (Razor Pages)
- **数据库**: SQL Server
- **ORM**: Entity Framework Core 8.0
- **认证**: Cookie Authentication
- **前端**: HTML/CSS/JavaScript

## 项目结构

```
MyStudyPlanSystem/
├── Data/                    # 数据库上下文
│   └── AppDbContext.cs
├── Models/                  # 实体模型
│   ├── User.cs              # 用户模型
│   ├── Course.cs            # 课程模型
│   ├── StudyPlan.cs         # 学习计划模型
│   ├── Message.cs           # 消息模型
│   └── ...
├── Pages/                   # Razor 页面
│   ├── Account/             # 账号管理
│   ├── Admin/               # 管理员页面
│   ├── Student/             # 学生页面
│   ├── Teacher/             # 教师页面
│   ├── Messages/            # 消息页面
│   └── Shared/              # 共享组件
├── Utils/                   # 工具类
├── wwwroot/                 # 静态资源
├── CreateDatabase.sql       # 数据库创建脚本
├── appsettings.json         # 应用配置
├── Program.cs               # 应用入口
└── MyStudyPlanSystem.csproj # 项目文件
```

## 快速开始

### 环境要求

- .NET 8.0 SDK
- SQL Server (LocalDB 或完整版本)

### 安装步骤

1. **克隆项目**

```bash
git clone https://github.com/yourusername/MyStudyPlanSystem.git
cd MyStudyPlanSystem
```

2. **配置数据库连接**

修改 `appsettings.json` 中的连接字符串：

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=YOUR_SERVER;Database=StudyPlanDB;Trusted_Connection=True;TrustServerCertificate=True"
  }
}
```

3. **创建数据库**

执行 `CreateDatabase.sql` 脚本创建数据库和表结构：

```sql
-- 使用 SQL Server Management Studio 或命令行执行
sqlcmd -S YOUR_SERVER -i CreateDatabase.sql
```

4. **运行应用**

```bash
dotnet run
```

应用将在 `https://localhost:5001` 启动。

### 默认用户

系统启动后，需要通过注册页面创建用户。支持三种角色：
- **Student** - 学生
- **Teacher** - 教师  
- **Admin** - 管理员

## 使用说明

### 用户注册与登录

1. 访问首页，点击"注册"链接
2. 填写用户名（8位数字）、密码和姓名
3. 选择角色完成注册
4. 返回登录页面登录系统

### 角色权限

| 页面/功能 | 学生 | 教师 | 管理员 |
|-----------|------|------|--------|
| 课程浏览 | ✓ | ✓ | ✓ |
| 学习计划 | ✓ | ✗ | ✗ |
| 课程管理 | ✗ | ✓ | ✓ |
| 用户管理 | ✗ | ✓ | ✓ |
| 系统设置 | ✗ | ✗ | ✓ |
| 消息系统 | ✓ | ✓ | ✓ |

## 数据库架构

### 主要表

- `Users` - 用户表（用户名、密码、角色、专业等）
- `Courses` - 课程表（课程代码、名称、描述、教师）
- `CourseTasks` - 课程任务表（任务名称、预估学时、资源链接）
- `StudyPlans` - 学习计划表（计划名称、日期范围、关联课程）
- `PlanTasks` - 计划任务表（任务完成状态、备注）
- `Messages` - 消息表（发送者、接收者、主题、内容）
- `MessageReplies` - 消息回复表
- `Announcements` - 公告表

### 关系图

```
Users ──(1:N)──> Courses ──(1:N)──> CourseTasks
Users ──(1:N)──> StudyPlans ──(1:N)──> PlanTasks
PlanTasks ──(N:1)──> CourseTasks
Users ──(1:N)──> Messages ──(1:N)──> MessageReplies
```

## 开发说明

### 开发环境

- 推荐使用 Visual Studio 2022 或 Rider
- 支持 VS Code 配合 C# 扩展

### 构建命令

```bash
# 构建项目
dotnet build

# 发布项目
dotnet publish -c Release -o publish
```

### 代码规范

- 遵循 .NET 命名规范
- 使用 nullable reference types
- 异步操作使用 `async/await`
- 数据库操作使用 Entity Framework Core

## 已知限制

- **密码存储**: 当前版本中用户密码以明文形式存储在数据库中。建议在生产环境中使用密码哈希算法（如 BCrypt）进行加密存储。
- **测试项目**: 目前项目暂无单元测试，建议后续添加测试用例。

## 许可证

MIT License

## 贡献

欢迎提交 Issue 和 Pull Request！

## 联系方式

如有问题或建议，请通过 GitHub Issues 联系。
