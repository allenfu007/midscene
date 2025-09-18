# Midscene YAML 测试最小可用环境（MVP）

使用 Midscene.js 直接以 YAML 编写并执行端到端测试，无需 JS 代码。

## 环境要求
- Node.js ≥ 18（建议 LTS）
- Windows 10/11

## 安装依赖
```bash
npm install
```

## 配置环境变量（.env）
项目已将 `.env` 写入 `.gitignore`，请在根目录创建/编辑 `.env`：
```env
# 如使用系统 Chrome，请设置为实际路径
PUPPETEER_EXECUTABLE_PATH=C:\\Program Files\\Google\\Chrome\\Application\\chrome.exe

# 若需下载指定 Chrome 版本，推荐使用国内镜像（可选）
PUPPETEER_DOWNLOAD_BASE_URL=https://registry.npmmirror.com/-/binary/chrome-for-testing
```

如果运行提示缺少 Chrome 133，可执行：
```bash
npx puppeteer browsers install chrome@133.0.6943.53 --base-url https://registry.npmmirror.com/-/binary/chrome-for-testing
```

## 运行用例
- 运行 Bing 示例：
```bash
npx midscene ./bing-search.yaml
```
- 运行人群圈选业务用例：
```bash
npx midscene ./customer-segment.yaml
```

## 目录说明
```
midscene/
  ├─ .env                 # 私密变量（已被 .gitignore 忽略）
  ├─ .gitignore
  ├─ package-lock.json
  ├─ node_modules/
  ├─ bing-search.yaml     # 示例用例
  ├─ customer-segment.yaml# 业务用例：登录、新建人群、删除
  └─ midscene_run/        # 运行缓存与输出（执行后生成）
```

## 常见问题
- 提示 “Could not find Chrome (ver. 133.0.6943.53)”
  - 方案一：执行上面的 `npx puppeteer browsers install chrome@133.0.6943.53 ...`
  - 方案二：在 `.env` 设置 `PUPPETEER_EXECUTABLE_PATH` 指向本机 Chrome
- 下载失败/ECONNRESET：设置 `PUPPETEER_DOWNLOAD_BASE_URL` 为国内镜像后重试
- 若之前设置过 `PUPPETEER_SKIP_DOWNLOAD=true`：请移除后再安装或使用系统 Chrome 路径

## YAML 动作速览
- `ai`：自然语言执行复杂交互
- `aiTap`：点击
- `aiWaitFor`：等待页面出现文本/状态
- `sleep`：固定时长等待（毫秒）
- `aiAssert`：断言

如需扩展步骤，按现有风格在 `tasks/flow` 中继续追加即可。
