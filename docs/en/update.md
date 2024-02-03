# Update

Update methods diver among deployment methods, please be aware. After the update is successfully deployed, please also update the `x.x.x` version number in the Twikoo CDN address of the front end so that it is the same as the Serverless Cloud Function version number, and then deploy the website.

## 针对 Vercel 部署的更新方式

1. 进入 [Vercel 仪表板](https://vercel.com/dashboard) - twikoo - Settings - Git
2. 点击 Connected Git Repository 下方的仓库地址
3. 打开 package.json，点击编辑
4. 将 `"twikoo-vercel": "latest"` 其中的 `latest` 修改为最新版本号。点击 Commit changes
5. 部署会自动触发，可以回到 [Vercel 仪表板](https://vercel.com/dashboard)，查看部署状态

## 针对 Railway 和 Zeabur 部署的更新方式

1. 登录 Github，找到部署时 fork 到自己账号下的名为 twikoo-zeabur 的仓库
2. 打开 package.json，点击编辑
3. 将 `"tkserver": "latest"` 其中的 `latest` 修改为最新版本号。点击 Commit changes
4. 部署会自动触发

## 针对 Netlify 部署的更新方式

1. 登录 Github，找到部署时 fork 到自己账号下的名为 twikoo-netlify 的仓库
2. 打开 package.json，点击编辑
3. 将 `"twikoo-vercel": "latest"` 其中的 `latest` 修改为最新版本号。点击 Commit changes
4. 部署会自动触发

## 针对 Hugging Face 部署的更新方式

1. 登录 Hugging Face，找到部署的 Space，点击上方 Settings，往下滚动找到并点击 Factory rebuild

## 针对私有部署的更新方式

1. 停止旧版本 `kill $(ps -ef | grep tkserver | grep -v 'grep' | awk '{print $2}')`
2. 拉取新版本 `npm i -g tkserver@latest`
3. 启动新版本 `nohup tkserver >> tkserver.log 2>&1 &`

## 针对私有部署 (Docker) 的更新方式

1. 拉取新版本 `docker pull imaegoo/twikoo`
2. 停止旧版本容器 `docker stop twikoo`
3. 删除旧版本容器 `docker rm twikoo`
4. [启动新版本容器](#私有部署-docker)

## 自动更新

考虑到可用性和安全性问题，Twikoo 没有实现自动更新，也没有计划实现自动更新。如果您希望实现自动更新，可以参考 MHuiG 基于 Github 工作流的 [twikoo-update](https://github.com/MHuiG/twikoo-update) 的实现方式。
