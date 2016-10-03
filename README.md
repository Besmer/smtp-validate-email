# SMTP\_Validate\_Email

Perform email address validation/verification via SMTP.

The class retrieves MX records for the email domain and then connects to the
domain's SMTP server to try figuring out if the address really exists.


### How to install with composer

Add to you composer.json file this code

```json
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/Besmer/smtp-validate-email"
    }
  ],
  "require": {
    "smtp-validate-email/smtp-validate-email": "dev-master"
  },
```

### Some features (see the source for more)

* Not really sending a message, gracefully resetting the session when done
* Command-specific communication timeouts implemented per relevant RFCs
* Catch-all account detection
* Batch mode processing supported
* MX query support on Windows without requiring any PEAR packages
* Logging and debugging support

### Basic example
```php
<?php

use SMTPValidateEmail\SMTPValidateEmail;

$from = 'sendingemail@test.test';
$email = 'emailtoverify@test.test';

$validator = new SMTPValidateEmail($email, $from);
$smtp_results = $validator->validate();

print_r($smtp_results);

```

### Array usage
The class supports passing an array of addresses in the constructor or to the
`validate()` method. Checking multiple addresses on the same server uses
a single connection.
```php
<?php

use SMTPValidateEmail\SMTPValidateEmail;

$from = 'a-happy-camper@campspot.net'; // for SMTP FROM:<> command
$emails = array(
    'someone@somewhere.net',
    'some-other@somewhere-else.net',
    'someone@example.com',
    'someone-else@example.com'
);

$validator = new SMTPValidateEmail($emails, $from);
$smtp_results = $validator->validate();

// or passing to the validate() method
// $validator = new SMTPValidateEmail();
// $smtp_results = $validator->validate($emails, $from);

print_r($smtp_results);
```
