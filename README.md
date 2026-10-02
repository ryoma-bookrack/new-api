# Stem

脑干。

Stem 是本地 AI 网关，接在 Brain 下面。
Brain 是大脑，用模型完成各种能力。
Stem 把这些请求转到上游模型，再把结果送回来。

```text
Brain（大脑）
    |
    v
Stem（脑干）
    |
    v
上游模型
```

## 本机做什么

在本机提供一个统一入口。
渠道、访问密钥和用量都在这里管理。
Brain 和其他客户端只对接 Stem。

## 上游项目

这个仓库基于 [new-api](https://github.com/QuantumNous/new-api)（QuantumNous）。
原来的英文说明在 [README.upstream.md](./README.upstream.md)。
简体中文说明在 [README.zh_CN.md](./README.zh_CN.md)。
部署、接口和开发细节以这两份说明为准。
上游项目的名字和作者署名保留在这些文件和代码里。
