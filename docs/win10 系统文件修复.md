---
layout: default
title: win10 系统文件修复
parent: 日常问题记录
nav_order: 4
---


系统文件检查器是 Windows 中的一个实用工具，用于检查计算机上文件的问题。 若要运行它，请按照下列步骤进行操作：

1. 在任务栏上的搜索框中，键入命令提示符，然后右键单击或按住命令提示符 (桌面应用) 结果列表中。 选择“以管理员身份运行”，然后选择“是”。

2. 键入 `DISM.exe /Online /Cleanup-image /Restorehealth`（注意每个 "/" 前的空格），然后按“Enter”键。 (注意： 此步骤可能需要几分钟才能开始和完成。)
![image.png](https://file.mbad.top/file/202304171610205.png)

3. 看到显示“操作成功完成”的消息后，键入 sfc /scannow (记下“sfc”和“/”) 之间的空格，然后按 Enter。

4. 看到“验证 100% 完成”的消息后，键入 “退出”，然后按 Enter。
