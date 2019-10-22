# Posh-HipChatLogs
## A PowerShell module to search and display HipChat log archives

This module accepts JSON data from HipChat log files in a number of formats. It can then search the files for specific strings and then display the result in a human readable format.

### Installation

Drop this directory into your PowerShell modules directory then restart PowerShell.

You can find a module directory with:
`$Env:PSModulePath`

### Usage

Extract a HipChat archive to disk.

You can then input that data in a number of ways:

##### Search a file for a string
`Find-HipChatLog -FileName "C:\archive\rooms\1111\history.json" -Patterns '*find this text*' -Before '2017-02' -AuditDirectory 'C:\audit'`

Searches FileName for the text "find this text" with wildcard matching. The date comparison will also exclude matches on or after February 1, 2017. The search hits and misses will be saved to disk inside AuditDirectory.

##### Search a directory of files for a string
`Find-HipChatLog -Directory "C:\archive\rooms\1111\" -Patterns '*find this text*' -After '2017-02' -AuditDirectory 'C:\audit' -NoConsoleLog`

Searches all files named history.json under Directory for the text "find this text" with wildcard matching. The date comparison will also exclude matches on or before February 1, 2017. The search hits and misses will be saved to disk inside AuditDirectory. The results will not be printed to the console - this can increase performance for large searches.

##### Search the files with another system and use the line number to extract context
`Find-HipChatLog -FileName "C:\archive\rooms\1111\history.json" -Line 3627 -Context 900 -LegacyFormat`

Searches FileName for line 3627 and extracts 900 context lines (default: 1000) before and after. It then prints the results to the console in the legacy text format.

##### Extract the JSON with another system then parse it for display
`Format-HipChatLogAsChat -FileName "C:\archive\users\1111\history.json" -Highlight '*find this text*'` -Extract

Reads FileName for the text "find this text" with wildcard matching. Displays the chat log as a table with messages containing "find this text" marked in the Hit column. The Extract switch excludes PrivateMessage conversations that do not include the search terms.

### Host

At the moment this module works best with PowerShell 5, but may be updated to support PowerShell Core (6+) in the future.