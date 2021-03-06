# SMTP

This package is a new SMTP class built from scratch.  Many of the existing email libraries are old, bloated, not on GitHub, and worst of all written in camelcase.  I wanted something short and simple.

12/20/2013 - I know that Laravel 4 contains its own mailing class based on SwiftMailer, but I still have problems with that software.  I've decided to continue development of this package for the time being.

## Install ##

Normal install via Composer.

### Provider

Register your service provider in ``app/config/app.php``:

```php
'Travis\SMTP\Provider'
```

You may also wish to add an alias to remove the namespace:

```php
'Date' => 'Travis\SMTP'
```

### Configuration

You should copy the config file provided to ``app/config/packages/travis/smtp/config.php`` and input the necessary information.

## Usage

A normal email would go like this:

```php
$mail = new SMTP();
$mail->to('tim@gmail.com');
$mail->from('paul@gmail.com', 'Paul T.');
$mail->subject('Hello World');
$mail->body('This is a <b>HTML</b> email.');
$result = $mail->send();
```

You can add multiple recipients, name is optional:

```php
// add to
$mail->to('matthew@gmail.com');
$mail->to('mark@gmail.com');

// add cc
$mail->cc('luke@gmail.com');
$mail->cc('john@gmail.com');

// add bcc
$mail->bcc('james@gmail.com');
$mail->bcc('peter@gmail.com');
```

You can add recipients en masse:

```php
// build list
$list = array();
$list[] = 'matthew@gmail.com';
$list[] = 'mark@gmail.com';

// add to
$mail->to($list);

// build list w/ names
$list = array();
$list[] = array('matthew@gmail.com', 'Matthew');
$list[] = array('mark@gmail.com', 'Mark');

// add to
$mail->to($list);
```

You can set a custom reply-to address:

```php
$mail->reply('paul@gmail.com', 'Paul T.');
```

You can pass arrays to set from and reply-to addresses:

```php
// set from
$from = array('paul@gmail.com', 'Paul T.');

// add from
$mail->from($from);

// add reply-to
$mail->reply($from);
```

You can add attachments:

```php
$mail->attach('/path/to/file1.png');
$mail->attach('/path/to/file2.png');
```

You can assign a text version of your email:

```php
$mail->text('This is a text email.');
```

You can send text-only emails:

```php
$result = $mail->send_text();
```

### Debug Mode

In the config you can flag ``'debug_mode' = true;``, which can be helpful in testing your SMTP connections.  It will echo server responses from each step in the email sending process.

## Limitations

Below are some current limitations.  Please feel free to contribute to this ongoing project.

* Does not support encryption.
* Does not support priority level.
* Does not keep connection open for spooling email sends.
