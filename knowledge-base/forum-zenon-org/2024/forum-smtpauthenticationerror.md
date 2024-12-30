Thread: forum-smtpauthenticationerror
0x3639 | 2024-03-27 15:20:04 UTC | #1

We are getting the following error in the logs.

```
Jobs::HandledExceptionWrapper: Wrapped Net::SMTPAuthenticationError: 535 Authentication failed
```

Looks like an SMTP authentication error w/ Mailgun.  There are > 18k failed attempts.  I'm traveling today and can look into this more closely tonight.

I probably need to  reset the SMTP password in mailgun and update the .yml file and rebuild discourse.  that will result in a 30 second outage.  I will just do it when ready hopefully later tonight.

-------------------------

0x3639 | 2023-03-10 00:42:30 UTC | #2

CPU is spiking to process the email backlog.  it's possible users will get a LOT of email when I fix this.

![Screenshot 2023-03-09 at 6.40.56 PM|690x277](upload://rMNUyi7YAtCtQbAUExGQoY8Qque.png)

-------------------------

0x3639 | 2023-03-10 00:52:03 UTC | #3

I just dumped the email backlog.  Taking a snapshot and will rebuild shortly.

-------------------------

0x3639 | 2023-03-10 11:08:26 UTC | #4

Looks like this rebuild fixed the SMTP issue.  Everyone should be receiving emails from the forum now.

-------------------------

