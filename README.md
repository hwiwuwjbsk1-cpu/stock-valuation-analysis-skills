# 股票估值分析 Skills

让 AI 大模型直接调用专业金融数据的 Agent Skill，对 A 股个股进行多维度估值分析。基于**相对估值、历史估值分位、成长性匹配度验证、估值合理性综合判断**四层维度输出结构化估值分析报告。

数据由 [今日投资数据市场](https://data-api.investoday.net) 提供，20 年金融数据积累，腾讯投资、毕马威 KPMG 金融科技 50 强认证。

---

## 快速开始

### 1. 获取 API Key

**InvestToday API Key**：
前往 [今日投资数据平台](https://data-api.investoday.net/login) 注册并创建 API Key。

### 2. 安装依赖

```bash
pip install -r requirements.txt
```

### 3. 配置 API Key

```bash
cp .env.example .env
# 编辑 .env，填入：INVESTODAY_API_KEY=your_key_here
```

### 4. 安装 Skill

将 `skills/` 目录复制到对应平台的 Skills 目录：

```bash
# Cursor — 个人级（适用所有项目）
cp -r skills/ ~/.cursor/skills/stock-valuation-analysis/

# Cursor — 项目级
cp -r skills/ .cursor/skills/stock-valuation-analysis/

# Claude Code
cp -r skills/ ~/.claude/skills/stock-valuation-analysis/

# OpenClaw
cp -r skills/ ~/.openclaw/workspace/skills/stock-valuation-analysis/
```

重启客户端后，AI 自动加载该 Skill。

---

## 功能特性

### 核心功能

- **四层估值分析**：相对估值、历史估值分位、成长性匹配度验证、估值合理性综合判断
- **结构化报告输出**：一句话结论、估值画像总览、亮点与风险、详细分析、观察点
- **自动意图识别**：自动识别股票代码/名称，标准化为 6 位 A 股代码
- **合规风控**：不输出买卖建议、目标价、交易指令，仅做估值状态描述

### 分析维度

| 维度 | 核心指标 | 参考标准 |
|------|----------|----------|
| 相对估值 | PE(TTM)、扣非 PE、PB、PS | PE 越低通常估值越便宜 |
| 历史估值分位 | PE、PB、PS 历史分位 | 分位越低，历史安全边际越高 |
| 成长性匹配度验证 | PEG、乔尔收益率、自由现金流估值 | PEG<1 匹配度较好 |
| 估值合理性综合判断 | 综合评分、估值状态 | 综合判断贵不贵 |

---

## 使用示例

### 输入示例

```
分析 000977 估值
浪潮信息现在贵吗
帮我看看 600519 的估值高低
分析 sz000001 的安全边际
```

### 输出示例

```markdown
# 浪潮信息（000977）估值分析报告

## 🧭 一句话结论
**公司当前整体估值状态为估值相对合理偏低，核心特征是 PE 处于历史低位，PEG 显示成长性匹配度较好。**

## 🪪 估值画像总览

| 维度 | 关键指标 | 当前数据（截至 2026-03-16） |
|------|----------|------------------------|
| 相对估值 | PE(TTM)、扣非 PE、PB、PS | PE(TTM) 18.5x，PB 2.8x |
| 历史估值分位 | PE、PB、PS 历史分位 | PE 分位 25%，PB 分位 30% |
| 成长性匹配度验证 | PEG、乔尔收益率 | PEG 0.8，乔尔收益率 12% |
| 估值合理性综合判断 | 综合评分、估值状态 | 综合评分 7.5/10，估值合理 |

...
```

---

## MCP 工具调用

本 Skill 调用以下 InvestToday MCP 工具：

| 工具名 | 用途 | 调用次数 |
|--------|------|----------|
| `get_stock_finance_valuation` | 股票估值指标 | 1 |
| `get_stock_finance_valuation_hist` | 股票估值历史指标 | 1 |

---

## 输出模板

报告严格遵循以下结构（7 个二级标题）：

1. **🧭 一句话结论** - 整体估值状态与核心特征
2. **🪪 估值画像总览** - 四层表格对比
3. **✅ 当前亮点** - 1-3 条积极信号
4. **⚠️ 当前风险** - 1-3 条风险因素
5. **🔍 详细估值分析** - 四层深度解析
   - 相对估值
   - 历史估值分位
   - 成长性匹配度验证
   - 估值合理性综合判断
6. **👀 下一期重点观察** - 1-3 个观察点
7. **🛡️ 风险提示** - 合规声明

---

## 合规说明

- ✅ 仅描述估值状态、历史位置、支撑情况
- ✅ 输出风险来源和后续跟踪点
- ❌ 不输出目标价、买卖建议、止盈止损
- ❌ 不输出仓位配置、短线操作建议
- ❌ 不展示内部评分、计算过程

> 本 Skill 提供的金融数据仅供参考，不构成投资建议。请遵守相关法律法规和交易所规定，合法合规使用数据。

---

## 相关链接

- [今日投资数据市场](https://data-api.investoday.net/hub?url=%2Fapidocs%2Fai-native-financial-data)
- [常见问题](https://data-api.investoday.net/hub?url=%2Fapidocs%2Ffaq)

---

## License

MIT
