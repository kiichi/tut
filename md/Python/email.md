
##email

###sendmail
```python
 ```
```python
    """
    Usage:
    mail('somemailserver.com', 'me@example.com', 'someone@example.com', 'test', 'This is a test')
    """
    headers = "From: %s\r\nTo: %s\r\nSubject: %s\r\n\r\n" % (sender, to, subject)
    message = headers + text
    mailServer = smtplib.SMTP(serverURL)
    mailServer.sendmail(sender, to, message)
    mailServer.quit()
###Reference
http://www.eskimo.com/~jet/python/examples/mail/smtp1.html



