# About
GraphRunner is a post-exploitation toolset for interacting with the Microsoft Graph API. It provides various tools for performing reconnaissance, persistence, and pillaging of data from a Microsoft Entra ID (Azure AD) account.

It consists of three separate parts:

- A PowerShell script where the majority of modules are located
- An HTML GUI that can leverage an access token to navigate and pillage a user's account
- A simple PHP redirector for harvesting authentication codes during an OAuth flow
## Links
[Github](https://github.com/dafthack/GraphRunner/)
https://github.com/dafthack/GraphRunner/wiki/Authentication
https://www.blackhillsinfosec.com/introducing-graphrunner/
# Usage
```powershell
cd C:\Toolz\Graphrunner-main
Import-Module .\GraphRunner.ps1
Get-GraphTokens # login on with URL / Code
Invoke-GraphRunner -Tokens $tokens
Invoke-SearchSharePointAndOneDrive -tokens $Tokens
```
