# Advanced Guide

This advanced guide includes tips and tricks, and also solutions to common issues you may face when using FormSG. This section is updated regularly, so feel free to check back once in a while.

## When can I build and fill forms on the Intranet?

The primary goal of FormSG is to replace Internet citizen-facing paper forms. However, by end 2019 we will move onto the Intranet where you can create and fill forms there. We also have future plans in 2020 to extend FormSG to handle client relationship management (CRM) and case management (CMS).

## Where is the signature field?

There are a few variants of electronic signatures available on FormSG, all of which, according to the Electronic Transactions Act, are not legally weaker than a wet ink signature. Agencies such as IRAS and MOM have used the following for electronic signatures: a) an NRIC field, b) an attachment of a wet ink signature and c) SingPass Login. 

## How do I route responses to different emails based on form option selected? 

This might apply for an enquiry form. If user chooses "Complaint" response should route to Complaints Department, but if user chooses "IT" response should route to IT Department. There's no such feature on FormSG, but you can set mail forwarding rules on your email. For example, one such rule can detect "Complaint" in the form response email, and forward this to the Complaints Department automatically.

## My form is really long. Why can't users save draft?

We took out Save Draft because there is no good place to save such data - our servers do not store data, and saving data on the local computer might leak this out to unintended recipients if form is filled from a library computer. Furthermore, it's more important to advise the user how long it takes to fill in the form, so they have sufficient time to submit in one sitting, which is a better user experience than saving draft and coming back repeatedly. In the future with end-to-end encrypted Storage mode, we might consider re-enabling Save Draft function.

## How do I increase attachment size limit? And what if there are many attachments for my form?

The current size limit is 7 MB for the entire form. We auto-compress images to 1024x768 resolution, which is typically less than 1 MB. This is a hard limit because the email service we use has a fixed 10 MB outgoing size, and we buffer 3 MB for email fields and metadata. In the future with Storage mode, we are considering raising this size limit to 20 MB. 

Because the smallest unit you can attach per attachment field is 1 MB, you can have a max of 7 attachments on your form. If your user has to submit more than 7 documents, you may create just one attachment field of 7 MB, and advise your user to zip documents up and submit as one attachment.

## I am leaving the organisation or switching over to a new email. How do I transfer ownership of my forms?

Note that you might not need to transfer ownership of your form. You may simply add your colleague as a collaborator. Collaborators have the same rights as form creators, except they cannot delete the form.

![FormSG FAQ Add Collaborators](https://s3-ap-southeast-1.amazonaws.com/misc.form.gov.sg/faq-collaborator.png "FormSG FAQ Add Collaborators")

If you have already lost access to your old email and can no longer edit your form, you may file a [Support Form](https://go.gov.sg/formsg-support) request to transfer ownership to another email.

## My forms are particularly sensitive and I do not want other public officers to see them on the Examples tab.

Note that only forms that are active, and have at least 10 responses will be searchable on the Examples tab. And that the Examples tab is only viewable by authenticated public officers, not the general public. Furthermore, only your form fields are viewable, not your form data.

But if there is still a need to unlist your form from the Examples tab because the form fields alone are already sensitive to be viewed by fellow public officers, then you may submit our [Support Form](https://go.gov.sg/formsg-support), and attach an email approval from your MIC stating justifications for unlisting it from the Examples tab.

## How should I name my form? Symbols like "(" are not allowed.

Unfortunately, symbols such as brackets "(" are not allowed on form titles yet. You may substitute this with dashes, e.g. License Application - For Companies.

## Is there an address field? How can I auto-populate one?

You may create a Postal code field with Short Text that validates 6 characters, together with a few more fields for block and unit numbers. If verified addresses are needed, you may enable SingPass on your form, and drag in a Registered Address MyInfo field.

## How long does the OTP take to send? For how long do I remain logged in for?

The OTP is sent immediately, but might take a while to arrive in your government email due to the potentially multiple firewalls the email has to go through. OTPs expire in 15 minutes, after which you have to resend another one. After logging in, you will remain logged in for 24 hours. This means you need not have both Intranet and Internet devices at all times; you can log in to your Internet device before you leave your office, and for 24 hours be able to create forms from one Internet device.

## How do I restrict access to fill in my form to selected users?

The unguessable form link acts as a password. You can circulate the form link to only users that you intend to gather responses from. As long as you don't add the form link to public channels such as on your agency's Internet website, the form link will not be indexed by search engines. If the form link ends up widely circulated with non-authorised users submitting the form, you may then filter off such non-authorised submissions.

## When should I use a radio button vs a dropdown field? 

For 6 or fewer choices, it is advised to use a radio button, as there are only a few options to display:

![FormSG FAQ Radio Button](https://s3-ap-southeast-1.amazonaws.com/misc.form.gov.sg/faq-radio.png "FormSG FAQ Radio Button")

For >6 choices, you should use a dropdown field: 

![FormSG FAQ Dropdown](https://s3-ap-southeast-1.amazonaws.com/misc.form.gov.sg/faq-dropdown.png "FormSG FAQ Dropdown")

## Excel responses from table style questions are clumped into one line, how do I separate them?

1. Open the excel sheet generated from our Data Collation Tool
2. Select the entire column of the responses
3. Go to the Data tab and choose Text to Columns > Delimit by comma (,).

![FormSG FAQ Excel Split Response](https://s3-ap-southeast-1.amazonaws.com/misc.form.gov.sg/faq-excel.png "FormSG FAQ Excel Split Response")

## How can I split the form into multiple pages?

We don't support multiple pages, because >70% of our users fill in forms from their phones, and are used to navigate through content by scrolling not tabbing through pages, such as when they scroll through their social media feeds. Hence we built the Header field to separate your form into sections that your user can scroll through.

![FormSG FAQ Create Section](https://s3-ap-southeast-1.amazonaws.com/misc.form.gov.sg/faq-section.png "FormSG FAQ Create Section")

## How do I know if the logic for the form is correct?

When you implement a new logic, you should test it yourself via the preview page. Note that the onus is on you to verify the correct logic for your form.

![FormSG FAQ Logic](https://s3-ap-southeast-1.amazonaws.com/misc.form.gov.sg/faq-logic.png "FormSG FAQ Logic")

## What is FormSG’s infrastructure like?

We have our NodeJS web servers hosted on AWS Singapore zone. Our NoSQL database that stores only form fields and not form data is managed by Mongo Atlas, and also hosted on AWS Singapore zone. We use AWS SES to send out mails, which are not open mail relays, have valid SPF and DKIM records, and encrypts form data before sending them over to government SG-Mail. Our web servers are protected with Cloudflare SSL, their Anti-DDoS protection and Web Application Firewall. We use Pingdom for website performance and availability monitoring, and have AWS CloudWatch alarms. Our Data Collation Tool is built with vanilla Javascript and hosted on top of Nectar on the Intranet, and is an S3 static site on the Internet.

## Does my data go to your server when I use the Data Collation Tool?

No, your data is not seen by our server. Aggregation of your email responses happens offline on your browser. Another way for you to use the Data Collation Tool is to save the web page and open it again to use it without network connectivity. When you're on the Data Collation Tool's site, you can simply Right Click > Save As to download the web page, then open the web page to use the tool as per usual.

## Email reliability

## Will my emails be blocked?

If emails are non-malicious, they typically will not be blocked. There are two junctures where they might be blocked, but the form submitter will know about it and will be able to retry:

- When a user clicks Submit on his form, the response first goes to our server. Before reaching our server, we have a web application firewall that detects for malicious content and might block the submission. If blocked, a user will see a "Please try again later" message on the form.

- If the form passes the web application firewall, it goes to our server, and we email it to your government email (SGMail) without storing it on our servers. If the government email does not exist then your response will bounce and the user will see a "Please try again later" message on the form.

From here on out, if the email is blocked, your user will not be aware. But there is still a way for you as the form creator to retrieve the blocked responses:

- If the government email exists, it proceeds to SGMail servers. Before it enters SGMail, it will arrive at SGMail's firewall. This firewall will block out emails if there are attachments with non-whitelisted file extensions, for e.g. ".abc" or ".mov". We are not aware of the full list of file extensions that SGMail whitelists, but most of the file extensions that are whitelisted can be viewed here on [our spreadsheet](https://go.gov.sg/email-cwl). If your email gets blocked due to non-whitelisted attachment file extensions, you will receive a mail hygiene notification. You may contact SPEAR (spear@tech.gov.sg) within 1 month from receiving the mail hygiene notification to retrieve the dropped mail.

## How do I recover my mail when I receive a mail hygiene notification?

You may recover your blocked email within 1 month if you email SPEAR (spear@tech.gov.sg) and attach the mail hygiene notification.

## What is Storage mode?

FormSG does not store your responses in the clear. In Storage mode, form responses are encrypted, before being sent to our server for storage. Here's how it works:

1) You create a form using Storage mode, and is prompted to download a form password which you have to keep safe:

![FormSG FAQ Storage Create Form](https://s3-ap-southeast-1.amazonaws.com/misc.form.gov.sg/faq-storage-createform.png "FormSG FAQ Storage Create Form")

2) When user submits your form, responses gets encrypted on user's browser before being sent to our server for storage:

![FormSG FAQ Storage Encrypted](https://s3-ap-southeast-1.amazonaws.com/misc.form.gov.sg/faq-storage-encrypted.png "FormSG FAQ Storage Encrypted")

3) When you want to retrieve responses, visit the Results tab, and enter your form password in order to download encrypted responses have them decrypted on your browser with the form password you provide:

![FormSG FAQ Storage View Response](https://s3-ap-southeast-1.amazonaws.com/misc.form.gov.sg/faq-storage-viewresponses.png "FormSG FAQ Storage View Response")

4) You may then view your responses one-by-one or click the Download button to export all responses to an Excel.

## What are the benefits of this mode over Email mode?

The key benefit here is convenience. You no longer have to manage emails, and no longer have to manually aggregate emails into Excel using the Data Collation Tool. If your form has high volume such as tens of thousands of responses or more, it can be quite painful to manage those responses in your mailbox.

## When is Storage mode coming out?

With Storage mode, responses will be in the clear on an Internet device, which is not ideal. Hence we are first moving FormSG to the Intranet first before launching Storage mode. Storage mode is expected to be launched end of 2019.

## This form password sounds important. What if I lose it?

Note that the form password has to be kept safely by you. Our server will not be able to recover the form password for you if you lose it. This is a key security benefit, because that means if our server were to be compromised, the attacker will not have the form password to unlock your encrypted responses, and will only see gibberish.

If you really do lose your form password, you will lose past responses. Unfortunately, there is no way for us to retrieve the form password for you. It is advised you promptly duplicate the form, and publish the new form with a new form password to continue gathering responses from your users. We are actively discussing with agencies to see if a backup password can be stored by the relevant parties in agencies.

## How should I keep my form password safe?

It is recommended you at least pass the password to one other colleague just in case. You may email yourself the password. Or store it in a third-party password manager tool. And most importantly, it is advised you regularly log in to decrypt your form responses to make sure you still have the form password.

## What if I want to purge the encrypted data on the FormSG server?

To purge encrypted data from our server, all you have to do is destroy/delete/forget your form password. Because our server only stores gibberish, without the form password, your data is as good as being purged.

## What if my form password has been accidentally circulated?

A first step is to download the data, then create a new form with a new form password and continue gathering responses from this new form. Then send us an email to assist you in deleting the responses from the old form with the leaked form password.

## How do I suggest changes to this user guide?

Our user guide is hosted by [OpenDoc](https://opendoc.sg) and is written in [Markdown](https://www.markdownguide.org/), which is a laymen-friendly language. The code for our user guide is open-sourced, and you may visit our [Github repository](https://github.com/opendocsg/opendoc-formsg-faq), and send us a [Pull Request](https://help.github.com/en/articles/creating-a-pull-request) if you have corrections or suggestions to the guide.
