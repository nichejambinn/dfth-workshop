# Walkthrough
1. Signin to Elastic/Kibana `http://localhost:5601`
	1. We'll refer to the GUI as Elastic from now on.
2. Use the left-hand hamburger menu to navigate to Analytics > Discover
## Process Creation
1. Open up Paint
2. Put the query `event.code:1 AND process.name:mspaint.exe` into the search bar.
	1. The search should default to the last 15min. Results may take a second - you should expect to see one document/log corresponding to the Sysmon process creation event for Paint.
3. In the list of available fields on the left, find `process.command_line`, `process.parent.command_line` and `message`. Click the '+' button that appears when you hover on the right side of the field entry to select to display them in the table view.
	1. (You can hover over the field name to find the 'X' button to remove them from the table later on.)
## User Logon
1. Sign out of the `dfthrunter` account without shutting down. Don't worry, Elastic will stay running,
2. Sign back into Windows.
3. Reopen Elastic and sign in.
4. Now search `event.code:4624 AND user.name:dfthrunter`
5. Select the `winlog.event_data.LogonType` and `message` fields for display.
	1. To the left-hand side of each log there's a double-sided arrow to expand and view the full contents of the record.
	2. Look at the contents of `message`. That's the original event log.
## Dump LSASS
1. Run `Invoke-AtomicTest T1003.001 -TestNumbers 2`
	1. Remember you can use the `-ShowDetails` flag to see what actions an atomic will perform.
2. Microsoft Defender will generate an alert notification.
3. Go into Windows Security > Virus & threat protection > Protection history.
	1. You should see `Detected: Trojan:Win32/RundllLolBin.AF` and the PowerShell command line Atomic Red Team used.
4. Back in Virus & threat protection, go to Manage settings and disable Real-time protection.
5. Run the atomic test again.
6. Search `event.code:1 AND process.name:rundll32.exe`. Select `process.command_line`.
