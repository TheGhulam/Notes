## Sending Emails (Simple Mail Transfer Protocol)
```python
import smtplib

conn = smtplib.SMTP('smtp.gmail.com', 587)
conn.ehlo()
conn.starttls()
conn.login(<username>, <password>)
conn.sendmail(<from_address>, <to_address>, 'Subject: So long…\n\nDear al, \nSo long, and thanks for all the fish.\n\n-AL')
conn.quit()
```
	
## Receiving e-mails (IMAP) Internet Message Access Protocol

```python
import imapclient, pyzmail

conn = imapclient.IMAPClient('imap.gmail.com', ssl=True)
conn.login(<username>, <password>)

conn.select_folder('INBOX', readonly=True)

UIDs = conn.search(['SINCE 20-Aug-2015'])

rawMessage = conn.fetch([UID], ['BODY[]', 'FLAGS'])

message = pyzmail.PyzMessage.factory(rawMessage[UID][b'BODY[]'])
message.get_subject()
message.get_address('from')
message.get_address('to')
message.get_address('bcc')

message.text_part # If none, email is html
message.html_part # If True, email is html

message.text_part.get_payload().decode('UTF-8')

conn.logout()
```
	

![](smtp.png)

![](smtp1.png)

