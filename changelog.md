## 1.0.8 - 2021-03-31
- fix table overflow (ACP)
- added ssl-certificates checks
- added legal redirection (imprint & privacy-policy)
- changed style of <a> tag (added opacity on hover state)
- added autofixer for missing configuration keys
- added favicon-uploader
- added preview for project-image & favicon on theme settings
- added version view (ACP - on left-top)
- added translations to ACP (not 100% completely)
- centered status pill to monitor overview
- added overall statuspill on categories
- removed useless stuff from monitors table (ACP)

#### important for upgrading to this version 
add following section to config/livck.php
```php
'imprint_url' => 'your-domain.com/imprint',
'privacy_policy_url' => 'your-domain.com/privacy-policy',
```

## 1.0.7 - 2021-03-23
- Fixed Line-Spacing from Compose Alert Editor
- Added collapse to monitor list (Homepage/Overview)
- Fixed Updater (assets loading)
- Added image uploader
- Added positioning of newsfeed (alerts)

## 1.0.6 - 2021-03-21
- Added Incident Creator (For past failures)

## 1.0.3 - 2020-12-03
- An updater has been added which brings the project up to date with one command
- An version command was added

## 1.0.2 - 2020-12-01
- The .env was renamed to .env.example to simplify the update process
- Fixed empty string on guard permission check

## 1.0.1 - 2020-11-30
- Fixed that the software can now be used without a mail server
- License check has been reworked and no longer throws errors when a freshly set up project

## 1.0.0 - 2020-11-06
Release of our software 😊
- We have made our software sale proficient for 2020-11-06

