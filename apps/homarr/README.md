## 环境变量

- SECRET_ENCRYPTION_KEY 加密密钥,必须是长度 64 位的字符串

在终端通过 shell 命令生成:

```shell
openssl rand -hex 32
```

在浏览器通过控制台生成:

```js
Array.from(crypto.getRandomValues(new Uint8Array(32)))
  .map((b) => b.toString(16).padStart(2, "0"))
  .join("");
```
