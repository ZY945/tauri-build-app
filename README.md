# 笔记路径
 https://www.yuque.com/zhangyang.com/tuiv0m/aev9n21009v4gqok#JnlPW
# 打包前端项目成为exe可执行文件
```text
rustc 1.78.0
cargo 1.78.0
node v16.17.0
```
# 启动过程
```bash
yarn tauri dev
```
# 构建
```bash
yarn tauri build
```
# 如何把已有的vue项目构建成应用程序
官方文档https://tauri.app/zh-cn/v1/guides/getting-started/setup/integrate
在package.json添加,然后把src-tauri文件夹拖入项目内
```json
"@tauri-apps/api": "^1"
```
![本地路径](/img/package-json.png)
# tauri打包后axios请求失败(有对应插件可以解决)
复现场景：开发环境直接启动没报错，构建成exe文件后启动报错
感谢提供的案例,个人首页地址为https://github.com/M-1202
![本地路径](/img/error.png)
解决办法：https://github.com/persiliao/axios-tauri-api-adapter

有个插件可以使用https://github.com/persiliao/axios-tauri-api-adapter
一、添加依赖
```bash
npm install axios-tauri-api-adapter
```
二、
在你使用axios创建实例的地方添加adapter: axiosTauriApiAdapter
```TypeScript
import axios from 'axios';
import axiosTauriApiAdapter from 'axios-tauri-api-adapter';
const client = axios.create({ adapter: axiosTauriApiAdapter });
```
三、在tauri.config.json根据你的后端网站进行添加
```json
{
  "tauri": {
    "allowlist": {
      "http": {
        "all": true, // Use this flag to enable all HTTP API features.
        "request": true, // Allows making HTTP requests.
        "scope": ["https://example.com/*"] // access scope for the HTTP APIs.
      }
    }
  }
}
```