# ============================================================
# AdGuard Home 上游 DNS 分流配置
# ============================================================
# 适用版本：AdGuard Home v0.107+
# 最后更新：2025-05
# 开源地址：https://github.com/vip-weizhen/DNS
#
# 分流策略说明：
#   1. 国内域名        → 阿里DNS(主) + 腾讯DNSPod(备)   延迟低、无污染
#   2. GitHub/开发资源 → Google DNS + Cloudflare         抗污染能力强
#   3. 隐私敏感服务    → Quad9 + Cloudflare              注重隐私、过滤恶意
#   4. Meta系服务      → OpenDNS + Cloudflare            过滤能力强
#   5. 未匹配域名      → 默认上游兜底（见文件末尾）
#
# 使用方法：
#   将本文件内容粘贴到 AdGuard Home → 设置 → DNS设置 → 上游DNS服务器
#
# 测试配置是否生效：
#   nslookup baidu.com 223.5.5.5
#   nslookup google.com 8.8.8.8
# ============================================================
