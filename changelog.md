## 1.2.33 - 2021-12-04
- Added Pushover Notification Provider
- Added Incident Management
- Improved install.sh script
- Fixed RateLimiter to API
- Added flushing cache on forceUpdate values (e.g for designer action)
- Added new frontend construct to category list (code/components separated)

** Deprecated **
- API v1

## 1.2.32 - 2021-10-10
- Added Pagination to monitors

## 1.2.31 - 2021-10-09
- Added Caching
- Added API for resource crud
- Added Code Editor for Javascript
- Added Two-Factor Authentication
- SLA calculation on statuspage
- Designer for moving monitors between categories
- Improved Alert-System (Added answering -> UI)
- Added install script
- Added Docker-Compose file for fast-deployment
- Reworked the Frontend (TailwindCSS & Vuejs)
- Added resend of verification (newsletter) 
- Added Session-Management
- Added Logo to some mails
- Added Dark/Light Mode

[Read Blog](https://blog.livck.com/veroffentlichung-unserer-software-aktualisierung/)

## 1.1.3 - 2021-06-18
- Added customization of style (A box for styling the page was added to the settings site)
- Newsletter notifications will be sent via the queue from now on
- Newsletter input is cleared after successful sending
- Added caching for public data
- Added StateChangedEvent for calling updates arround the application
- Added SQL-Indexes on tables
- Dropped unique of sort_id in monitors (No data will be lost through the update!!)
- Fixed route-names
- Removed some inline styles and migrated to classes
- Added listener for flushing data on cache (public data)
- Fixed keywords metatag (wrong data was displayed)
- Added style file to main path (Stored custom style)

** Important for the update command **
- Confirm at the update command that the resource files may be replaced!

## 1.1.2 - 2021-06-16
- fixed sla on monitor overview (SLA was displayed in decimal)

## 1.1.1 - 2021-06-16
- fixed cleanup command (incorrect sql statements were corrected)

## 1.1.0 - 2021-06-16
- added advanced monitor check (This check, can verify if a service is really down. This works with a delay & retries which are executed via the queue. This check is also customizable)
- added cleanup command (The command can either run itself or be automated. This will delete all incidents over 60 days - the days are also customizable)
- fixed logo/favicon upload (The cache is now updated when a new image is uploaded)
- fixed discord embeds (Duplicate embeds due to not finding the message)
- fixed logo/favicon mimetypes (From now on all mimetypes are allowed to upload his logo)
- added ip-resolver (Now you can specify with which IP resolver to access our license servers. [V4,V6])

#### important for upgrading to this version 
add following section to config/livck.php
```php
'ip_resolver' => 'V4',
'advanced_monitor_check' => 'true',
'advanced_monitor_tries' => '5',
'advanced_monitor_delay' => '5',
'automatic_cleanup' => 'true',
'automatic_cleanup_range' => '60 days',
```

## 1.0.9 - 2021-04-28
- added remembering state to collapsed categories
- added email-alerting checkbox to profile (to specify whether email downtime notifications can be sent or not)
- added manual type to monitors (this type is for non-automated checking | only for monitors which are set manually)

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

