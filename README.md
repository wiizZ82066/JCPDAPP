# JCP 链上经济仿真实验 DApp

基于以太坊 Sepolia 测试网的完整经济仿真系统，实现代币管理、去中心化交易所、流动性池、宏观税率调控、链上 DAO 治理及“技能提交获代币”功能。
[老师的项目仓库](https://github.com/moyang-creator/JCP-LAB)

## ✨ 功能特性

- 🔌 **钱包连接** – 支持 MetaMask，自动检测 Sepolia 网络
- 💼 **资产与授权** – 查看 JCP、JCPUSD、LP 代币余额，授权 DEX 合约
- 💧 **流动性池** – 添加/移除流动性，实时显示池中储备和价格
- 🔄 **去中心化兑换** – JCP ⇄ JCPUSD 无滑点兑换（恒定乘积 AMM）
- 📚 **技能市场** – 提交劳动成果获得 JCP 代币，支持分页查看与 CSV 导出
- 🏛️ **DAO 治理** – 创建提案（税率修改、国库转移、补贴发放、账户冻结/解冻），投票，执行提案
- ⏱️ **实时区块监控** – 显示当前区块，自动估算提案剩余时间（UTC+8）
- ⚙️ **合约地址配置** – 图形化界面修改所有合约地址，一键跳转 Etherscan
- 📟 **事件控制台** – 记录所有交易和错误信息，便于调试

## 🚀 快速开始

### 前置条件

- 安装 [MetaMask](https://metamask.io/) 浏览器扩展
- 网络切换至 **Sepolia 测试网**
- 准备 Sepolia ETH 作为 gas（可通过[水龙头](https://cloud.google.com/application/web3/faucet/ethereum/sepolia)获取）

#### 网页运行 （**推荐**）
- [网页版](https://wiizz82066.github.io/JCPDAPP/JCPDAPP)
#### 本地运行

1. 下载 `JCPDAPP.html` 文件到本地
2. 使用任意 Web 服务器[`测试环境为本地phpstudy的Apache服务`]
3. 打开浏览器访问
4. 点击「连接钱包」并授权，即可使用全部功能

## 📋 默认合约地址配置（Sepolia）

| 合约 | 地址 |
|------|------|
| JCP Token | `0xB7195a16DF4d49Ba337E9dbF0DC5617023587A6d` |
| JCPUSD Token | `0x843e84b5F223d1D7Dd89d0A06427C9A2E408D1B2` |
| DEX (JCPExchangeV3) | `0x44c57Df765b369c749A414E79AF06174E6D71fFd` |
| DAO (JCPGovernor) | `0x219Ea1eE622011Ff6CEC6DC563e17B8FeD209b62` |
| SkillMarket | `0x15EDad51E7316e161Dc24B80cC391Aa7144c63d5` |
| Treasury (JCPTreasury) | `0xf4a30daf8860FF135fC2D81F5cC54bac88f8BE3c` |

> 您可以在页面右上角「修改合约地址」中随时更改这些地址。

## 🖥️ 界面概览

- **顶部栏** – 显示网络状态、账户地址，提供钱包连接和刷新按钮
- **技能市场** – 提交技能描述，获得 JCP 奖励；技能列表支持分页和导出 CSV
- **资产与授权** – 展示各类代币余额，并可授权 DEX 使用 JCP
- **流动性池** – 添加/移除 JCP-JCPUSD 流动性，查看池内数量和实时价格
- **去中心化兑换** – 执行 JCP 与 JCPUSD 之间的互换
- **宏观经济调控** – 显示当前劳动税、资本税率和国库地址
- **DAO 治理** – 创建提案、投票、执行提案；提案列表完整显示参数（税率目标/地址/补贴数量等），并显示截止时间（UTC+8）
- **事件控制台** – 记录所有操作日志和错误信息

## 📦 项目结构

```
.
└── JCPDAPP.html   # 完整 DApp 单文件（包含样式、脚本、HTML）
```

> 采用了单文件设计，所有功能集中在一个文件中。

## 🔧 常见问题

### 1. 连接钱包后提示“非Sepolia”
- 请确保 MetaMask 当前网络选择为 **Sepolia**。点击页面「切换至Sepolia」按钮可快速切换。

### 2. 合约初始化失败（CALL_EXCEPTION）
- 检查您使用的合约地址是否与 Sepolia 上部署的一致（可通过 [Etherscan](https://sepolia.etherscan.io/) 验证）
- 确认当前钱包地址拥有 Sepolia ETH 用于 gas
- 如果自定义了合约地址，请确保 ABI 与前端提供的匹配

### 3. 提案列表不显示详细参数
- 本 DApp 直接从链上 `proposals` 映射读取原始数据，只要合约符合 `JCPGovernor` 接口即可正常显示
- 若遇到无法解析的情况，请尝试点击「手动刷新提案」按钮

### 4. 技能提交失败
- 技能市场合约需要具有 `MINTER_ROLE` 权限，请确保 `SkillMarket` 地址已被授予该角色

### 5.本地运行提示<u>请安装MetaMask</u>
- `Http/Https`协议才会正常连接钱包，本地文件协议`file`会忽略。请使用[网页版](https://wiizz82066.github.io/JCPDAPP/JCPDAPP)或参考[本地运行](#本地运行)
## 👨‍🏫 教学用途

本项目设计用于区块链课程实验教学，演示以下概念：
- ERC20 代币、流动性池、恒定乘积 AMM
- DAO 治理（链上提案、投票、执行）
- 宏观经济参数（税率）通过 DAO 调整
- 劳动价值代币化（技能市场）

学生可以通过实际操作理解 DeFi 与 DAO 的协同运作。

---
