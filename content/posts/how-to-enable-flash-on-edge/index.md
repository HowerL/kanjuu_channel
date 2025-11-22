+++
title = "Edge Chromium 中如何始终允许运行 Flash 内容"
date = "2020-02-18"
draft = false
tags = ["Windows"]
categories = ["解决方案"]
+++

众所周知，由于 Adobe Flash 控件历史久远，积累了许多漏洞。早在 2017 年 7 月，Adobe 就宣布了要在 2020 年底终止对 Flash 的支持。微软称其浏览器移除 Flash 插件的最后期限是 **2020 年 12 月**前。

但由于国内的主流网站都还大量使用 Flash ，因此我们需要一种办法解决此问题，使 Flash 内容能够被正确加载，而不是即点即用（先询问）的模式。

我们需要借用到 Chromium 的 **Policy**（策略）功能，该功能由组织管理，实则可以通过**注册表**来实现操作，请谨慎。

本文以 Edge 80.0.361.54 x64 / Windows 10 专业版 1909 (18363.592) x64 为演示。

---

一、进入**注册表编辑器** 可以使用 `Win + R` 组合键调出“**运行**”窗口，输入 `regedit` 即可。

二、进入 `\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge\PluginsAllowedForUrls` 项，一般情况下该项不存在（如有请忽略），因此我们需要在 `\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\` 下右键新建项 `Edge` （注意大小写）—— 在 `Edge` 下新建项 `PluginsAllowedForUrls` （注意大小写）

三、在 `\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge\PluginsAllowedForUrls` 中新建字符串值，数值名称为 `1` ，双击该数值，设置数值数据为 `https://*`

四、在 `\HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge\PluginsAllowedForUrls` 中新建字符串值，数值名称为 `2` ，双击该数值，设置数值数据为 `http://*`

五、请检查注册表设置是否如图所示：

![](edge_reg.jpg)

六、重新打开 Edge Chromium 浏览器，在地址框中访问 `edge://policy/` 以确认该策略是否被应用，并打开设置，查看页面顶部是否显示“**你的浏览器由你的组织进行管理**”，如有则已设置完成。

---

以下为专业人士准备的*相关链接* ：

> - 关于 Edge Chromium 的更多内容，请访问：https://www.microsoft.com/en-us/edge
> - 关于详细的 Policy（策略）内容，请查询 Microsoft Edge 浏览器策略文档：https://docs.microsoft.com/zh-cn/DeployEdge/microsoft-edge-policies#pluginsallowedforurls 注意：该内容仅适用 Edge Chromium（即 Microsoft Edge 版本 77 或更高）

策略文档中关于 **PluginsAllowedForUrls** 内容如下：_允许特定网站上的 Adobe Flash 插件_

Windows 注册表设置

- 路径（必需）： `SOFTWARE\Policies\Microsoft\Edge\PluginsAllowedForUrls`
- 路径（推荐）： N/A
- 值名称：1，2，3，...
- 值类型： REG_SZ 列表
