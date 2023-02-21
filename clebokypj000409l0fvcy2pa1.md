# How  I  automated  'Monitoring Job'

My friend is a Software Engineer at a recognized MNC, working as Support Engineer on a project, I have been watching my friend doing a monitoring job specifically in that project from last 5 month.

His job is to check every mail, their criticality, if it is high/medium/low then he has to forward it to the responsible team to fix it as soon as possible, also in every mail he has to check some more parameters like from which team or client this error/alert is coming.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676828249457/21560c88-0a34-4f2d-95d5-40d1458ba5cf.png align="center")

I observed that he looks at the subject of a mail for criticality, the body of the mail to recognize the team/client, then he uses it to forward to response teams.

Also, he and his team have to look at emails every time so that they do not miss any alerts/errors.

### Thought

My thought after watching his job was like, can't we automate this? means why there should be a human to read emails and forward them to some specific teams as per the nature of alerts/errors.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676828292262/381a29cd-59da-4654-95be-e0023eafb667.png align="center")

This work can be done by some lines of code if we have a function to read unseen/new emails, its subject and body to get more details so that they can be forwarded to responsible teams.

### Approach

As they are using their official outlook mail for work, whose API can't be available easily, I tried to demonstrate my idea through Gmail as it is easier to use.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1676828380251/f5be819e-e5ed-440b-a885-d859632aa42d.png align="center")

I tried with 4-5 Gmail account for which I need to make some changes in the security of every Gmail like a less secure app option is made on.

### Code

Below send\_mail() method is made to send a mail with a message and subject.

```python
def send_email(to, subject, email_message):
    server = smtplib.SMTP_SSL('smtp.gmail.com', 465)
    server.ehlo()
    # server.starttls()
    server.ehlo()
    # login to your mail in which alert mails are coming
    server.login('xxxxxxxxxxx@gmail.com', 'xxxxxxxxxxxxxx')

    # print('hey mail going to be sent')
    msg = MIMEMultipart()
    msg['From'] = "xxxxxxxxxxx@gmail.com"
    msg['To'] = to
    msg['Subject'] = subject
    msg.attach(MIMEText(email_message, "plain"))
    server.sendmail(
        'xxxxxxxxxxx@gmail.com',
        to, msg.as_string()
    )
    # print('hey mail sent')
    server.quit()
```

The below code loop through all emails and do operation like checking the subject and body, then based on cases it forwards the mail.

```python
# Connect to the Gmail server using IMAP
mail = imaplib.IMAP4_SSL("imap.gmail.com")
mail.login("insane@gmail.com", "xxxxxxxxxxxxxx")
mail.select("inbox")

# Search for new emails
status, email_ids = mail.search(None, "UNSEEN")
email_ids = email_ids[0].split()


# Loop through all emails
for email_id in email_ids:
    # Get the email
    status, email_data = mail.fetch(email_id, "(RFC822)")
    email_message = email.message_from_bytes(email_data[0][1])
    
    # Connect to the Gmail server
    mail = imaplib.IMAP4_SSL("imap.gmail.com")
    mail.login("xxxxxxx@gmail.com", "xxxxxxxxx")
    mail.select("inbox")
    
    # Search for new emails
    status, email_ids = mail.search(None, "UNSEEN")
    email_ids = email_ids[0].split()
    # Get the subject of the email
    subject = email_message["subject"]
    # Get the body of the email
    body = email_message.get_payload(decode=True).decode()
    
    # Check if the subject contains "critical", "major", or "minor"
    if "critical" in subject.lower():
         # Check if the body contains "ABC", "BCC", or "DCC"
         if "ABC" in body:
                # Forward the email to the ABC team email
           send_email("aim_team@example.com", subject, email_message.as_string())
         elif "BCC" in body:
                # Forward the email to the BCC team email
           send_email("nbm_team@example.com", subject, email_message.as_string())
         elif "DCC" in body:
                # Forward the email to the DCC team email
           send_email("tcc_team@example.com", subject, email_message.as_string())
         elif "ECC" in body:
                # Forward the email to the ECC team email
           send_email("ecc_team@example.com", subject, email_message.as_string())
    elif "major" in subject.lower():
         # Check if the body contains "ABC", "BCC", or "DCC"
         if "ABC" in body:
                # Forward the email to the ABC team email
           send_email("amm_team@example.com", subject, email_message.as_string())
         elif "BCC" in body:
                # Forward the email to the BCC team email
           send_email("itm_team@example.com", subject, email_message.as_string())
         elif "DCC" in body:
                # Forward the email to the DCC team email
           send_email("ahc_team@example.com", subject, email_message.as_string())
         elif "ECC" in body:
                # Forward the email to the ECC team email
           send_email("ajc_team@example.com", subject, email_message.as_string())
    elif "minor" in subject.lower():
         # Check if the body contains "ABC", "BCC", or "DCC"
         if "ABC" in body:
                # Forward the email to the ABCteam email
           send_email("anm_team@example.com", subject, email_message.as_string())
         elif "BCC" in body:
                # Forward the email to the BCC team email
           send_email("ikm_team@example.com", subject, email_message.as_string())
         elif "DCC" in body:
                # Forward the email to the DCC team email
           send_email("agc_team@example.com", subject, email_message.as_string())
         elif "ECC" in body:
                # Forward the email to the ECC team email
           send_email("ecc_team@example.com", subject, email_message.as_string())
```

### Conclusion

I tried the above automation by observing only one kind of monitoring job, this is a basic example of what an automated monitoring job of the above-explained task looks like, there will be some change that needs to be made above to meet the exact automation.