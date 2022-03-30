# Retrieve Windows Product Key from Registry

If your product key isn't embedded in the firmware or you're missing your COA sticker, you're not out of luck as long as you haven't formatted your computer. You can still recover the key because Windows stores it in the registry. Here is how:

1. Open a new Notepad window

2. Copy and paste the following text into the window

```
Set WshShell = CreateObject("WScript.Shell")
MsgBox ConvertToKey(WshShell.RegRead("HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\DigitalProductId"))

Function ConvertToKey(Key)
Const KeyOffset = 52
i = 28
Chars = "BCDFGHJKMPQRTVWXY2346789"
Do
Cur = 0
x = 14
Do
Cur = Cur * 256
Cur = Key(x + KeyOffset) + Cur
Key(x + KeyOffset) = (Cur \ 24) And 255
Cur = Cur Mod 24
x = x -1
Loop While x >= 0
i = i -1
KeyOutput = Mid(Chars, Cur + 1, 1) & KeyOutput
If (((29 - i) Mod 6) = 0) And (i <> -1) Then
i = i -1
KeyOutput = "-" & KeyOutput
End If
Loop While i >= 0
ConvertToKey = KeyOutput
End Function
```

3. Click File > Save As and save the file to your desktop as productkey.vbs. It's important to include the .vbs extension because this is a Windows Scripting Host file.

4. Close Notepad and double-click the file. Wait a few seconds, and then you will be presented with a popup displaying your product key.
