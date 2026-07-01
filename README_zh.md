# 孙荣个人学术网站

本仓库是爱知县癌症中心肿瘤抑制领域 Research Resident 孙荣的个人学术主页项目。

网站基于 Hugo 构建，并采用与相关学术网站一致的三语言数据驱动结构。论文、项目、研究指导经历、动态和个人简介均通过 `data/` 文件夹中的 YAML 文件维护。

## 主要功能

- 支持英文、日文、中文三语言页面。
- 主页包含个人简介、履历、研究领域、寄语和外部链接。
- Publications、Projects、Supervision、News、Access、Links 均采用数据文件管理。
- 论文信息在 `data/publications/` 中按年份管理。
- 研究方向在 `data/research/` 中按文件夹管理。
- 通过 `scripts/update_citations.py` 从 Google Scholar 更新引用数据。
- 通过 GitHub Actions 自动部署到 GitHub Pages。

## 本地预览

```powershell
hugo server -D
```

生成正式网站：

```powershell
hugo --minify
```

## 数据管理

- `data/home/`：个人资料和主页内容。
- `data/access/`：联系方式与访问相关信息。
- `data/links/`：外部个人主页链接；暂未提供的链接可以留空，后续再补充。
- `data/research/`：研究方向与代表论文。
- `data/publications/`：按年份划分的论文列表。
- `data/projects/items.yaml`：研究项目。
- `data/supervision/items.yaml`：研究指导经历。
- `data/news/<year>/`：按年份划分的动态和履历信息。
- `data/citations/meta.yaml`：引用统计与最新更新时间。

三语言数据中，`en.yaml` 尽量保存共通信息，`ja.yaml` 和 `zh.yaml` 只保存同一 ID 下需要翻译或覆盖的内容。

## 引用数据更新

手动更新命令：

```powershell
python scripts/update_citations.py
```

该脚本会读取 Google Scholar 个人主页，更新所有论文 YAML 文件中的引用数，写入 `data/citations/meta.yaml`，并在发现新论文时尝试自动添加到对应年份文件中。

`.github/workflows/update-citations.yml` 会每天自动运行两次，时间约为日本时间夜间 12 点和中国时间中午 12 点。

Google Scholar 有时会限制自动访问。如果更新失败，可以稍后重新运行 workflow 或在本地再次执行脚本。

## 部署

`.github/workflows/hugo.yml` 负责 GitHub Pages 自动部署。将修改 push 到 GitHub 后，网站会自动构建并发布。
