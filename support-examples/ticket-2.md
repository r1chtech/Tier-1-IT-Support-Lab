### Ticket 2

```
Priority: Medium
Submitted by: David Okafor
Department: Finance
Subject: Locked out of my account

Hi IT, it's David from Finance. I've been trying to log in this morning but I keep getting a message saying my account is locked. I'm sure I'm using the right password but it just won't let me in. I need to get in urgently, I have a finance report due this morning.
```

**Resolution Approach**

Firstly, due to the nature of this ticket, it would be a good idea to cotact David to make sure that he is the on who has created this ticket for security reasons. Ask for the exact error. When it is confirmed that indeed David's account is locked, check active directory users and find David. Click on the account tab and check unlock. Then right click on David and reset password.

**Work Note Example**

- Ticket received from David in the Finance department reporting that his account was locked out.
- Contacted David by phone to verify identity and confirm ticket authenticity.
- Confirmed the error message: “The referenced account is currently locked out and may not be logged on to.”
- Located David’s account in Active Directory Users and Computers.
- Unlocked the account under the Account tab.
- Reset the user password in accordance with security policy.
- Provided David with a temporary password and instructed him to change it after login.
- Confirmed with David that he was able to log in successfully.

No further issues reported. Resolved.

> Simulate this using the lab. Ensure you have a group policy with an account lockout threshold. [Check here](../gpo.md).
> From a client workstation, select a user account.
> Attempt to log in using an incorrect password 5 times.
> Verify that the account becomes locked.

[Next ticket](./ticket-3.md)
