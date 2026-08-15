# 📊 2026年流量监控与智能管理完全指南

> 本仓库专注于机场订阅的流量监控与智能管理，帮助你全面了解流量消耗情况、设置智能预警、实现精细化的流量管理。无论是个人使用还是家庭共享，都能实现流量使用的可视化与可控化。

## 📋 目录导航

- [流量监控的重要性](#流量监控的重要性)
- [各平台流量统计](#各平台流量统计)
- [流量预警设置](#流量预警设置)
- [流量节省技巧](#流量节省技巧)
- [智能流量分配](#智能流量分配)
- [流量偷跑检测](#流量偷跑检测)
- [自动化管理方案](#自动化管理方案)
- [常见问题与解决方案](#常见问题与解决方案)

---

## 🎯 流量监控的重要性

### 为什么需要流量监控

#### 流量管理三大痛点

| 痛点 | 影响 | 解决方案 |
|------|------|---------|
| **超流量被限速** | 速度骤降影响使用 | 设置预警提前知晓 |
| **流量不明消耗** | 不知去向的流量 | 深度监控分析 |
| **共享流量不均** | 家庭成员使用不透明 | 分设备流量统计 |

#### 流量消耗的主要场景

**高流量消耗排行**

| 排名 | 应用类型 | 平均小时消耗 | 说明 |
|------|---------|-------------|------|
| 1 | 4K 视频流媒体 | 15-20GB | Netflix/Disney+ 4K |
| 2 | 文件下载 | 取决于文件 | P2P/云盘/直链 |
| 3 | 游戏更新 | 50-100GB | 主机/PC 游戏 |
| 4 | 系统更新 | 5-20GB | OS/应用更新 |
| 5 | 在线游戏 | 1-5GB | 实时联网游戏 |
| 6 | 视频通话 | 1-3GB | 1080P 会议 |
| 7 | 社交媒体 | 500MB-2GB | 视频/图片加载 |

### 流量监控的核心指标

#### 基础指标

| 指标 | 说明 | 参考值 |
|------|------|--------|
| 月总流量 | 每月消耗总量 | 套餐流量上限 |
| 日均流量 | 平均每天消耗 | 月流量÷30 |
| 峰值流量 | 单日最高消耗 | 异常检测基准 |
| 剩余流量 | 当月可用流量 | 提前续费参考 |

#### 进阶指标

| 指标 | 说明 | 应用场景 |
|------|------|---------|
| 时段分布 | 流量使用时间段 | 优化连接策略 |
| 设备分布 | 各设备消耗占比 | 家庭管理 |
| 协议分布 | 各协议流量占比 | 协议优化 |
| 节点分布 | 各节点流量占比 | 节点选择 |
| 应用分布 | 各应用消耗占比 | 行为分析 |

---

## 📱 各平台流量统计

### Clash for Windows 流量统计

#### 内置流量统计

```
Clash for Windows > 统计

显示内容：
- 当前会话上传/下载流量
- 累计上传/下载总量
- 各代理组流量统计
- 连接数统计
```

#### 日志分析

```powershell
# PowerShell 统计 Clash 日志
$logPath = "$env:APPDATA\Clash for Windows\logs"
$today = Get-Date -Format "yyyy-MM-dd"

# 统计今日流量
$todayLogs = Get-Content "$logPath\*.log" | Where-Object { $_ -match $today }

$upload = ($todayLogs | Select-String "upload" | Measure-Object).Count
$download = ($todayLogs | Select-String "download" | Measure-Object).Count

Write-Host "今日上传记录: $upload"
Write-Host "今日下载记录: $download"
```

### Clash for Android 流量监控

#### 实时流量显示

```
Clash for Android > 主界面

显示内容：
- 当前连接状态
- 实时上传/下载速度
- 本会话总流量
- 今日累计流量
```

#### 数据导出

```bash
# 使用 ADB 导出 Clash 数据
adb shell "am start -n com.github.kr328.clash/.MainActivity"
adb shell "run-as com.github.kr328.clash cat files/premiumUidMap.txt"
```

### OpenClash 流量监控

#### LuCI 流量统计

```
OpenClash > 流量统计

功能：
- 实时流量监控
- 历史流量记录
- 流量排行榜
- 带宽使用率
```

#### OpenWrt 流量监控脚本

```bash
#!/bin/bash
# openwrt-traffic-monitor.sh

# 获取接口流量
LAN_IFACE="br-lan"
WAN_IFACE="eth0"

# 读取流量数据
LAN_RX=$(cat /sys/class/net/$LAN_IFACE/statistics/rx_bytes)
LAN_TX=$(cat /sys/class/net/$LAN_IFACE/statistics/tx_bytes)
WAN_RX=$(cat /sys/class/net/$WAN_IFACE/statistics/rx_bytes)
WAN_TX=$(cat /sys/class/net/$WAN_IFACE/statistics/tx_bytes)

# 转换为 MB
LAN_RX_MB=$((LAN_RX / 1024 / 1024))
LAN_TX_MB=$((LAN_TX / 1024 / 1024))
WAN_RX_MB=$((WAN_RX / 1024 / 1024))
WAN_TX_MB=$((WAN_TX / 1024 / 1024))

echo "=== OpenWrt 流量统计 ==="
echo "LAN 接收: ${LAN_RX_MB} MB"
echo "LAN 发送: ${LAN_TX_MB} MB"
echo "WAN 接收: ${WAN_RX_MB} MB"
echo "WAN 发送: ${WAN_TX_MB} MB"
echo "总计: $(( (LAN_RX + LAN_TX + WAN_RX + WAN_TX) / 1024 / 1024 )) MB"
```

### iOS/Android 应用级流量监控

#### iOS 系统流量统计

```
设置 > 蜂窝网络 > 蜂窝数据用量

功能：
- 各应用流量使用
- 系统服务流量
- VPN 流量统计
```

#### Android 系统流量统计

```
设置 > 网络与互联网 > 数据Saver > 数据使用量

功能：
- 应用级流量统计
- 按 Wi-Fi/移动数据分类
- 流量使用历史
```

---

## ⚠️ 流量预警设置

### 预警策略设计

#### 预警级别

| 级别 | 触发条件 | 通知方式 | 处理建议 |
|------|---------|---------|---------|
| ⚪ 正常 | < 70% 使用 | 无需通知 | 正常使用 |
| 🟡 提醒 | 70-85% 使用 | 推送通知 | 注意节省 |
| 🟠 警告 | 85-95% 使用 | 推送+邮件 | 谨慎使用 |
| 🔴 紧急 | > 95% 使用 | 推送+短信 | 立即行动 |
| ⚫ 超限 | 100% 使用 | 紧急通知 | 续费或等待 |

### OpenClash 预警配置

#### 邮件预警设置

```bash
# 配置邮件通知
# LuCI > 系统 > 计划任务

# 添加 cron 任务
0 */6 * * * /root/scripts/traffic-check.sh

# traffic-check.sh 脚本内容
#!/bin/bash

# 获取订阅信息
SUBSCRIPTION_URL="https://clashvip.net/api/subscription"
USAGE=$(curl -s "$SUBSCRIPTION_URL" | grep -o '"used":[0-9]*' | cut -d: -f2)
LIMIT=$(curl -s "$SUBSCRIPTION_URL" | grep -o '"limit":[0-9]*' | cut -d: -f2)

# 计算使用百分比
PERCENTAGE=$(( USAGE * 100 / LIMIT ))

# 判断并发送通知
if [ $PERCENTAGE -ge 85 ]; then
    curl -s -X POST "https://api.pushplus.plus/send" \
        -d "token=YOUR_TOKEN" \
        -d "title=流量预警" \
        -d "content=您的流量已使用 ${PERCENTAGE}%，请注意节省"
fi
```

#### 推送预警设置

```bash
# 使用 PushPlus 推送通知
# https://pushplus.plus

PUSH_TOKEN="your_push_token"

send_notification() {
    local title="$1"
    local content="$2"
    
    curl -s -X POST "https://www.pushplus.plus/send" \
        -H "Content-Type: application/json" \
        -d "{
            \"token\": \"$PUSH_TOKEN\",
            \"title\": \"$title\",
            \"content\": \"$content\"
        }"
}

# 流量检查函数
check_traffic() {
    local usage=$1
    local limit=$2
    local percentage=$(( usage * 100 / limit ))
    
    if [ $percentage -ge 90 ]; then
        send_notification "流量紧急预警" "您的流量已使用 ${percentage}%，即将用尽！"
    elif [ $percentage -ge 70 ]; then
        send_notification "流量提醒" "您的流量已使用 ${percentage}%，请注意使用"
    fi
}
```

### 智能预警脚本

#### 综合预警脚本

```powershell
# traffic-alert.ps1
# Clash 流量预警脚本

param(
    [string]$PushPlusToken = "YOUR_TOKEN",
    [int]$WarningThreshold = 70,
    [int]$CriticalThreshold = 90
)

$ErrorActionPreference = "Stop"

# 从订阅 API 获取流量信息
# 注意：实际使用时请替换为真实的 API 地址
$apiUrl = "https://clashvip.net/api/subscription/info"
$response = Invoke-RestMethod -Uri $apiUrl -Headers @{
    "Authorization" = "Bearer YOUR_TOKEN"
}

$usedGB = [math]::Round($response.used / 1024, 2)
$limitGB = [math]::Round($response.limit / 1024, 2)
$percentage = [math]::Round(($response.used / $response.limit) * 100, 1)
$remainingGB = [math]::Round(($response.limit - $response.used) / 1024, 2)

Write-Host "=== 流量使用情况 ===" -ForegroundColor Cyan
Write-Host "已使用: ${usedGB} GB / ${limitGB} GB" -ForegroundColor Yellow
Write-Host "使用率: ${percentage}%" -ForegroundColor Yellow
Write-Host "剩余: ${remainingGB} GB" -ForegroundColor Green

# 发送预警通知
if ($percentage -ge $CriticalThreshold) {
    $title = "🚨 流量紧急预警"
    $content = @"
您的 Clash 订阅流量已使用 ${percentage}%！

📊 当前状态：
- 已使用: ${usedGB} GB / ${limitGB} GB
- 剩余: ${remainingGB} GB
- 使用率: ${percentage}%

⚠️ 请尽快续费或等待流量重置！
"@
    
    # 发送推送通知
    curl -s -X POST "https://www.pushplus.plus/send" `
        -H "Content-Type: application/json" `
        -d @{
            token = $PushPlusToken
            title = $title
            content = $content
        }
    
    Write-Host "🚨 已发送紧急预警！" -ForegroundColor Red
    
} elseif ($percentage -ge $WarningThreshold) {
    $title = "⚠️ 流量提醒"
    $content = @"
您的 Clash 订阅流量已使用 ${percentage}%。

📊 当前状态：
- 已使用: ${usedGB} GB / ${limitGB} GB
- 剩余: ${remainingGB} GB
- 使用率: ${percentage}%

💡 建议注意流量使用，避免超限。
"@
    
    curl -s -X POST "https://www.pushplus.plus/send" `
        -H "Content-Type: application/json" `
        -d @{
            token = $PushPlusToken
            title = $title
            content = $content
        }
    
    Write-Host "⚠️ 已发送提醒通知！" -ForegroundColor Yellow
} else {
    Write-Host "✅ 流量使用正常" -ForegroundColor Green
}
```

---

## 💰 流量节省技巧

### 应用级流量优化

#### 视频流媒体节省

| 平台 | 节省方式 | 节省比例 |
|------|---------|---------|
| YouTube | 设置 720P/1080P | 节省 50-70% |
| Netflix | 设置中低画质 | 节省 40-60% |
| Disney+ | 限制下载质量 | 节省 30-50% |
| Bilibili | 关闭自动播放 | 节省 20-30% |

#### 视频设置脚本

```powershell
# video-quality-optimizer.ps1
# 自动优化视频平台画质设置

Write-Host "=== 视频平台画质优化工具 ===" -ForegroundColor Cyan

# YouTube 画质限制建议
Write-Host "`nYouTube 推荐设置：" -ForegroundColor Yellow
Write-Host "1. 画质偏好：Auto (自动)"
Write-Host "2. 数据保护模式：启用"
Write-Host "3. 限制移动网络画质：720P"

# Netflix 画质建议
Write-Host "`nNetflix 推荐设置：" -ForegroundColor Yellow
Write-Host "1. 播放设置：自动"
Write-Host "2. 下载画质：中（建议）"
Write-Host "3. 下载数量：限制"

# 通用建议
Write-Host "`n💡 通用流量节省技巧：" -ForegroundColor Cyan
Write-Host "1. 关闭视频自动播放"
Write-Host "2. 禁止后台视频加载"
Write-Host "3. 使用数据Saver模式"
Write-Host "4. 优先使用 Wi-Fi 下载"
Write-Host "5. 定期清理缓存"
```

### 协议级流量优化

#### 低带宽协议选择

| 协议 | 流量效率 | 推荐场景 | 节省比例 |
|------|---------|---------|---------|
| VLESS + XTLS | 高 | 通用推荐 | 基准 |
| Trojan | 中 | 稳定性优先 | 0-10% |
| Shadowsocks | 中 | 兼容性优先 | 0-10% |
| WireGuard | 极高 | 大流量场景 | 20-40% |

#### 协议优化配置

```yaml
# 流量优化配置示例
# 选择 WireGuard 协议可节省 20-40% 流量

# WireGuard 配置示例
proxies:
  - name: WireGuard-优化
    type: wireguard
    server: wg.clashvip.net
    port: 51820
    ipv6: false
    private-key: your-private-key
    peer-public-key: server-public-key
    reserved: [0, 0, 0]
    mtu: 1420
    local-address:
      - 10.0.0.2/32

# 或者使用 Hysteria2（QUIC协议，高压缩比）
proxies:
  - name: Hysteria2-省流量
    type: hysteria2
    server: hy2.clashvip.net
    port: 443
    auth: your-auth
    up: "100 Mbps"
    down: "100 Mbps"
    sni: example.com
    alpn:
      - h3
    skip-cert-verify: false
```

### 系统级流量控制

#### Windows 流量限制

```powershell
# windows-qos.ps1
# Windows QoS 流量控制

# 设置 Clash 进程优先级
Get-Process -Name "Clash for Windows" | 
    ForEach-Object { 
        $_.PriorityClass = "High" 
        Write-Host "已将 Clash 进程设置为高优先级" -ForegroundColor Green
    }

# 限制后台应用流量
Set-NetQoSPriority -Name "Clash" -PriorityValue 10

# 禁用 Windows Update（节省大量流量）
net stop wuauserv
sc config wuauserv start= disabled
Write-Host "已禁用 Windows Update 自动更新" -ForegroundColor Yellow
```

#### macOS 流量限制

```bash
# macos-traffic-control.sh

# 限制 Time Machine 备份频率
sudo tmutil setdestinations /path/to/backups
sudo tmutil thinlocalsnapshots 999 1

# 禁用自动 macOS 更新
sudo softwareupdate --schedule off

# 限制 App Store 自动下载
defaults write com.apple.SoftwareUpdate AutomaticDownload -bool false

echo "已优化 macOS 流量设置"
```

---

## 🧠 智能流量分配

### 流量配额策略

#### 个人配额设计

```yaml
# 月流量 500GB 配额分配示例

流量配额:
  日常工作: 100GB/月
    - 邮件收发
    - 文档同步
    - 视频会议
    - 浏览器浏览
  
  视频娱乐: 250GB/月
    - YouTube: 100GB
    - Netflix: 80GB
    - 其他: 70GB
  
  游戏下载: 100GB/月
    - 游戏更新
    - 补丁下载
  
  备用缓冲: 50GB/月
    - 系统更新
    - 其他消耗
```

#### 家庭配额设计

| 成员 | 月配额 | 用途 | 超额处理 |
|------|-------|------|---------|
| 父亲 | 200GB | 办公+娱乐 | 降速至 2Mbps |
| 母亲 | 100GB | 社交+视频 | 降速至 2Mbps |
| 孩子 | 50GB | 学习+娱乐 | 完全阻断 |
| 访客 | 20GB/人 | 临时使用 | 禁止上网 |
| 公共 | 130GB | 电视+设备 | 共享使用 |

### OpenWrt 流量配额

#### 基于 MAC 的流量限制

```bash
# openwrt-quota.sh
# OpenWrt 流量配额管理脚本

# 获取已连接设备
arp | grep br-lan | awk '{print $3, $1}'

# 为特定设备设置流量限制
# 假设孩子设备 MAC 为 AA:BB:CC:DD:EE:FF
CHILD_MAC="AA:BB:CC:DD:EE:FF"
MONTHLY_LIMIT_GB=50

# 使用 iptables 记录流量
iptables -A INPUT -m mac --mac-source $CHILD_MAC -j RETURN
iptables -A OUTPUT -d 192.168.1.121 -j RETURN

# 创建流量统计链
iptables -N TRAFFIC_COUNT
iptables -A INPUT -j TRAFFIC_COUNT
iptables -A OUTPUT -j TRAFFIC_COUNT

echo "流量统计已启用"
```

#### QoS 流量整形

```bash
# openwrt-qos.sh
# OpenWrt QoS 流量整形配置

# 安装 QoS 组件
opkg install luci-app-qos

# 配置 QoS
# LuCI > 网络 > QoS

# 上行带宽设置（根据实际带宽调整）
UPLOAD=50  # Mbps

# 下行带宽设置
DOWNLOAD=200  # Mbps

# QoS 规则优先级
# 1. SSH (最高)
# 2. 游戏
# 3. 视频会议
# 4. 网页浏览
# 5. P2P 下载 (最低)

cat > /etc/config/qos << 'EOF'
config qos wan
    option enabled '1'
    option upload '$UPLOAD'
    option download '$DOWNLOAD'

# 高优先级：SSH
config classify
    option target 'Priority'
    option proto 'tcp'
    option ports '22'
    option comment 'SSH'

# 中优先级：游戏
config classify
    option target 'Normal'
    option proto 'udp'
    option ports '3478,3479,3480'
    option comment 'Game'

# 低优先级：P2P
config classify
    option target 'Bulk'
    option proto 'tcp'
    option ports '6881,6882,6883'
    option comment 'P2P'
EOF

/etc/init.d/qos restart
echo "QoS 已启用"
```

---

## 🔍 流量偷跑检测

### 偷跑原因分析

#### 常见偷跑来源

| 来源 | 消耗量 | 检测难度 | 解决方案 |
|------|--------|---------|---------|
| 系统更新 | 高 | 易 | 禁用自动更新 |
| 云同步 | 中 | 中 | 调整同步策略 |
| 后台应用 | 中 | 中 | 限制后台活动 |
| 广告追踪 | 低 | 难 | 使用广告拦截 |
| DNS 泄漏 | 低 | 难 | 启用 fake-ip |
| WebRTC 泄漏 | 低 | 难 | 禁用 WebRTC |

### 流量异常检测

#### 实时监控脚本

```powershell
# traffic-monitor.ps1
# 实时流量异常检测

param(
    [int]$AlertThresholdMB = 100,  # 每小时超过 100MB 报警
    [int]$CheckIntervalSec = 60
)

Write-Host "=== 流量异常监控系统 ===" -ForegroundColor Cyan
Write-Host "监控间隔: ${CheckIntervalSec}秒" -ForegroundColor Yellow
Write-Host "告警阈值: ${AlertThresholdMB}MB/小时" -ForegroundColor Yellow
Write-Host "按 Ctrl+C 停止监控`n" -ForegroundColor Gray

$lastCheck = Get-Date
$lastRx = (Get-NetAdapterStatistics | Where-Object { $_.Name -eq "以太网" }).ReceivedBytes
$lastTx = (Get-NetAdapterStatistics | Where-Object { $_.Name -eq "以太网" }).SentBytes

while ($true) {
    Start-Sleep -Seconds $CheckIntervalSec
    
    $now = Get-Date
    $currentRx = (Get-NetAdapterStatistics | Where-Object { $_.Name -eq "以太网" }).ReceivedBytes
    $currentTx = (Get-NetAdapterStatistics | Where-Object { $_.Name -eq "以太网" }).SentBytes
    
    $rxDiff = ($currentRx - $lastRx) / 1MB
    $txDiff = ($currentTx - $lastTx) / 1MB
    $totalDiff = $rxDiff + $txDiff
    
    $elapsedMin = ($now - $lastCheck).TotalMinutes
    $hourlyRate = $totalDiff / $elapsedMin * 60
    
    # 显示实时状态
    $color = if ($hourlyRate -gt $AlertThresholdMB) { "Red" } elseif ($hourlyRate -gt ($AlertThresholdMB * 0.7)) { "Yellow" } else { "Green" }
    Write-Host "[$($now.ToString('HH:mm:ss'))] 实时: $([math]::Round($totalDiff, 2))MB | 预估小时: $([math]::Round($hourlyRate, 0))MB" -ForegroundColor $color
    
    # 异常告警
    if ($hourlyRate -gt $AlertThresholdMB) {
        Write-Host "⚠️ 检测到异常流量消耗！当前速率：$([math]::Round($hourlyRate, 0))MB/小时" -ForegroundColor Red
        
        # 列出高流量进程
        $highTrafficProcesses = Get-Process | Where-Object { $_.WorkingSet64 -gt 100MB } | 
            Select-Object Name, @{Name="Memory(MB)";Expression={[math]::Round($_.WorkingSet64/1MB,0)}} |
            Sort-Object "Memory(MB)" -Descending | Select-Object -First 5
        
        Write-Host "`n可能的高流量进程：" -ForegroundColor Yellow
        $highTrafficProcesses | Format-Table -AutoSize
    }
    
    $lastCheck = $now
    $lastRx = $currentRx
    $lastTx = $currentTx
}
```

#### 深度流量分析

```powershell
# deep-traffic-analysis.ps1
# 深度流量分析脚本

Write-Host "=== 深度流量分析 ===" -ForegroundColor Cyan

# 1. 检查 DNS 泄漏
Write-Host "`n[1] DNS 泄漏检测" -ForegroundColor Yellow
$dnsLeaks = Resolve-DnsName "whoami.akamai.net" -Type A -Server 8.8.8.8
Write-Host "DNS 解析结果: $($dnsLeaks.IPAddress)"

# 2. 检查 WebRTC 泄漏
Write-Host "`n[2] WebRTC 泄漏检测" -ForegroundColor Yellow
# 注意：需要浏览器环境
Write-Host "请访问 https://browserleaks.com/webrtc 进行检测"

# 3. 检查代理状态
Write-Host "`n[3] 代理状态检测" -ForegroundColor Yellow
$proxyStatus = Get-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
Write-Host "代理启用: $($proxyStatus.ProxyEnable -eq 1)"
Write-Host "代理服务器: $($proxyStatus.ProxyServer)"

# 4. 检查 Clash 日志
Write-Host "`n[4] Clash 日志分析" -ForegroundColor Yellow
$clashLog = Get-Content "$env:APPDATA\Clash for Windows\logs\*.log" -Tail 100 -ErrorAction SilentlyContinue
$errors = $clashLog | Select-String "error|failed|timeout" -SimpleMatch
if ($errors) {
    Write-Host "检测到 $($errors.Count) 条错误日志" -ForegroundColor Red
    $errors | Select-Object -First 5 | ForEach-Object { Write-Host $_.Line -ForegroundColor Gray }
} else {
    Write-Host "未检测到明显错误" -ForegroundColor Green
}

# 5. 网络连接分析
Write-Host "`n[5] 活动连接分析" -ForegroundColor Yellow
$connections = Get-NetTCPConnection -State Established | 
    Where-Object { $_.RemoteAddress -notmatch "^192\.168|^10\.|^172\.(1[6-9]|2[0-9]|3[01])\." } |
    Select-Object RemoteAddress, RemotePort, OwningProcess |
    Group-Object RemoteAddress |
    Select-Object Name, Count |
    Sort-Object Count -Descending |
    Select-Object -First 10

Write-Host "外部连接统计（前10）：" -ForegroundColor Cyan
$connections | Format-Table -AutoSize
```

---

## ⚙️ 自动化管理方案

### 定时任务配置

#### 每日流量报告

```powershell
# daily-traffic-report.ps1
# 每日流量报告生成

param(
    [string]$WebhookUrl = "YOUR_WEBHOOK_URL"
)

# 获取今日流量数据
$today = Get-Date -Format "yyyy-MM-dd"
$reportTime = Get-Date -Format "yyyy年MM月dd日 HH:mm"

# 模拟数据（实际使用时从 API 获取）
$usedGB = 15.6
$limitGB = 100
$percentage = [math]::Round(($usedGB / $limitGB) * 100, 1)
$remainingGB = [math]::Round($limitGB - $usedGB, 2)

# 生成报告
$report = @"
📊 Clash 流量日报
📅 日期: $reportTime

📈 流量使用情况：
• 已使用: ${usedGB} GB / ${limitGB} GB
• 使用率: ${percentage}%
• 剩余: ${remainingGB} GB

$(if ($percentage -ge 80) { "⚠️ 流量使用率较高，请注意节省" } else { "✅ 流量使用正常" })

---
由 Clash 流量管理助手自动生成
"@

Write-Host $report

# 发送到 Webhook
if ($WebhookUrl) {
    Invoke-RestMethod -Uri $WebhookUrl -Method Post -Body (@{ content = $report } | ConvertTo-Json) -ContentType "application/json"
}
```

#### 定时任务设置

```powershell
# 创建每日报告任务
$action = New-ScheduledTaskAction -Execute "powershell.exe" -Argument "-ExecutionPolicy Bypass -File C:\Scripts\daily-traffic-report.ps1"
$trigger = New-ScheduledTaskTrigger -Daily -At "21:00"
$settings = New-ScheduledTaskSettingsSet -AllowStartIfOnBatteries -DontStopIfGoingOnBatteries

Register-ScheduledTask -TaskName "ClashDailyReport" -Action $action -Trigger $trigger -Settings $settings -Description "每日 Clash 流量报告"

# 创建流量预警检查任务（每6小时）
$alertAction = New-ScheduledTaskAction -Execute "powershell.exe" -Argument "-ExecutionPolicy Bypass -File C:\Scripts\traffic-alert.ps1"
$alertTrigger = New-ScheduledTaskTrigger -Once -At "09:00" -RepetitionInterval (New-TimeSpan -Hours 6) -RepetitionDuration ([TimeSpan]::MaxValue)

Register-ScheduledTask -TaskName "ClashTrafficAlert" -Action $alertAction -Trigger $alertTrigger -Settings $settings -Description "Clash 流量预警检查"

Write-Host "定时任务已创建" -ForegroundColor Green
```

### 智能流量控制

#### 按时间段自动切换

```powershell
# smart-traffic-control.ps1
# 智能流量控制脚本

$hour = (Get-Date).Hour

switch ($true) {
    # 工作时间（9:00-18:00）- 使用稳定节点
    ({ $hour -ge 9 -and $hour -lt 18 }) {
        Write-Host "工作时间模式 - 稳定优先"
        # 切换到稳定节点
        # Set-ClashNode -Group "工作" -Node "香港-稳定"
    }
    
    # 晚间（18:00-23:00）- 视频优先
    ({ $hour -ge 18 -and $hour -lt 23 }) {
        Write-Host "晚间娱乐模式 - 高带宽优先"
        # 切换到高带宽节点
        # Set-ClashNode -Group "视频" -Node "香港-高带宽"
    }
    
    # 深夜（23:00-9:00）- 节能模式
    ({ $hour -ge 23 -or $hour -lt 9 }) {
        Write-Host "深夜节能模式 - 降低频率"
        # 降低更新频率，节省资源
        # Set-ClashUpdateInterval -Minutes 3600
    }
}
```

---

## ❓ 常见问题与解决方案

### 问题一：流量消耗异常快

**可能原因：**
1. 系统/应用自动更新
2. 云盘同步大文件
3. 后台视频播放
4. 代理被滥用

**排查步骤：**
1. 检查各应用流量使用
2. 禁用自动更新
3. 设置流量告警
4. 检查是否有异常连接

### 问题二：流量突然耗尽

**可能原因：**
1. 家庭成员共享使用
2. 设备被蹭网
3. 订阅被分享

**解决方案：**
1. 检查设备列表
2. 更改 Wi-Fi 密码
3. 启用设备限速
4. 升级套餐或续费

### 问题三：流量统计不准确

**可能原因：**
1. 统计工具差异
2. 单位换算错误
3. 缓存未清理

**解决方案：**
1. 使用统一的数据源
2. 核实单位（GB vs GiB）
3. 定期重启设备清缓存

---

## 📥 相关资源

| 资源 | 链接 |
|------|------|
| ClashVIP 官网 | https://clashvip.net |
| 机场导航 | https://nav.clashvip.net |
| Clash 教程 | https://clashhub.net |
| 用户社区 | https://bbs.clashhub.net |
| 客户端下载 | https://clash-for-windows.net |
| PushPlus | https://www.pushplus.plus |

---

## ⚠️ 免责声明

1. 本仓库仅提供技术教程，不参与任何商业活动
2. 请遵守当地法律法规使用网络服务
3. 机场服务可能受地区政策影响
4. 购买前请仔细阅读服务商服务条款
5. 请勿用于任何违法用途

---

**最后更新：2026-08-15**

**更新内容：**
- 新增流量监控重要性深度分析
- 添加各平台流量统计完整指南
- 增加流量预警设置方案
- 完善流量节省技巧（应用/协议/系统级）
- 新增智能流量分配策略
- 增加流量偷跑检测方案
- 提供自动化管理完整脚本
