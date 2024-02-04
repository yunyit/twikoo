# Serverless Cloud Function Deployment

| <div style="width: 6em">Ways of deployment</div> | Recommend  | Description  |
| ---- | ---- | ---- |
| [Vercel deployment](#vercel-deployment) | ★★★☆☆ | Suitable for users who want free deployment; binding your own domain name can improve access speed. |
| [Railway deployment](#railway-deployment) | ★★☆☆☆ | Free plans are available but not enough for one month of continuous operation; easy to deploy and suitable for global access. |
| [Zeabur deployment](#zeabur-deployment) | ★☆☆☆☆ | Easy to use and support pay-as-you-go. |
| [Netlify deployment](#netlify-deployment) | ★★★★☆ | Decent free plan. |
| [Hugging Face deployment](#hugging-face-部署) | ★★★★☆ | Free to use. |
| [私有部署](#私有部署) | ★★☆☆☆ | Suitable for users who have a server and need to apply for an HTTPS certificate by themselves. |
| [私有部署 (Docker)](#私有部署-docker) | ★★★☆☆ | Suitable for users who have a server and need to apply for an HTTPS certificate by themselves. |
## Vercel deployment

::: warning Note
Vercel should be deployed with twikoo.js version 1.4.0 or above.

The default domain name `*.vercel.app` is slow or impossible to access in mainland China, so bind your own domain name to improve access speed.
::.

[Video Tutorial](https://www.bilibili.com/video/BV1Fh411e7ZH)

1. Apply for a [MongoDB](https://www.mongodb.com/cloud/atlas/register) account.
2. Create a free MongoDB database, and choose `AWS / N. Virginia (us-east-1)` as the recommended region.
3. In the 'Database Access' page, click 'Add New Database User' to create a database user; select 'Password' for 'Authentication Method'; in 'Password Authentication', set the database username and password, and set the database user name and password in 'Password Authentication'; the user name and password can contain numbers and upper and lower case letters, please do not include special symbols. Click 'Add Built In Role' under 'Database User Privileges', select 'Atlas Admin' for 'Select Role', and click 'Add User'.

![](./static/mongodb-1.png)

4. On the 'Network Access' page, click 'Add IP Address', enter `0.0.0.0/0` for 'Access List Entry' (to allow connections from all IP addresses), and click 'Confirm'.

![](./static/mongodb-2.png)

5. On the `Database' page, click `Connect', select `Drivers' as the connection method, and record the database connection string; please change `<username>:<password>` in the connection string to `username:password` of the database you just created.

![](./static/mongodb-3.png)

6. 申请 [Vercel](https://vercel.com/signup) 账号
7. 点击以下按钮将 Twikoo 一键部署到 Vercel<br>

[![Deploy](https://vercel.com/button)](https://vercel.com/import/project?template=https://github.com/twikoojs/twikoo/tree/main/src/server/vercel-min)

8. 进入 Settings - Environment Variables，添加环境变量 `MONGODB_URI`，值为前面记录的数据库连接字符串
9. 进入 Settings - Deployment Protection，设置 Vercel Authentication 为 Disabled，并 Save

![](./static/vercel-1.png)

10. 进入 Deployments , 然后在任意一项后面点击更多（三个点） , 然后点击 Redeploy , 最后点击下面的 Redeploy
11. 进入 Overview，点击 Domains 下方的链接，如果环境配置正确，可以看到 “Twikoo 云函数运行正常” 的提示
12. Vercel Domains（包含 `https://` 前缀，例如 `https://xxx.vercel.app`）即为您的环境 id

## Railway deployment

::: warning 注意
Railway 部署的环境需配合 1.4.0 以上版本的 twikoo.js 使用

请一定要创建 MongoDB，不创建 MongoDB 也能正常使用，但重新部署后数据会丢失！
:::

1. 在 [Railway](https://railway.app/dashboard) 申请并登录账号，点击 New Project - Provision MongoDB，名称随意
2. 打开 [twikoojs/twikoo-zeabur](https://github.com/twikoojs/twikoo-zeabur) 点击 fork 将仓库 fork 到自己的账号下
3. 回到 Railway 点击 New - GitHub Repo - Configure GitHub App - 授权 GitHub - 选择刚才 fork 的仓库，等待部署完成
4. 点开环境卡片 - Variables - New Variable，左边输入 `PORT` 右边输入 `8080` 然后点 Add
5. 同样地，添加 MongoDB 相关环境变量 - New Variable - Add Reference - MONGO* - Add，重复步骤以添加 `MONGOHOST`、`MONGOPASSWORD`、`MONGOPORT`、`MONGOUSER` 和 `MONGO_URL` 环境变量。
6. 点开环境卡片 - Settings - Environment - Domains，绑定一个域名（例如 `mytwikoo.up.railway.app`）
7. 到博客配置文件中配置 envId 为 `https://` 加域名（例如 `https://mytwikoo.up.railway.app`）

## Zeabur deployment

::: warning 注意
Zeabur 部署的环境需配合 1.4.0 以上版本的 twikoo.js 使用

请一定要创建 MongoDB，不创建 MongoDB 也能正常使用，但重新部署后数据会丢失！
:::

1. 在 [Zeabur](https://dash.zeabur.com) 申请并登录账号，点击部署新服务 - 部署其他服务 - 部署 MongoDB，名称随意
2. 打开 [twikoojs/twikoo-zeabur](https://github.com/twikoojs/twikoo-zeabur) 点击 fork 将仓库 fork 到自己的账号下
3. 回到 Zeabur 点击部署新服务 - 部署你的源代码 - 授权 GitHub - 选择刚才 fork 的仓库，名称随意
  > _无需配置数据库连接字符串！ Zeabur 已自动配置_
4. 部署好后点开环境卡片 - 设置 - 域名，绑定一个域名（例如 `mytwikoo.zeabur.app`）
5. 到博客配置文件中配置 envId 为 `https://` 加域名（例如 `https://mytwikoo.zeabur.app`）

## Netlify deployment 

::: warning 注意
Netlify 部署的环境需配合 1.4.0 以上版本的 twikoo.js 使用

Netlify 免费等级（Functions Level 0）支持每月 125,000 请求次数和 100 小时函数计算时长
:::

1. 申请 [MongoDB](https://www.mongodb.com/cloud/atlas/register) 账号
2. 创建免费 MongoDB 数据库，区域推荐选择 `AWS / N. Virginia (us-east-1)`
3. 在 Database Access 页面点击 Add New Database User 创建数据库用户，Authentication Method 选 Password，在 Password Authentication 下设置数据库用户名和密码，用户名和密码可包含数字和大小写字母，请勿包含特殊符号。点击 Database User Privileges 下方的 Add Built In Role，Select Role 选择 Atlas Admin，最后点击 Add User

![](./static/mongodb-1.png)

4. 在 Network Access 页面点击 Add IP Address，Access List Entry 输入 `0.0.0.0/0`（允许所有 IP 地址的连接），点击 Confirm

![](./static/mongodb-2.png)

5. 在 Database 页面点击 Connect，连接方式选择 Drivers，并记录数据库连接字符串，请将连接字符串中的 `<username>:<password>` 修改为刚刚创建的数据库 `用户名:密码`

![](./static/mongodb-3.png)

6. 申请并登录 [Netlify](https://app.netlify.com) 账号，创建一个 Team
7. 打开 [twikoojs/twikoo-netlify](https://github.com/twikoojs/twikoo-netlify) 点击 fork 将仓库 fork 到自己的账号下
8. 回到 Netlify，点击 Add new site - Import an existing project

![](./static/netlify-1.png)

9. 点击 Deploy with GitHub，如果未授权 GitHub 账号，先授权，然后选择前面 fork 的 twikoo-netlify 项目

![](./static/netlify-2.png)

10. 点击 Add environment variables - New variable，Key 输入 `MONGODB_URI`，Value 输入前面记录的数据库连接字符串，点击 Deploy twikoo-netlify

![](./static/netlify-3.png)

11. 部署完成后，点击 Domain settings - 右侧 Options - Edit site name，可以设置属于自己的三级域名（`https://xxx.netlify.app`）

![](./static/netlify-4.png)

12. 进入 Site overview，点击上方的链接，如果环境配置正确，可以看到 “Twikoo 云函数运行正常” 的提示

![](./static/netlify-5.png)

13. 云函数地址（包含 `https://` 前缀和 `/.netlify/functions/twikoo` 后缀，例如 `https://xxx.netlify.app/.netlify/functions/twikoo`）即为您的环境 id

## Hugging Face 部署

1. 申请 [MongoDB](https://www.mongodb.com/cloud/atlas/register) 账号
2. 创建免费 MongoDB 数据库
3. 在 Database Access 页面点击 Add New Database User 创建数据库用户，Authentication Method 选 Password，在 Password Authentication 下设置数据库用户名和密码，用户名和密码可包含数字和大小写字母，请勿包含特殊符号。点击 Database User Privileges 下方的 Add Built In Role，Select Role 选择 Atlas Admin，最后点击 Add User

![](./static/mongodb-1.png)

4. 在 Network Access 页面点击 Add IP Address，Access List Entry 输入 `0.0.0.0/0`（允许所有 IP 地址的连接），点击 Confirm

![](./static/mongodb-2.png)

5. 在 Database 页面点击 Connect，连接方式选择 Drivers，并记录数据库连接字符串，请将连接字符串中的 `<username>:<password>` 修改为刚刚创建的数据库 `用户名:密码`

![](./static/mongodb-3.png)

6. 申请 [Hugging Face](https://huggingface.co/join) 账号
7. 登录，点击 Spaces - Create new Space

![](./static/hugging-1.png)

8. 输入 Space name，Select the Space SDK 选择 Docker，Choose a Docker template 选择 Blank，Space hardware 选择 FREE，选择 Public，点击 Create Space

![](./static/hugging-2.png)

9. 进入刚刚创建的 Space，点击页面上方的 Settings，滚动到 Variables and secrets 部分，点击 New secret，Name 输入 `MONGODB_URI`，Value 输入前面记录的数据库连接字符串，点击 Save

![](./static/hugging-3.png)

10. 点击页面上方的 Files - Add file - Create a new file

![](./static/hugging-4.png)

11. 在 Name your file 中输入 `Dockerfile`，在 Edit 区域输入以下内容

```Dockerfile
FROM imaegoo/twikoo
ENV TWIKOO_PORT 7860
EXPOSE 7860
```

![](./static/hugging-5.png)

12. 点击 Commit new file to main
13. 点击右上角 Settings 右方的菜单（三个点）图标 - Embed this Space，Direct URL 下的内容（例如 `https://xxx-xxx.hf.space`）即为您的环境 id

![](./static/hugging-6.png)

## 私有部署

::: warning 注意
私有部署的环境需配合 1.6.0 或以上版本的 twikoo.js 使用

私有部署对服务器系统没有要求，Windows、Ubuntu、CentOS、macOS 等常用系统均支持。

私有部署涉及终端操作、申请证书、配置反向代理或负载均衡等高级操作，如果对这些不太了解，建议优先选择其他方式部署。
:::

1. 服务端下载安装 [Node.js](https://nodejs.org/zh-cn/)
2. 安装 Twikoo server: `npm i -g tkserver`
3. 根据需要配置环境变量，所有的环境变量都是可选的

| 名称 | 描述 | 默认值 |
| ---- | ---- | ---- |
| `MONGODB_URI` | MongoDB 数据库连接字符串，不传则使用 lokijs | `null` |
| `MONGO_URL` | MongoDB 数据库连接字符串，不传则使用 lokijs | `null` |
| `TWIKOO_DATA` | lokijs 数据库存储路径 | `./data` |
| `TWIKOO_PORT` | 端口号 | `8080` |
| `TWIKOO_THROTTLE` | IP 请求限流，当同一 IP 短时间内请求次数超过阈值将对该 IP 返回错误 | `250` |
| `TWIKOO_LOCALHOST_ONLY` | 为`true`时只监听本地请求，使得 nginx 等服务器反代之后不暴露原始端口 | `null` |
| `TWIKOO_LOG_LEVEL` | 日志级别，支持 `verbose` / `info` / `warn` / `error` | `info` |
| `TWIKOO_IP_HEADERS` | 在一些特殊情况下使用，如使用了`CloudFlare CDN` 它会将请求 IP 写到请求头的 `cf-connecting-ip` 字段上，为了能够正确的获取请求 IP 你可以写成 `['headers.cf-connecting-ip']` | `[]` |

4. 启动 Twikoo server: `tkserver`
5. 访问 `http://服务端IP:8080` 测试服务是否启动成功
6. 配置前置代理实现 HTTPS 访问（可以用 Nginx、负载均衡或 Cloudflare 等）
7. 到博客配置文件中配置 envId 为 `https://` 加域名（例如 `https://twikoo.yourdomain.com`）

::: tip 提示
1. Linux 服务器可以用 `nohup tkserver >> tkserver.log 2>&1 &` 命令后台启动
2. 数据默认在 data 目录，请注意定期备份数据
:::

## 私有部署 (Docker)

::: warning 注意
私有部署的环境需配合 1.6.0 或以上版本的 twikoo.js 使用

私有部署涉及终端操作、申请证书、配置反向代理或负载均衡等高级操作，如果对这些不太了解，建议优先选择其他方式部署。
:::

### Docker

```sh
docker run --name twikoo -e TWIKOO_THROTTLE=1000 -p 8080:8080 -v ${PWD}/data:/app/data -d imaegoo/twikoo
```

### Docker Compose

```yml
version: '3'
services:
  twikoo:
    image: imaegoo/twikoo
    container_name: twikoo
    restart: unless-stopped
    ports:
      - 8080:8080
    environment:
      TWIKOO_THROTTLE: 1000
    volumes:
      - ./data:/app/data
```
