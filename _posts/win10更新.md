2021-05-21

操作之前备份注册表，

HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer
在这里新建一个32位DWORD值NoWindowsUpdate，把数值改为1。如果想重新开启可删除此键值。

---

删除了C:\Windows\UpdateAssistant路径下的window10update.exe文件

---

首先，在开始菜单右边的对话框中输入“计划任务”，然后在左边的“任务计划程序库”中点开Microsoft。在下边的WINDOWS选项中找到“Update Orchestrater”.在右边的窗口处找到“'Update Assistant”。双击后在触发器选项中双击第一个标签后将最下方的“已启用”选项框勾掉。确认后将所有的标签都重复次操作。完成后按确认回到任务计划程序界面。同样在右边找到“Update Assistant CalendarRun”选项卡后双击打开。点击触发器选项重复上一步操作即可

还关了windowupdate里的