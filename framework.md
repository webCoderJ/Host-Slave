## Micro - FE - Architecture

### Node Server Express

Middleware based

-   静态资源分发
-   请求转发
    -   根据项目前缀对不同项目前缀做请求转发
-   登录鉴权
-   子项目注册、更新机制(Host 根据此数据生成子项目菜单以及对应页面)
    -   文件上传至对应目录
    -   接口注册相应权限
-   DB
    -   子项目数据

### Vue 子项目运行器 `Host`

-   提供 宿主环境(vue、router、vuex、ui-lib)
-   公共 JS、CSS 等其他资源承载
-   提供公共 API 供子项目使用

    -   注册 vuex
    -   注册 router
    -   注册 命名空间
    -   Api 请求资源注册、卸载

-   子项目路由动态注册、导航自动生成
-   项目作用域控制，为了避免各个子项目中使用的冲突
    -   css，给所有的 css 加上项目前缀
    -   js

### Vue 子项目 `Slave`

-   编译输出对应 css/js 等其他静态资源
-   独立 Store

### DEV

-   引用 Host
-   devServer
    -   Mock
    -   本地转发
-   webpack - external
-   webpack - css 添加前缀

### 构建部署、交付形态

以 dist 包为交付介质，只包含静态文件，无 html 文件

1.  子项目单独构建打包
2.  Copy 到 Host-serve 目录，目录名为子项目名
3.  把子项目的 entry 文件引入到 host 的 index.html
4.  使用 Host-register-api 注册子项目

### 微服务

-   打包机制
