### Ticket 5

```

Priority: Medium

Submitted by: Sarah Jensen

Department: Finance

Subject: Unable to Print to Finance Office Printer

Hi IT,

I am unable to print to the Finance department printer `FIN-PRN-02`.

When I send documents to the printer, the print jobs remain in the queue and eventually display an error stating "Printer is offline."

I have restarted my computer and confirmed that I am connected to the corporate network, but the issue persists.

My colleagues are able to print successfully, so the issue appears to be affecting only my workstation.

```

**Resolution Approach**

Contact Sarah and confirm the exact error message displayed and whether the issue is isolated to her workstation.

Establish the scope of the issue by confirming:

- Colleagues can print successfully to FIN-PRN-02
- Whether Sarah can print to other printers
- Whether the issue occurs from a specific application or all applications
- Whether the problem started after any recent changes, such as a password reset, workstation replacement, or software update

Verify that Sarah is connected to the corporate network or VPN, if working remotely.

Navigate to Control Panel > Devices and Printers and confirm that FIN-PRN-02 is visible and set as the default printer, if applicable.

Check the printer status and ensure it is not showing as Offline, Paused, or Disconnected.

Open the print queue and clear any stuck or failed print jobs.

Restart the Print Spooler service on the workstation and attempt to print again.

- Press `Win+R` and type `services.mcs`
- Once service open, look for print spooler. Double click and choose stop.
- Go to C: > Windows > System32 > spool > PRINTERS and delete any printer queued files.
- Go back to the printer spool service and start it.

If the printer remains unavailable:

- Remove and re-add the printer
- Verify that the correct printer driver is installed
- Check for available driver updates
- Reinstall the printer using the latest approved driver, if necessary

Confirm network connectivity to the print server or printer by testing access to the printer's hostname or IP address.

**Work Note Example**

- Contacted Sarah Jensen and verified issue details.
- Confirmed `FIN-PRN-02` displays as **Offline** and issue is isolated to Sarah's workstation; colleagues can print successfully.
- Verified user can access the corporate network and print to other devices.
- Cleared stuck print jobs and restarted the Print Spooler service.
- Removed and re-added `FIN-PRN-02`; verified correct printer driver is installed.
- Sent Windows test page and confirmed successful printing.
- User verified documents now print normally.

No further issues reported. Resolved.
