# TrendRadar 启动手册

## 项目概述

TrendRadar 是一个热点新闻分析工具，能够：
- 自动抓取多个平台的热点新闻数据
- 生成结构化的 HTML 报告
- 提供数据可视化和分析功能
- 支持 HTTP 服务器远程访问

## 环境搭建

### 首次部署步骤

1. **下载项目**
   - 确保项目已下载到本地目录：`e:\skillstest\trendRadar`

2. **运行部署脚本**
   - 双击运行 `setup-windows.bat`（中文版本）或 `setup-windows-en.bat`（英文版本）
   - 等待脚本自动安装所有依赖项
   - 完成后会创建虚拟环境 `.venv`

3. **验证部署成功**
   - 检查 `.venv` 目录是否存在
   - 检查 `output` 目录是否已创建

## 一键启动程序

项目根目录提供了简化版的一键启动程序：`start_trendradar_simple.bat`

### 运行方法

1. **双击启动**
   - 直接双击 `start_trendradar_simple.bat` 文件
   - 或在命令行中运行：`.tart_trendradar_simple.bat`

2. **主菜单操作**
   - 启动后会显示主菜单，提供以下选项：

   ```
   ===========================================================
   Main Menu
   ===========================================================
   1. Run data crawl and generate report
   2. Generate HTML report only
   3. Start HTTP server
   4. View latest news data
   5. Exit
   ===========================================================
   Select operation (1-5): 
   ```

   - 输入对应数字并按 Enter 键执行操作

### 功能说明

#### 1. Run data crawl and generate report
- **功能**：运行完整流程，包括数据抓取和报告生成
- **执行步骤**：
  1. 运行 `python -m trendradar` 抓取数据
  2. 抓取完成后自动运行 `python generate_html_from_db.py` 生成报告
- **输出**：
  - 数据文件：`output/news/[日期].db`
  - HTML 报告：`output/html/[日期]/[时间].html`

#### 2. Generate HTML report only
- **功能**：仅使用现有数据生成 HTML 报告
- **执行**：运行 `python generate_html_from_db.py`
- **输出**：`output/html/[日期]/[时间].html`

#### 3. Start HTTP server
- **功能**：启动 HTTP 服务器，支持远程访问
- **执行**：运行 `uv run python -m mcp_server.server --transport http --host 0.0.0.0 --port 3333`
- **访问地址**：`http://localhost:3333/mcp`
- **停止方法**：按 `Ctrl+C` 停止服务并返回主菜单

#### 4. View latest news data
- **功能**：查看最新抓取的新闻数据
- **执行**：运行 `python view_news_data.py`
- **输出**：在命令行中显示最新新闻列表

#### 5. Exit
- **功能**：退出一键启动程序

## 数据文件结构

```
trendRadar/
├── output/
│   ├── html/          # HTML 报告文件
│   │   ├── [日期]/     # 按日期分类
│   │   │   └── [时间].html  # 按时间命名的报告
│   ├── news/          # 新闻数据库文件
│   │   └── [日期].db   # 按日期命名的 SQLite 数据库
│   ├── reports/       # PDF 报告文件
│   └── rss/           # RSS 数据文件
├── trendradar/        # 核心代码
├── start_trendradar_simple.bat  # 一键启动程序
└── STARTUP_GUIDE.md   # 本启动手册
```

## 常见问题与解决方案

### 1. 虚拟环境未找到

**错误信息**：`ERROR: Virtual environment not found`

**解决方案**：
- 运行 `setup-windows.bat` 重新部署环境
- 检查 `.venv` 目录是否存在

### 2. 数据抓取失败

**错误信息**：`ERROR: Crawl failed, error code: XXX`

**解决方案**：
- 检查网络连接是否正常
- 等待一段时间后重试
- 检查 `config/config.yaml` 配置文件是否正确

### 3. 报告生成失败

**错误信息**：`ERROR: Report generation failed, error code: XXX`

**解决方案**：
- 确保 `output/news/` 目录下有数据库文件
- 检查 `generate_html_from_db.py` 脚本是否正确

### 4. HTTP 服务器启动失败

**错误信息**：端口被占用或启动失败

**解决方案**：
- 检查端口 3333 是否被其他程序占用
- 尝试使用其他端口（修改启动脚本中的 `--port` 参数）

## 最佳实践

1. **定期运行**：建议每天运行一次数据抓取，保持数据最新
2. **备份数据**：定期备份 `output/news/` 目录下的数据库文件
3. **查看报告**：使用浏览器打开生成的 HTML 报告，查看热点新闻分析
4. **远程访问**：在需要远程访问时启动 HTTP 服务器

## 技术支持

- **项目文档**：查看 `README.md` 和 `DOCUMENTATION.md`
- **日志文件**：检查 `output` 目录下的日志文件
- **联系支持**：如有问题，请参考项目文档中的支持信息

## 版本信息

- 最后更新时间：2026-01-22
- 适用版本：TrendRadar 最新版
- 操作系统：Windows

---

**注意**：本手册仅适用于 Windows 操作系统。如需在其他操作系统上运行，请参考相应的部署文档。