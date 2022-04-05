# MinorVersion
; Dec, Int, Number Constants Global Const $NUMBER_AUTO = 0 Global Const $NUMBER_32BIT = 1 Global Const $NUMBER_64BIT = 2 Global Const $NUMBER_DOUBLE = 3  Global Const $tagOSVERSIONINFO = 'struct;dword OSVersionInfoSize;dword MajorVersion;dword MinorVersion;dword BuildNumber;dword PlatformId;wchar CSDVersion[128];endstruct'  ConsoleWrite('Windows version: ' &amp; _WinAPI_GetVersion() &amp; @CRLF)  Func _WinAPI_GetVersion()         Local $tOSVI = DllStructCreate($tagOSVERSIONINFO)         DllStructSetData($tOSVI, 1, DllStructGetSize($tOSVI))          Local $aCall = DllCall('kernel32.dll', 'bool', 'GetVersionExW', 'struct*', $tOSVI)         If @error Or Not $aCall[0] Then Return SetError(@error, @extended, 0)          MsgBox(0, "OSVERSIONINFO", "MajorVersion = " &amp; DllStructGetData($tOSVI, "MajorVersion") &amp; @CRLF &amp; _                         "MinorVersion = " &amp; DllStructGetData($tOSVI, "MinorVersion") &amp; @CRLF &amp; _                         "BuildNumber = " &amp; DllStructGetData($tOSVI, "BuildNumber"))          Return Number(DllStructGetData($tOSVI, "MajorVersion") &amp; "." &amp; DllStructGetData($tOSVI, "MinorVersion"), $NUMBER_DOUBLE) EndFunc   ;==>_WinAPI_GetVersion
