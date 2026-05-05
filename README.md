# JSON → MessagePack 在线转换器

一个纯前端实现的 JSON 转 MessagePack 工具，无需任何外部库，部署于 GitHub Pages。

**在线使用：** https://graphif.github.io/json2msgpack/

---

## 功能

- 将任意 JSON 转换为标准 MessagePack 二进制格式
- 输出与 Python `msgpack.packb(data, use_bin_type=True)` **字节完全一致**
- 支持下载生成的 `.msgpack` 文件
- 显示 Hex 预览及格式化 Hex Grid（每行 16 字节，带 ASCII 侧栏）
- 显示 JSON / MessagePack 大小对比及压缩率
- `Ctrl+Enter` 快捷键快速转换

## 支持的类型

| JSON 类型 | MessagePack 格式 |
|-----------|-----------------|
| string    | fixstr / str8 / str16 / str32（UTF-8 编码，正确处理中文等多字节字符） |
| integer   | positive fixint / negative fixint / uint8~64 / int8~64 |
| float     | float64 |
| boolean   | true / false |
| null      | nil |
| array     | fixarray / array16 / array32 |
| object    | fixmap / map16 / map32 |

## 实现说明

完全手写 MessagePack 编码器，核心要点：

- 字符串长度取 **UTF-8 字节数**（通过 `TextEncoder` 编码），而非 JavaScript 的 `.length`（字符数）——这是中文等非 ASCII 字符能正确编码的关键
- 遵循 [MessagePack 官方规范](https://github.com/msgpack/msgpack/blob/master/spec.md)
- 零依赖，单个 HTML 文件，可直接离线使用

## 本地使用

直接用浏览器打开 `index.html` 即可，无需任何构建步骤或服务器。

```bash
# 克隆后直接打开
git clone https://github.com/graphif/json2msgpack.git
open json2msgpack/index.html
```

## License

MIT
