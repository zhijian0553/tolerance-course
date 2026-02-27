# 公差配合与测量技术 - 在线课程系统

## 项目简介

这是一个为中等职业教育设计的《公差配合与测量技术》在线教学网页系统，支持手机端使用，符合AI赋能职业教育政策要求。

## 功能特点

### 1. 课程内容系统
- **9个完整章节**：涵盖公差配合与测量技术核心内容
- 每章包含：主题内容、重点难点突破、例题讲解、课堂练习、产教融合案例
- 每章20道课后作业题

### 2. AI智能助教
- 智能问答：基于课程知识库的常见问题解答
- 智能总结：自动生成章节要点
- 学情分析：跟踪学习进度
- 产教案例：展示行业应用

### 3. 学生管理系统
- 支持6个班级：机器人241班、智能242班、数控255班、数控243班、数控256班、数控251班
- 学生可自助注册加入班级
- 学习进度自动记录

### 4. 作业系统
- 每章20道课后作业
- 自动记录提交状态
- 教师可查看各班级作业完成情况

### 5. 教师管理后台
- 查看各班级学生作业提交情况
- 一目了然哪些学生未交作业
- 支持数据导出

## 部署方法

### 方法一：直接打开（最简单）
直接双击 `index.html` 文件在浏览器中打开即可使用。数据存储在浏览器本地存储中。

### 方法二：使用本地服务器

#### 使用 Python（如果已安装）
```bash
cd tolerance-course
python -m http.server 8080
```
然后访问 http://localhost:8080

#### 使用 Node.js（如果已安装）
```bash
cd tolerance-course
npx serve
```

### 方法三：部署到静态网站托管

#### 部署到 GitHub Pages
1. 创建 GitHub 仓库
2. 上传所有文件
3. 在仓库设置中启用 GitHub Pages
4. 选择 main 分支作为源

#### 部署到 Vercel
1. 注册 Vercel 账号
2. 导入项目
3. 自动部署

#### 部署到 Netlify
1. 注册 Netlify 账号
2. 拖拽文件夹到上传区域
3. 自动获得访问地址

## Supabase 数据库配置

要启用云端数据存储功能：

1. 注册 Supabase 账号：https://supabase.com
2. 创建新项目
3. 在 SQL Editor 中运行以下建表语句：

```sql
-- 学生表
CREATE TABLE students (
    id TEXT PRIMARY KEY,
    name TEXT NOT NULL,
    className TEXT NOT NULL,
    studentId TEXT,
    createdAt TIMESTAMP DEFAULT NOW()
);

-- 作业提交表
CREATE TABLE homework_submissions (
    id SERIAL PRIMARY KEY,
    studentId TEXT NOT NULL,
    chapterId INTEGER NOT NULL,
    answers JSONB NOT NULL,
    score INTEGER,
    submittedAt TIMESTAMP DEFAULT NOW(),
    UNIQUE(studentId, chapterId)
);

-- 学习进度表
CREATE TABLE learning_progress (
    id SERIAL PRIMARY KEY,
    studentId TEXT NOT NULL,
    chapterId INTEGER NOT NULL,
    progress INTEGER DEFAULT 0,
    completed BOOLEAN DEFAULT FALSE,
    lastAccess TIMESTAMP DEFAULT NOW(),
    UNIQUE(studentId, chapterId)
);
```

4. 修改 `js/supabase-config.js` 中的配置：
```javascript
const SUPABASE_URL = '你的项目URL';
const SUPABASE_ANON_KEY = '你的anon密钥';
```

## 文件结构

```
tolerance-course/
├── index.html          # 主页面
├── admin.html          # 教师管理后台
├── styles.css          # 样式文件
├── data/
│   ├── chapters.js     # 课程章节内容
│   └── questions.js    # 练习题和作业题
├── js/
│   ├── app.js          # 主应用逻辑
│   ├── ai-assistant.js # AI助教功能
│   └── supabase-config.js # 数据库配置
└── package.json        # 项目配置
```

## 使用说明

### 学生使用
1. 打开网页，点击"登录"按钮
2. 输入姓名、选择班级
3. 浏览课程章节，学习内容
4. 完成课堂练习和课后作业
5. 使用AI助教获取帮助

### 教师使用
1. 访问 `admin.html` 进入管理后台
2. 查看各班级学生作业提交情况
3. 点击章节标签查看特定章节的提交情况
4. 导出数据生成报表

## 技术特点

- 纯前端实现，无需后端服务器
- 响应式设计，支持手机端
- 本地存储 + Supabase 云端存储双模式
- 符合AI赋能职业教育政策要求

## 课程章节

1. 绪论
2. 光滑圆柱体结合的极限与配合
3. 测量技术基础
4. 几何公差
5. 表面粗糙度
6. 滚动轴承的公差与配合
7. 键与花键的公差与配合
8. 螺纹的公差与配合
9. 圆柱齿轮公差

## 更新日志

- v1.0.0 - 初始版本发布
  - 完成9章课程内容
  - 实现AI助教功能
  - 实现作业系统
  - 实现教师管理后台
