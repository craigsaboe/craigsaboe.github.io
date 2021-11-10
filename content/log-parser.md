Title: Log Parser Studio + Log Parser 2.2
Date: 2021-08-30 10:48:00
Category: General

* Log Parser is a CLI tool for parsing text-based data that can handle a wide range of sources
* Log Parser Studio (LPS) is a GUI for that CLI because it sucks trying to remember long CLI arg strings like: <code>LogParser "SELECT TimeGenerated, SourceName, EventCategoryName, Message INTO report.txt FROM Security WHERE EventID = 528 AND SID LIKE '%TESTUSER%'" -resolveSIDs:ON</code>

Download:
* LP 2.2: https://www.microsoft.com/en-us/download/details.aspx?id=24659
* LPS V2.D2: https://techcommunity.microsoft.com/gxcuf89792/attachments/gxcuf89792/Exchange/16744/1/LPSV2.D2.zip

Notes:
* Web server log parsing:
    * There are a few different log types for web server logs, especially IIS. Which one to use for standard IIS?


Docs:
* LP 2.2 Docs: C:\Program Files (x86)\Log Parser 2.2\LogParser.chm > esp. under "Reference"

Links:
* "Using LogParser 2.2 to Parse IIS Logs and Other Logs" - http://aspalliance.com/articleViewer.aspx?aId=1714&pId=-1
* "How Log Parser 2.2 Works" - https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-xp/bb878032(v=technet.10)?redirectedfrom=MSDN
* "Log Parser 2.2 and ASP.NET" - https://support.microsoft.com/en-us/topic/log-parser-2-2-and-asp-net-37531636-1cf5-dc52-f12a-6a9252155631
* "Introducing: Log Parser Studio" - https://techcommunity.microsoft.com/t5/exchange-team-blog/introducing-log-parser-studio/ba-p/601131

Ex:
* SELECT TOP 10 * FROM '[LOGFILEPATH]'
* SELECT * FROM '[LOGFILEPATH]' WHERE [AllXml] like '%2600:387:3:803::28%'