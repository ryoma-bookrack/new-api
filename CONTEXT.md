# CONTEXT.md — 领域术语表

> 本文件是术语 glossary，**不**放实现细节、规格、草稿。新条目由
> agent-step 的 align-grill 在对齐过程中**当场**写入。

## 约定

- 术语首字母大写，不变复数（`Project` 而非 `Projects`）。
- 每条术语一段定义；冲突 / 歧义当场指出并解决。
- 当用户口语与本表冲突时，**本表优先**，直到用户显式改本表。

## 术语

### Stem

本仓库。
本地 AI 网关，含义是脑干。
它接在 Brain 下面，把 Client 的请求转到上游模型，再把结果送回来。

### Brain

另一个项目，含义是大脑。
它用模型完成各种能力，并通过 Stem 调用模型。
本仓库不包含 Brain 的实现。

### Client

调用 Stem 的一方。
Brain 是 Client。
持有 API Key 的其他程序也是 Client。

### Upstream Project

本仓库所基于的上游项目 new-api，作者组织是 QuantumNous。
Git 远程 `upstream` 和分支 `upstream-main` 用来同步这份上游代码。
上游项目的名字和作者署名保留在仓库里。
易混词：Provider。
Provider 是模型供应商，不是这份源码。

### Provider

供应商。
它标明模型属于哪一家，供模型目录展示。
易混词：Channel。
Channel 是一条可以真正发起调用的连接。
Provider 本身不保存调用密钥，也不接收请求。

### Channel

渠道。
Stem 通往某一家模型服务的一条配置，包括供应商类型、上游密钥、地址、对外提供的模型、所属分组，以及优先级和权重。
同一个 Model 名可以在这条 Channel 上映射成供应商侧的另一个名字。
易混词：Channel 上的上游密钥不是 API Key。

### Model

模型。
Client 在请求里点名的那个名字。
它是 Stem 对外的模型名，不必等于供应商侧的原始名字。

### Group

分组。
User、API Key 和 Channel 共用的访问范围。
一次请求只会落到该 API Key 允许的分组里、并且启用了所点 Model 的 Channel。

### API Key

控制台中的 API 密钥。
Client 调用 Stem 时出示的凭证。
代码里的类型名是 Token。
易混词：Channel 的上游密钥、一次回复消耗的 token 数量、浏览器登录会话。

### User

用户。
控制台账号，带有角色、分组和额度。

### Quota

额度。
Stem 按使用扣减的余额。
User 和 API Key 都可以带有额度。

### Ability

分组、模型、渠道三者之间的一条启用关系。
它决定某个分组里的某个模型可以由哪条 Channel 来接。
易混词：它不是用户角色，也不是模型的功能清单。

### Relay

一次请求从 Client 进入 Stem、选中 Channel、转成上游协议、再把结果送回的全过程。

### RelayKit

独立模块，只负责文本协议之间的请求、响应和流式转换。
易混词：Relay。
RelayKit 不选择 Channel，也不做鉴权和计费。

### Task

异步任务。
图片、视频这类不能在一次请求里结束的工作，由插件发起，之后再查询结果。
易混词：普通对话请求是 Relay，不是 Task。

### Project

一个 git 仓库根目录所代表的工作单元。所有 agent-step skill 都假设"当前工作目录落在某个 Project 内"。

### Skill

一项可触发的 Agent 能力（`SKILL.md`）。Agent 在满足触发条件时**自动**或**应用户指令**调用之；不强制按顺序串联。

### Problem

`.scratch/<problem-group>/NNN-<slug>.md` 这一份 markdown 文件。本仓开发流程中使用的工单。状态由文件首部的 `Status:` 行表达。

### Problem Group

`.scratch/<problem-group>/` 这一层目录所代表的功能 / 主题分组。一个 Problem Group 可以包含若干 Problem。
