# 任意数据备份

## 0x01 漏洞描述

Android属性`allowBackup`安全风险源于`adb backup`允许任何一个能够打开USB 调试开关的人，从Android手机中复制应用数据到外设，一旦应用数据被备份之后，所有应用数据都可被用户读取，`adb restore`允许用户指定一个恢复的数据来源（即备份的应用数据）来恢复应用程序数据的创建。

因此，当一个应用数据被备份之后，用户即可在其他Android手机或模拟器上安装同一个应用，以及通过恢复该备份的应用数据到该设备上，在该设备上打开该应用即可恢复到被备份的应用程序的状态。

## 0x02 漏洞危害

当allowBackup标志为true时，用户即可通过adb backup和adb restore来进行对应用数据的备份和恢复。

尤其是通讯录应用，一旦应用程序支持备份和恢复功能，攻击者即可通过adb backup和adb restore进行恢复新安装的同一个应用来查看聊天记录等信息；对于支付金融类应用，攻击者可通过此来进行恶意支付、盗取存款等；

## 0x03 修复意见

* 设置`android:allowBackup`值为false。