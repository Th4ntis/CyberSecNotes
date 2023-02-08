# Powershell Obfuscation

Obfuscation essentially means to make obscure, or to hide. We can use it for concealment of written code purposefully. It is mainly done for the purposes of security by making it obscure to hide implicit values or conceal the logic used. One can obfuscate code with the help of language-specific deobfuscators that convert into meaningful code. This will cover various ways we can hide malicious powershell commands. A helpful resource is the [Offensive Security Powershell Security](https://www.offensive-security.com/offsec/powershell-obfuscation/) page.

## AMSI

The Windows Antimalware Scan Interface (AMSI) is essentially an API that allows applications, such as anti-virus, to scan various types of content in memory before it’s executed. Think of AMSI as an additional security check for your system. Keep in mind that AMSI is not limited to just anti-virus as it’s also integrated into these components of Windows 10:

* User Account Control, or UAC (elevation of EXE, COM, MSI, or ActiveX installation)
* PowerShell (scripts, interactive use, and dynamic code evaluation)
* Windows Script Host (wscript.exe and cscript.exe)
* JavaScript and VBScript
* Office VBA macros

The challenge that this will present to us is that if we use common payloads without making any modifications, or even obfuscation tools that are outdated, then it will more than likely get flagged. As we mentioned before, some of the techniques include the use of layering logic to hide your payloads in plain sight. Here are some of those techniques to give you an idea on how they’re generated and how the final launcher appears in your payloads.

## Base64 Encoded Commands

PowerShell supports the ability to execute base64 encoded commands right from the command line. It also allows you use partial parameter names so long as it’s unambiguous, which is a common practice with this particular launcher. This is arguably the most popular approach and is also one of the easiest to discover when reviewing the logs.

Here is a break down of these parameters and what they do:

* \-NoP – (-NoProfile) – Does not load the Windows PowerShell profile.)
* \-NonI – (-NonInteractive) – Does not present an interactive prompt to the user.
* \-W Hidden (-WindowStyle) – Sets the window style to Normal, Minimized, Maximized or Hidden.
* \-Exec Bypass (-ExecutionPolicy) – Sets the default execution policy for the current session and saves it in the $env:PSExecutionPolicyPreference environment variable. This parameter does not change the Windows PowerShell execution policy that is set in the registry.
* \-Enc (-EncodedCommand) – Accepts a base-64-encoded string version of a command. Use this parameter to submit commands to Windows PowerShell that require complex quotation marks or curly braces.

`powershell.exe -NoP -NonI -W Hidden -Exec Bypass -Enc 'Vy5yLmkudC5lLi0uTy51LnQucC51LnQuIC4iLkguZS5sLmwuby4gLlcuby5yLmwuZC4iLg=='`

### Base64 Expressions

This method enables you to execute base64 encoded strings within your script itself.

`Invoke-Expression ([System.Text.Encoding]::Unicode.GetString(([convert]::FromBase64String('Vy5yLmkudC5lLi0uTy51LnQucC51LnQuIC4iLkguZS5sLmwuby4gLlcuby5yLmwuZC4iLg=='))))`

## Compression

Compression obfuscation can aid in both evading AMSI (sometimes) and makes it a little tricky to deconstruct. This will take a given payload and compress it into a gzip object then it’ll get encoded so it can be stored within the payload. The sneakiness is that you will need to know how to properly decode it or else your payload will be look be unintelligible. Keep in mind that not everyone is comfortable with PowerShell so it may not be that straight forward to extract the intended payload.

## Payload Reversing

You are able to reverse virtually anything that can be split into a character array. You’ll see this more often with base64 encoded strings, however, you can also store reversed commands within a payload as well.

## Helpful Tools and Resouces

[Offensive Security Powershell Security](https://www.offensive-security.com/offsec/powershell-obfuscation/)

[Invoke-Obfuscation Github](https://github.com/danielbohannon/Invoke-Obfuscation)

[Invoke-PSObfuscation Github](https://github.com/gh0x0st/Invoke-PSObfuscation)

## Defense

COMING SOON
