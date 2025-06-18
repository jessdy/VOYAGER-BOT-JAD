# VOYAGER AUTO BOT - 自动化任务机器人

一个用于自动化执行 Voyager 平台日常任务的机器人，支持多账号管理和代理连接，包括任务完成、宝箱开启等功能。

## ✨ 主要功能

- 🤖 **自动化任务执行** - 自动完成 Voyager 平台的日常任务
- 🎁 **自动开启宝箱** - 每日自动开启奖励宝箱
- 👥 **多账号支持** - 同时管理多个钱包账号
- 🌐 **代理支持** - 支持 HTTP/HTTPS/SOCKS4/SOCKS5 代理
- 🔄 **智能重试** - 网络请求失败自动重试
- 📊 **美观界面** - 彩色日志和表格化数据展示
- ⏰ **定时循环** - 24小时自动循环执行

## 🛠️ 系统要求

- **Node.js** (版本 14 或更高)
- **npm** (Node 包管理器)
- **macOS/Linux/Windows** 操作系统

## 📦 安装步骤

1. **克隆项目**
   ```bash
   git clone https://github.com/jessdy/VOYAGER-BOT-JAD.git
   cd VOYAGER-BOT-JAD
   ```

2. **安装依赖**
   ```bash
   npm install
   ```

## ⚙️ 配置说明

### 1. 私钥配置 (必需)

创建 `pk.txt` 文件，每行一个钱包私钥：

```
privateKey1
privateKey2
privateKey3
...
```

⚠️ **安全提醒**: 请确保私钥安全，不要泄露给他人

### 2. 代理配置 (可选)

创建 `proxy.txt` 文件，每行一个代理地址：

```
socks5://username:password@IP:PORT
http://proxy.example.com:8080
https://secure-proxy.example.com:8443
...
```

**支持的代理格式**:
- `http://proxy:port`
- `https://proxy:port`
- `socks5://proxy:port`
- 带认证: `protocol://username:password@proxy:port`

## 🚀 使用方法

1. **启动机器人**
   
   **方式一：直接启动**
   ```bash
   npm start
   ```
   或
   ```bash
   node voyager.js
   ```
   
   **方式二：使用 PM2 (推荐生产环境)**
   ```bash
   # 安装 PM2
   npm install -g pm2
   
   # 启动机器人
   pm2 start voyager.js --name "voyager-bot"
   
   # 查看运行状态
   pm2 status
   
   # 查看日志
   pm2 logs voyager-bot
   
   # 停止机器人
   pm2 stop voyager-bot
   
   # 重启机器人
   pm2 restart voyager-bot
   
   # 删除进程
   pm2 delete voyager-bot
   
   # 设置开机自启
   pm2 startup
   pm2 save
   ```

2. **选择代理模式**
   - 启动时会询问是否使用代理
   - 输入 `y` 使用代理，`n` 直连

3. **自动执行**
   - 机器人会自动处理所有配置的账号
   - 完成任务后等待24小时再次执行
   - 可以随时按 `Ctrl+C` 停止

## 📋 功能详解

### 🔐 认证系统
- 使用以太坊钱包私钥进行 SIWE (Sign-In with Ethereum) 认证
- 自动获取认证载荷和签名
- 创建安全会话令牌

### 📝 任务管理
- 自动获取可用任务列表
- 智能判断任务状态
- 自动完成未完成的任务
- 实时显示任务进度

### 🎁 宝箱系统
- 自动开启每日宝箱
- 记录奖励详情
- 显示开启状态

### 👤 用户信息
- 显示用户名、积分、等级
- 实时更新账号状态

## 🔧 技术特性

### 网络处理
- **智能重试**: 失败请求自动重试最多3次
- **退避算法**: 重试间隔递增避免频繁请求
- **随机UA**: 随机轮换 User-Agent 避免检测
- **代理轮换**: 账号与代理按序分配

### 日志系统
- **分级日志**: INFO/WARN/ERROR/DEBUG 四个级别
- **彩色输出**: 不同级别使用不同颜色
- **时间戳**: 精确到秒的时间记录
- **上下文**: 账号编号和操作类型标识

### 界面美化
- **渐变标题**: 彩色渐变效果的标题
- **表格展示**: 任务和奖励以表格形式展示
- **进度条**: 操作进度实时显示
- **加载动画**: 优雅的等待动画

## 📊 运行流程

```
启动程序
    ↓
显示欢迎界面
    ↓
询问代理设置
    ↓
读取私钥和代理配置
    ↓
开始账号循环处理
    ↓
┌─────────────────────┐
│  单个账号处理流程     │
├─────────────────────┤
│ 1. 获取认证载荷      │
│ 2. 签名消息         │
│ 3. 创建会话         │
│ 4. 获取用户信息      │
│ 5. 获取任务列表      │
│ 6. 完成未完成任务    │
│ 7. 开启每日宝箱      │
│ 8. 显示结果统计      │
└─────────────────────┘
    ↓
所有账号处理完成
    ↓
等待24小时
    ↓
重新开始循环
```

## 📞 技术支持

- **Telegram频道**: [@OxJessdy](https://t.me/jessdy2)
- **作者**: 0xJessdy
- **版本**: v1.0.0

## 💝 捐赠支持

如果您觉得这个项目对您有帮助，可以通过以下地址进行捐赠支持项目开发：

- **EVM (以太坊/BSC/Polygon等)**: `0xD6611773079e022B4E403a5DF8152Cda9fA9B11f` 或 jessdy.eth
- **Solana**: `EEG8sYSWaU7S9c1NPKvkzWXZbfutvoRaR7sNtqrA22ru`
- **Bitcoin**: `bc1pv5xfcrvqadltd9vj83k7lshtz9vj4caj2uldj8d87e6f4c4p5unqh9um6q`

您的支持是我们持续改进和维护项目的动力！🙏

## 📄 许可证

本项目仅供学习和研究使用，请遵守相关平台的使用条款。

---

**免责声明**: 使用本工具的风险由用户自行承担，开发者不对任何损失负责。请确保遵守相关平台的服务条款。