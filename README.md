# publish-spec

> 产品发布规范

基于 git 分支作为开发环境区分，分为：

## 开发机

git分支： `master`

开发机用于开发人员在线调试前后端/第三方接口，和调试最新开发的功能。


## 预览机

git分支：`pre`

预览机保持环境与正式机一致，预览机数据库中应有测试预览所需的所有数据内容。必要时可从正式机同步数据（用户个人信息之外的数据不同步）。

预览机作为最终上线前最后一道检验平台，测试人员在预览机进行测试，产品人员在预览机验收功能。

## 正式机

git分支：`pro`

正式机即生产环境，生产环境只能通过 `pre`（预览机） 测试验收完成后合并至 `pro`（正式机） 发布。

## 后端目录结构

```bash
/config # 配置信息
```

`/config` 下存放所有配置文件，但在发布时不发布配置文件。配置文件由运维手动在服务中配置。


## 前端目录结构


```bash
/resource  # 前端静态资源未编译的源码
/public    # 网站入口和编译后的静态资源
```

基于 gitlab-ci 构建项目，当 gitlab-ci 的编译速度不能满足日常前端构建操作时，前端在本地构建完成后生成的[静态资源表](http://fis.baidu.com/fis3/docs/lv3.html#%E9%9D%99%E6%80%81%E8%B5%84%E6%BA%90%E6%98%A0%E5%B0%84%E8%A1%A8) 并将静态资源表添加至 `resource/resource_map.json`。 （编译后的静态资源发布至远程服务器，不存放在 git 中）
