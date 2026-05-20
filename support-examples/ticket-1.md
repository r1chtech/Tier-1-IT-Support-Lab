### Ticket 1

```
Priority: Low
Submitted by: Alice Carter
Department: Sales
Subject: Can't log in — first day

Hi, IT. It's Alice, I just started today. I've sat down at my PC and I'm not sure how to log in. The screen looks different to what I'm used to at home. Can someone help?
```

**Resolution Approach**

I would explain to Alice that she will need a username and password to log in. I she does not have a username and password, then I would need to add her by creating a new user. If she has credentials, I would then ask her which screen she is currently on. Once I establish her current location, for example the lock screen, I would guide her through the process step by step.

First, I would ask her to press `Ctrl + Alt + Delete` to access the login screen. Then, I would instruct her to select `Other User`.

I would provide her with the username: `RICHTECH\a.carter` and the temporary password: `changeme`

I would explain that, because this is her first login, she will be prompted to create a new password. I would reassure her that this is normal.

After she sets her new password, she can log in again using the new credentials, which will take her to the desktop/home screen.

I would also explain that, since this is her first login, Windows may take a few minutes to complete the initial setup process before the desktop is fully available.

It will also be a great opportunity to check that shared folder works. I would instruct Alice to open the file explorer. I would ask her to type `\\RICHTECH\Sales` in the address bar (where the file path display). If this succeed without any permission errors then great if not, then I would need to look into permissions and groups.

**Closing Ticket**

**Work Note Example**

- Received call from Alice Carter, new starter in Sales i.e. unable to log in on first day
- Verified account exists in Active Directory i.e. a.carter confirmed active
- Spoke to user to determine current screen i.e. confirmed on lock screen
- Assisted user in navigating to login screen and selecting Other User
- Instructed user to enter domain credentials: RICHTECH\a.carter
- User prompted to change temporary password i.e. explained this is expected behaviour for new accounts
- Assisted user through password change process
- User successfully logged into domain i.e. desktop loaded
- Verified Sales shared drive accessible via \RICHTECH-DC01\Sales
- Confirmed Finance and IT shares correctly denied

No further issues reported. Resolved.

> Simulate this using the lab.
