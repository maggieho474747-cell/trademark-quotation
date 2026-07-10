# 涉外商标报价系统

一个无需数据库、可部署在 GitHub Pages 上的涉外商标报价工具。支持多国家/地区和多个尼斯类别，自动拆分官费、服务费、检索费，并可打印或导出 PDF 报价单。

## 功能

- **多国家报价**：同时选择多个目的国，实时对比费用
- **尼斯分类 1–45 类**：可多选，费用按类别数自动计算
- **费率可配置**：官费、服务费、检索费、汇率均可自定义
- **汇率自动更新**：通过 GitHub Actions 每日自动获取最新汇率
- **打印/导出 PDF**：通过浏览器打印功能导出报价单
- **本地存储**：数据使用 `localStorage` 保存在当前浏览器中
- **报价历史**：保存并管理历史报价记录

## 部署到 GitHub Pages

### 1. 创建 GitHub 仓库

```bash
# 克隆或初始化
git init trademark-quotation
cd trademark-quotation

# 复制项目文件后
git add .
git commit -m "init: 涉外商标报价系统"

# 关联远程仓库
git remote add origin https://github.com/<你的用户名>/trademark-quotation.git
git push -u origin main
```

### 2. 启用 GitHub Pages

1. 进入仓库 → **Settings** → **Pages**
2. Source 选择 **Deploy from a branch**
3. Branch 选择 `main`，目录选 `/ (root)`
4. 保存后等待部署完成

### 3. 启用每日汇率更新

1. 进入仓库 → **Settings** → **Actions** → **General**
2. 确认 Workflow permissions 选择 **Read and write permissions**
3. GitHub Actions 会自动在每天 UTC 0:00（北京时间 8:00）更新汇率
4. 也可在 **Actions** 页面手动触发 `每日更新汇率` workflow

## 首次使用

1. 打开部署后的页面 `https://<用户名>.github.io/trademark-quotation/`
2. 进入「费率设置」，将演示官费、服务费和汇率替换为实际数据
3. 回到「新建报价」，填写客户、选择国家和尼斯类别
4. 核对右侧费用明细，可调整折扣/加急/税费
5. 点击「打印/导出 PDF」，在浏览器打印窗口中选择"另存为 PDF"

## 计价公式

```
单个国家的本币费用：

首类官费 + (类别数 - 1) × 附加类官费
+ 首类服务费 + (类别数 - 1) × 附加类服务费
+ 检索费/类 × 类别数（如启用）
```

汇率换算后汇总为 CNY 总计。

## 技术栈

- 纯 HTML/CSS/JavaScript，无需构建工具
- 数据存储：浏览器 `localStorage`
- 汇率数据：`data/exchange-rates.json`（GitHub Actions 自动更新）
- 部署：GitHub Pages（纯静态）

## 注意事项

- 清理浏览器数据会同时清除历史报价和自定义费率，建议定期备份
- 官费、税费、商品项限制及汇率会变化，建议定期核实
- 本工具仅供参考，正式报价请以各国知识产权局公示为准
