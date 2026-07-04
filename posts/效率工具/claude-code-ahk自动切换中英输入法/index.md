# Claude Code AHK自动切换中英输入法

功能：输入/或@，自动切换英文输入法；Enter接受或Esc清空，自动切换中文输入法。
<!--more-->

前提：

* 使用WindowsTerminal，其他请修改`ahk_exe *.exe`
* 中文和英语(美国)两个语言包和各自键盘

```AutoHotkey
#HotIf WinActive("ahk_exe WindowsTerminal.exe")
; 当按下 / 或 @ 时：保留符号并切换英文
~$/::
~$NumpadDiv::
~$+2:: ; Shift + 2 就是 @
{
    Sleep(50) ; 延迟 50ms 确保按键已输入，然后切换为英文
    SetInputLanguage(0x0409) ; en-US
}
; 当输入完成按下回车，或者取消按下 Esc 时：切换回中文
~$Enter::
~$Esc::
{
    Sleep(50)
    SetInputLanguage(0x0804) ; zh-CN
}
#HotIf

; ========== 核心函数：通过系统底层消息切换输入法 ==========
SetInputLanguage(langID) {
    targetHWND := WinExist("A")
    if (targetHWND) {
        ; WM_INPUTLANGCHANGEREQUEST = 0x0050
        PostMessage(0x0050, 0, langID, targetHWND)
    }
}
```

---

> 作者: [Jason](https://github.com/actforjason)  
> URL: https://actforjason.github.io/posts/%E6%95%88%E7%8E%87%E5%B7%A5%E5%85%B7/claude-code-ahk%E8%87%AA%E5%8A%A8%E5%88%87%E6%8D%A2%E4%B8%AD%E8%8B%B1%E8%BE%93%E5%85%A5%E6%B3%95/  

