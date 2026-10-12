# OIE 源码搜索

[![build](https://github.com/diridium-com/oie-source-code-search/actions/workflows/build.yml/badge.svg)](https://github.com/diridium-com/oie-source-code-search/actions/workflows/build.yml) [![release](https://img.shields.io/github/v/release/diridium-com/oie-source-code-search?label=release&color=blue)](https://github.com/diridium-com/oie-source-code-search/releases/latest) [![License: MPL 2.0](https://img.shields.io/badge/License-MPL%202.0-green.svg)](LICENSE) ![Java](https://img.shields.io/badge/Java-17%2B-blue.svg) [![OIE](https://img.shields.io/badge/OIE-4.6.0-blue.svg)](https://www.openintegrationengine.org/)

一个 [Open Integration Engine](https://www.openintegrationengine.org/)（OIE）插件，提供类似 grep 的搜索功能，可搜索所有通道脚本、代码模板、全局脚本和消息模板 — 直接在管理界面中使用。

![Source Code Search in action](https://raw.githubusercontent.com/wiki/diridium-com/oie-source-code-search/images/4.png)

## 功能特性

- **全文搜索** — 在单个查询中搜索所有产品类型
- **文本和正则** 搜索模式，区分或不区分大小写
- **范围控制** — — 可独立搜索通道、代码模板、全局脚本和消息模板
- **包含名称和描述** — 通道、代码模板和全局脚本的名称和描述会与代码一起被搜索，因此按名称查找产品即可生效
- **通道范围** — — 搜索所有通道、所选通道或编辑器中的当前通道
- **层级结果** — 带位置导航和匹配高亮
- **导出** — 将结果导出为 JSON（含元数据）或 CSV
- **非模态对话框** — — 边工作边搜索
- **权限感知** — — 发布“搜索源码”权限，并遵守每个角色的通道限制

## 权限

此插件注册了一个权限 **搜索源码**，涵盖其两个 REST 操作和两个菜单入口。

在默认安装的 OIE 中，这不会造成任何变化：默认授权控制器允许每个已认证用户执行所有操作，与通道编辑器一样。

在运行基于角色的授权控制器的安装中，必须将权限授予角色后其用户才能搜索，结果仅限于该角色可访问的通道。
不在角色范围内的通道会被跳过，代码模板仅限于至少一个可访问通道范围内的库，全局脚本被排除，因为它们是服务器级别的而非通道级别的。 名称和描述也遵循同样的规则：角色无法访问的通道不会被访问，因此其名称也不会通过名称搜索出现。 当有内容被过滤时，对话框会显示相应提示，此提示也会出现在 JSON 和 CSV 导出中，以免将部分结果集误认为完整结果。

> **Upgrading from 1.2.0 or earlier on a role-based server:** search was previously ungated, so
> every role could use it. After upgrading, an administrator must grant the new permission to
> each role that should keep it. See [issue #5](https://github.com/diridium-com/oie-source-code-search/issues/5).

## 文档

完整文档请参见 [Wiki](https://github.com/diridium-com/oie-source-code-search/wiki)，包括：

- [Why You Need This](https://github.com/diridium-com/oie-source-code-search/wiki/Why-You-Need-This) — real-world use cases
- [Getting Started](https://github.com/diridium-com/oie-source-code-search/wiki/Getting-Started) — how to launch and use the search
- [Search Options](https://github.com/diridium-com/oie-source-code-search/wiki/Search-Options) — what each scope searches
- [Regex Tips](https://github.com/diridium-com/oie-source-code-search/wiki/Regex-Tips) — common patterns and performance advice
- [FAQ](https://github.com/diridium-com/oie-source-code-search/wiki/FAQ)

## 设计说明

[docs/design-notes.md](docs/design-notes.md) 解释了插件各部分的设计原因，特别是其授权行为和搜索范围模型，以及测试套件保证和不保证的内容。在修改授权路径之前值得阅读。

## 系统要求

|属性|值|
|-----------|-------|
| OIE 版本 | 4.6.0+ |
| Java | 17+ |

## 安装

从 OIE 社区商店安装，或从 [Releases](https://github.com/diridium-com/oie-source-code-search/releases) 页面下载最新发布的 ZIP 包，通过 OIE 管理界面的插件管理器安装。

## 从源码构建

```
./scripts/install-engine-jars.sh
mvn verify
```

The script installs `mirth-server`, `donkey-server`, `mirth-client-core`, and `mirth-client` into your local Maven repository, taken from the published OIE release matching the POM's `mc.version` and checked against that release's `sha256sums`. Run it once per engine version.

## 许可证

[MPL-2.0](LICENSE) — Copyright (c) 2025-2026 Diridium Technologies Inc.

在 Finnegan 狗的精神支持下开发。
