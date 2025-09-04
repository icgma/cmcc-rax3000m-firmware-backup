# CMCC RAX3000M 路由器固件备份

> 📡 中国移动 RAX3000M (MT7981) 路由器完整固件备份集合

## 项目概述

本项目包含了中国移动 RAX3000M 路由器（基于 MediaTek MT7981 芯片）的完整固件备份文件。这些备份文件用于路由器的恢复、刷机或维护目的。

### 技术规格
- **芯片型号**: MediaTek MT7981
- **设备型号**: CMCC RAX3000M
- **固件类型**: ImmortalWrt OpenWrt
- **备份日期**: 2024年1月2日

## 文件结构

```
RAX3000M/
├── README.md                           # 本文档
├── .gitignore                          # Git忽略文件配置
├── immortalwrt-mediatek-mt7981-cmcc_rax3000m-squashfs-sysupgrade.bin  # [46MB] 系统升级固件
├── mt7981_cmcc_rax3000m-fip-fixed-parts.bin              # [1MB] FIP固定分区
├── mt798x-uboot-202307-fip.7z                            # [1MB] U-Boot FIP压缩包
├── mtd1_BL2.bin                                          # [1MB] Bootloader 2
├── mtd2_u-boot-env.bin                                   # [1MB] U-Boot环境变量
├── mtd3_Factory.bin                                      # [2MB] 工厂分区
├── mtd4_mtd4_FIP.bin                                     # [2MB] FIP分区
├── mtd5_ubi.bin                                          # [61MB] UBI根文件系统
├── mtd6_plugins.bin                                      # [37MB] 插件分区
├── mtd7_fwk.bin                                          # [8MB] 固件分区1
├── mtd8_fwk2.bin                                         # [8MB] 固件分区2
└── spi-all.gz                                            # [50MB] SPI闪存完整备份
```

### 文件说明

| 文件名 | 大小 | 描述 | 用途 |
|--------|------|------|------|
| `immortalwrt-*.bin` | 46MB | 系统升级固件 | 用于系统升级或恢复 |
| `spi-all.gz` | 50MB | SPI闪存完整备份 | 完整的闪存镜像备份 |
| `mtd5_ubi.bin` | 61MB | UBI根文件系统 | 包含系统根分区 |
| `mtd6_plugins.bin` | 37MB | 插件分区 | 存储系统插件和应用 |
| `mt798x-uboot-*.7z` | 1MB | U-Boot压缩包 | 引导加载程序 |
| `mtd1_BL2.bin` | 1MB | 二级引导加载程序 | 启动第一阶段 |
| `mtd2_u-boot-env.bin` | 1MB | U-Boot环境变量 | 存储启动配置 |
| `mtd3_Factory.bin` | 2MB | 工厂分区 | 原厂设置和信息 |
| `mtd4_*.bin` | 2MB | FIP分区 | 固件镜像协议分区 |
| `mtd7_fwk.bin` | 8MB | 固件分区1 | 系统固件部分1 |
| `mtd8_fwk2.bin` | 8MB | 固件分区2 | 系统固件部分2 |

## 使用指南

⚠️ **警告**: 刷机操作有风险，可能导致设备变砖。请确保您了解操作步骤，并在操作前备份重要数据。

### 环境要求
- 支持 MT7981 芯片的路由器设备
- U-Boot 访问权限（通过 TTL 串口或 Web 界面）
- 足够的设备存储空间

### 基本操作步骤

1. **准备工作**
   - 确保路由器电量充足
   - 准备 TTL 串口工具（可选，用于故障恢复）
   - 下载所需的固件文件

2. **系统升级**
   ```bash
   # 通过 U-Boot 命令行
   tftpboot 0x46000000 immortalwrt-mediatek-mt7981-cmcc_rax3000m-squashfs-sysupgrade.bin
   nand erase.part firmware
   nand write 0x46000000 firmware
   ```

3. **完整恢复**
   ```bash
   # 恢复单个分区
   nand write.e 0x46000000 mtd1 0x100000
   nand write.e 0x46000000 mtd2 0x80000
   # ... 其他分区
   ```

### 常见问题

**Q: 刷机后设备无法启动怎么办？**
A: 使用 TTL 串口连接设备，进入 U-Boot 模式重新刷入正确的固件。

**Q: 如何确认设备型号？**
A: 检查设备底部的标签，或通过原厂固件的管理界面查看。

**Q: 是否需要解锁 Bootloader？**
A: 部分设备可能需要先解锁 Bootloader 才能刷入第三方固件。

## 注意事项

- 本固件仅适用于 CMCC RAX3000M 型号路由器
- 请勿在其他型号设备上使用，可能导致设备损坏
- 大型二进制文件（.bin）未包含在 Git 仓库中，需要单独下载
- 使用前请确认固件版本与您的设备兼容

## 版本历史

- **v1.0** (2024-01-02)
  - 初始备份版本
  - 包含完整的分区镜像
  - 基于 ImmortalWrt 固件

## 许可证

本项目仅用于设备维护和恢复目的。固件文件的版权属于各自的制造商。

## 免责声明

使用者自行承担使用这些固件文件的风险。作者不对任何可能的数据丢失或设备损坏负责。

## 联系方式

如有问题或建议，请通过 GitHub Issues 提交。

---

*最后更新: 2024年1月2日*