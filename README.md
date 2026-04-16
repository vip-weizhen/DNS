AdGuardHome 上游 DNS 分流配置

简介

这是一套针对国内网络环境优化的 AdGuardHome 上游 DNS 分流配置。通过将不同域名指向最适合的 DNS 服务器，实现：

✅ 国内网站低延迟：使用阿里/腾讯 DoH，解析速度快

✅ 国际网站防污染：GitHub、Google 等使用海外可信 DNS

✅ 苹果/微软服务加速：Windows 更新、iCloud 等走国内 DNS，CDN 调度更优

✅ 开发资源优化：npm、pip、docker 等海外源使用国际 DNS

文件结构
AdGuardHomeDNSRules
直接复制到 AdGuardHome 的 设置 → DNS 设置 → 上游 DNS 服务器 中即可使用。

分流规则概览

分类	规则示例	使用的 DNS

国内顶级域名	*.cn、*.gov.cn、*.edu.cn	阿里 + 腾讯 DoH

主流互联网公司	QQ、阿里、百度、字节、B站、京东等	阿里 + 腾讯 DoH

苹果服务	iCloud、App Store、推送服务	阿里 + 腾讯 DoH

微软服务	Windows Update、OneDrive、Office	阿里 + 腾讯 DoH

GitHub 全家桶	github.com、raw、assets 等	Google + Cloudflare DoH

开发资源	npm、pypi、docker、golang	Google + Cloudflare DoH

Google 系	YouTube、gstatic、recaptcha	Google + Cloudflare DoH

Meta 系	Facebook、Instagram、WhatsApp	OpenDNS + Cloudflare DoH

推特/X	twitter.com、x.com	Quad9 + Cloudflare DoH

流媒体	Netflix、Disney+、Hulu、Twitch	OpenDNS + Cloudflare DoH

Steam/游戏	Steam、Epic、暴雪、米哈游	阿里 + 腾讯 DoH

默认上游	未匹配的域名	阿里 + 腾讯 + Cloudflare + Quad9 + Google + OpenDNS

上游 DNS 服务器说明

DNS 服务器	类型	用途

https://dns.alidns.com/dns-query	DoH	阿里 DNS，国内主力

https://doh.pub/dns-query	DoH	腾讯 DNS，国内主力

https://dns.google/dns-query	DoH	Google DNS，海外防污染

https://cloudflare-dns.com/dns-query	DoH	Cloudflare DNS，海外备选

https://dns.quad9.net/dns-query	DoH	Quad9 DNS，隐私保护

https://dns.opendns.com/dns-query	DoH	OpenDNS，Meta/流媒体优化

使用方法

方法一：直接粘贴（推荐）

打开 AdGuardHome 管理界面

进入 设置 → DNS 设置

在 上游 DNS 服务器 输入框中，直接粘贴配置文件内容

滚动到底部，点击 应用

方法二：上传文件

将配置文件保存为 upstream-dns.conf

在 AdGuardHome 中，点击 从文件读取 按钮

选择上传该文件

Bootstrap DNS 推荐

由于配置中使用了 DoH/DoT 服务器（域名形式），需要配置 Bootstrap DNS 来解析这些域名：

223.5.5.5

119.29.29.29

114.114.114.114

在 设置 → DNS 设置 → Bootstrap DNS 服务器 中填入上述 IP。

注意事项

规则顺序：AdGuardHome 按从上到下的顺序匹配，更具体的域名建议放在前面

性能影响：分流规则约 200+ 条，对性能基本无影响

IPv6 用户：如使用 IPv6，建议配置对应的 IPv6 DNS 或关闭 IPv6 DNS 解析

自定义修改：可根据个人需求增删域名规则

更新日志

2026-04-16

初始版本发布

覆盖国内主流互联网公司

覆盖国际常用服务（Google、Meta、推特、Telegram 等）

覆盖开发资源（npm、pypi、docker 等）

覆盖流媒体服务（Netflix、Disney+ 等）

许可证

MIT License

贡献

欢迎提交 Issue 或 Pull Request 来完善规则：

补充遗漏的常用域名

修正失效的 DNS 服务器

优化规则匹配顺序

Star History
如果这个配置对你有帮助，欢迎点个 ⭐️ 支持一下～
