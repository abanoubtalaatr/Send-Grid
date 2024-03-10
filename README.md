# SendGrid Integration

Integrate SendGrid into your application for seamless email communication using the API method.

There are two ways to integrate:
- SMTP
- API (this documentation focuses on API integration)

## Table of Contents

- [Install SendGrid](#install-sendgrid)
    - [Prerequisites](#prerequisites)
    - [Installation](#installation)
- [Usage](#usage)

### Prerequisites
1. Visit the official [SendGrid website](https://sendgrid.com/en-us).
2. Navigate to [Sender Authentication](https://app.sendgrid.com/settings/sender_auth/senders).
3. Click "Create new Sender," complete all requirements, and ensure you provide a valid email for verification. Save the API key generated during this process.
4. Delete any configuration for email if exists.
5. Set the following variables in your `.env` file:
    - `MAIL_FROM_ADDRESS`
    - `MAIL_FROM_NAME`
    - `SENDGRID_API_KEY`

### Installation
Execute the following command to install the SendGrid package using Composer:

```bash
$ composer require sendgrid/sendgrid
```

### Usage 

- (new SendGridService())->sendMail("Reject Email", 'abanoubtalaat555@gmail.com',$data,'mail.reject_driver');
- - Must Provide 
- - - Email subject
- - - Email Address
- - - Data will pass it to view
- - - Email View 

```php
class SendGridService
{
    public $email;
    
    public function __construct()
    {
        $this->email = new \SendGrid\Mail\Mail();
    }
    
    public function sendMail($subject, $to, $data, $viewPath)
    {
        $this->email->setFrom(env("MAIL_FROM_ADDRESS"), env("MAIL_FROM_NAME"));
        $this->email->setSubject($subject);
        $this->email->addTo($to);
        $this->email->addContent("text/html", view($viewPath, $data)->render());
        
        $sendgrid = new \SendGrid(getenv('SENDGRID_API_KEY'));
        $sendgrid->send($this->email);
    }
}
```
