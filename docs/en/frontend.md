# Frontend Deployment

## Deploy in Hexo 

### For [Hexo Butterfly](https://github.com/jerryc127/hexo-theme-butterfly) 

Please refer to [Butterfly 安裝文檔(四) 主題配置-2](https://butterfly.js.org/posts/ceeb73f/#%E8%A9%95%E8%AB%96) for configuration.

### For [Hexo Keep](https://github.com/XPoet/hexo-theme-keep) 

Please refer to [hexo-theme-keep/_config.yml](https://github.com/XPoet/hexo-theme-keep/blob/master/_config.yml) for configuration.

### For [Hexo Volantis](https://github.com/volantis-x/hexo-theme-volantis) 

Please refer to [hexo-theme-volantis/_config.yml](https://github.com/volantis-x/hexo-theme-volantis/blob/master/_config.yml) for configuration.

### For [Hexo Ayer](https://github.com/Shen-Yu/hexo-theme-ayer) 

Please refer to [hexo-theme-ayer/_config.yml](https://github.com/Shen-Yu/hexo-theme-ayer/blob/master/_config.yml) for configuration.

### For [Hexo NexT](https://github.com/next-theme/hexo-theme-next) 

**Versions below NexT 8 are not supported for now**, please upgrade to NexT 8 before executing the following in the Hexo project's root directory.

``` sh
# For NexT version >= 8.0.0 && < 8.4.0
npm install hexo-next-twikoo@1.0.0
# For NexT version >= 8.4.0
npm install hexo-next-twikoo@1.0.3
```

Then add the following to config file:

``` yml
twikoo:
  enable: true
  visitor: true
  envId: xxxxxxxxxxxxxxx # 腾讯云环境填 envId；Vercel 环境填地址（https://xxx.vercel.app）
  # region: ap-guangzhou # 环境地域，默认为 ap-shanghai，腾讯云环境填 ap-shanghai 或 ap-guangzhou；Vercel 环境不填
```

### For [Hexo Matery](https://github.com/blinkfox/hexo-theme-matery) 

Please refer to [hexo-theme-matery/_config.yml](https://github.com/blinkfox/hexo-theme-matery/blob/develop/_config.yml) for configuration.

### For [Hexo Icarus](https://github.com/ppoffice/hexo-theme-icarus) 

Please refer to [基于腾讯云，给你的 Icarus 博客配上 Twikoo 评论系统](https://www.anzifan.com/post/icarus_to_candy_2/).

### For [Hexo MengD(萌典)](https://github.com/lete114/hexo-theme-MengD) 

Please refer to [hexo-theme-MengD/_config.yml](https://github.com/lete114/hexo-theme-MengD/blob/master/_config.yml) for configuration.

### For [hexo-theme-fluid](https://github.com/fluid-dev/hexo-theme-fluid) 

Please refer to [配置指南-评论](https://hexo.fluid-dev.com/docs/guide/#%E8%AF%84%E8%AE%BA) for configuration.

### For [hexo-theme-cards](https://github.com/ChrAlpha/hexo-theme-cards) 

Please refer to [hexo-theme-cards/_config.yml](https://github.com/ChrAlpha/hexo-theme-cards/blob/master/_config.yml) for configuration.

### For [maupassant-hexo](https://github.com/tufu9441/maupassant-hexo) 

Please refer to [maupassant-hexo/_config.yml](https://github.com/tufu9441/maupassant-hexo/blob/master/_config.yml) for configuration.

### For [hexo-theme-redefine](https://github.com/EvanNotFound/hexo-theme-redefine) 

Please refer to [Redefine 官方文档 #comment](https://redefine-docs.ohevan.com/docs/configuration-guide/comment#twikoo) for configuration.

## Deploy in Hugo 

### For [hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack) 

Please refer to [Comments | Stack](https://stack.jimmycai.com/config/comments) and [hugo-theme-stack/config.yaml#L83](https://github.com/CaiJimmy/hugo-theme-stack/blob/master/config.yaml#L83) for configuration.

### For [FixIt](https://github.com/hugo-fixit/FixIt) 

Please refer to [入门篇 - FixIt #主题配置](https://fixit.lruihao.cn/zh-cn/documentation/basics/#theme-configuration) and [hugo-fixit/FixIt/config.toml#L613-L624](https://github.com/hugo-fixit/FixIt/blob/8bb2a35dcc4c54fc3e0fb968df063d6be1daabf3/config.toml#L613-L624) for configuration.

## Load from CDN

::: tip Tip
If your blog theme doesn't support Twikoo and you are unsure how to load Twikoo, you can [submit an adaptation request on Github](https://github.com/twikoojs/twikoo/issues/new)
:::

``` html
<div id="tcomment"></div>
<script src="https://cdn.staticfile.org/twikoo/1.6.31/twikoo.all.min.js"></script>
<script>
twikoo.init({
  envId: 'your envID', // 腾讯云环境填 envId；Vercel 环境填地址（https://xxx.vercel.app）
  el: '#tcomment', // 容器元素
  // region: 'ap-guangzhou', // 环境地域，默认为 ap-shanghai，腾讯云环境填 ap-shanghai 或 ap-guangzhou；Vercel 环境不填
  // path: location.pathname, // 用于区分不同文章的自定义 js 路径，如果您的文章路径不是 location.pathname，需传此参数
  // lang: 'zh-CN', // 用于手动设定评论区语言，支持的语言列表 https://github.com/twikoojs/twikoo/blob/main/src/client/utils/i18n/index.js
})
</script>
```

> It is recommended that users who use a CDN to load Twikoo lock the version on the linked address, to avoid future non-compatible updates from Twikoo.

### 更换 CDN 镜像

如果遇到默认 CDN 加载速度缓慢，可更换其他 CDN 镜像。以下为可供选择的公共 CDN，其中一些 CDN 可能需要数天时间同步最新版本：

* `https://cdn.staticfile.org/twikoo/1.6.31/twikoo.all.min.js`
* `https://lib.baomitu.com/twikoo/1.6.31/twikoo.all.min.js`
* `https://cdn.bootcdn.net/ajax/libs/twikoo/1.6.31/twikoo.all.min.js`
* `https://cdn.jsdelivr.net/npm/twikoo@1.6.31/dist/twikoo.all.min.js`

## 开启管理面板（腾讯云环境）

1. 进入[环境-登录授权](https://console.cloud.tencent.com/tcb/env/login)，点击“自定义登录”右边的“私钥下载”，下载私钥文件
2. 用文本编辑器打开私钥文件，复制全部内容
3. 点击评论窗口的“小齿轮”图标，粘贴私钥文件内容，并设置管理员密码

配置好登录私钥之后无需留存私钥文件，请勿再次下载登录私钥，否则会导致之前配置的登录私钥失效。

## 开启管理面板（非腾讯云环境）

点击评论窗口的“小齿轮”图标，设置管理员密码
