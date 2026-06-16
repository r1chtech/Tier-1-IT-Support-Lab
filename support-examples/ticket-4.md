### Ticket 4

```
Priority: Medium

Submitted by: Bob Marsh

Department: Sales

Subject: Cannot access fileserver01

I am unable to access fileserver01. I can successfully browse the internet and access external websites, but I cannot connect to the file server.
The issue started today; I was able to access fileserver01 without any problems yesterday.

```

**Resolution Approach**

Contact Bob using the office number on record to verify his identity and confirm the details of the issue.

Establish the scope of the problem by confirming:

- Whether Bob is the only user affected
- The exact error message displayed when attempting to access fileserver01
- Whether access is being attempted from the corporate network or remotely via VPN
- Whether the issue occurs when accessing the server by hostname, mapped drive, or UNC path

If access is denied or specific shares are unavailable, review the user's permissions and group memberships ([Ticket 3](./ticket-3.md)).

Verify that Bob has an active network connection and can access external websites, as reported in the ticket.

If Bob is connected remotely, confirm that the VPN session is active and connected successfully.

Once above is confirmed, perform DNS troubleshooting by `nslookup fileserver01`. If 'fileserver01' does not resolve to an IP address or returns an error such as "Non-existent domain", clear the local DNS cache using `ipconfig /flushdns`. Review the cached DNS entries using `ipconfig /displaydns`. Rerun `nslookup fileserver01` to verify successful name resolution.

If DNS resolution is successful, test network connectivity by pinging the server hostname or resolved IP address (`ping fileserver01/<IP>`).

If the request times out or the destination is unreachable, verify whether other users can access the server. If multiple users are affected, escalate to senior engineers.

If connectivity is successful but intermittent packet loss is observed, investigate potential network instability, firewall restrictions, or VPN-related issues. Escalate to the network team.

If network connectivity is confirmed, attempt to access the server directly using `\\fileserver01`

**Work Note Example**

- Contacted Bob Marsh and verified identity using office contact details.
- Confirmed issue affects only Bob; user unable to access `fileserver01` while internet connectivity is working.
- Confirmed user is connected from the corporate network/VPN.
- Verified DNS resolution for `fileserver01` using `nslookup`.
- Cleared local DNS cache using `ipconfig /flushdns` and retested.
- Tested network connectivity to `fileserver01` using `ping`.
- Attempted direct access via `\\fileserver01`.
- Based on results, escalated to the Infrastructure/Network team for further investigation.

User informed of next steps.

[Next ticket](./ticket-5.md)
