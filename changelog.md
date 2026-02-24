# v1.4.5 - 2026-02-24
<Note>
test
</Note>
> **⚠️ Important: After updating, you must restart your Docker stack for all changes to take effect:**
> ```bash
> cd /opt/livck && docker compose down && docker compose up -d
> ```
> If the update didn't apply correctly, you can force a re-run:
> ```bash
> cd /opt/livck && docker compose exec app php artisan update --force-pull --force
> ```

### Added
- **Timezone Support** - Users and public visitors can now select their preferred timezone
  - All dates and times across the platform are timezone-aware
  - New DateTime picker in Alert and Incident forms
- **Maintenance Windows** - Schedule and track planned maintenance with automatic start/end handling
  - Dedicated maintenance alert type with automatic state transitions
- **Sticky Alert Banners** - Display persistent announcements on your status page – always visible, stackable
  - Configurable banner display in alert management
- **PDF Attachments** - Attach PDF documents to alerts (e.g. for RCA reports or documentation)
  - Upload and manage files directly in alert forms
- **Alert Templates** - Create reusable templates for recurring alert types
  - Template selection when creating alerts
  - Default templates included – your existing customizations won't be overwritten
- **Alert Enhancements**
  - Link alerts to specific monitors
  - Schedule alerts with end date and duration
  - Active alert badges visible on monitor list entries
  - Affected services display on alert pages
- **Newsletter Improvements**
  - Monitor-specific subscriptions – subscribers choose which services to follow
  - Preference management page for subscribers
  - Import/Export for subscribers (CSV & JSON)
  - Locale support and manage-preferences links in emails
- **Localization** - Multi-language support for alerts and status pages
  - Language tabs in alert creation and editing
  - Locale switcher on public status pages
  - Automatic language fallback
- **Display Status** - Override the displayed status of a monitor with a custom message
  - Improved incident bar colors based on manual overrides
- **Demo Mode** - Built-in demo system for showcase environments
- **License System** - New license management (no action required)
- **Powered by LIVCK** - Optional badge for paid customers
- **Bulk Delete** - Bulk delete functionality across all list pages
- **Status Icon Legend** - Visual legend on status pages explaining status icons

### Changed
- **Dashboard** - Completely redesigned dashboard with improved layout, KPI cards, and quick actions
- **Eclipse Theme** - Set as default theme with updated color palette (zinc tones) and smooth view transitions
  - We're focusing exclusively on `Eclipse` for now to ensure every feature gets the quality it deserves. Multi-theme support may return in a future update

### Improved
- **Performance** - Significant speed improvements across the platform
  - Reduced API response times by eliminating redundant database queries
  - Improved notification dispatch for large subscriber lists
  - SLA calculation limited to 90-day window for faster loading
  - Settings cached by default for faster page loads
- **Upgrade Process**
  - Automatic recovery when updates are interrupted mid-process
  - Cache is now cleared automatically after version upgrades
  - Improved handling of invalid data during timezone conversion
- **UI/UX**
  - Improved flash messages across settings and monitoring pages
  - Adjusted title visibility and layout components
  - Updated form layouts and components
  - Refreshed Roles management page
  - Updated tooltip and CSS styles

### Fixed
- **Caching** - Fixed an issue where cached values could be computed twice
- **SSL Monitoring** - Corrected notification handling in SSL certificate observer
- **Monitor Checks** - Improved error handling in monitor cron job
- **Alerts** - Improved reliability of alert loading and error logging
- **API** - Fixed route model binding on V2 API routes
- **Modal** - Fixed z-index and dark mode contrast issues
- **Theme** - Ensured Eclipse theme applies correctly to all public pages
- **Sessions** - Fixed authentication issues in development environments
- **Deployment** - Improved build verification and cleanup of legacy assets


# v1.4.4 - 2025-10-05

### Added
- **Badge Builder** - New visual badge builder interface for creating custom status badges
- **Uptime Calendar** - Historical uptime visualization with monthly calendar views (Eclipse theme exclusive)
  - Feature toggle via `uptime_calendar_enabled` setting
  - Navigation through up to 24 months of history
  - SLA visualization with color-coded calendar days
- **Pagination** - Added pagination to Announcements and Maintenances pages

### Changed
- **Install Script** - Updated to use `docker compose` instead of deprecated `docker-compose`
- **Documentation** - Refactored documentation for improved clarity and organization
  - Updated [Installation](/installation) guide
  - Updated [upgrade flow](/upgrade) documentation
  - Updated Resources section on homepage
  - Added [Discord Bot](/discord-bot) documentation
  - Added [PWA (Progressive Web App)](/pwa) documentation
  - Added [Alerts](/alerts) feature documentation
  - Added [Badges](/badges) feature documentation
  - Added [Designer](/designer) feature documentation
  - Added [Uptime Calendar](/uptime-calendar) documentation `Eclipse exclusive`
  - Added [Discord Webhook](/discord-webhook) documentation
  - Added [Themes](/themes) documentation
  - Added [Notification Throttling](/notification-throttling) documentation
  - Added [Permissions](/permissions) documentation
  - Added [Users & Roles](/users-and-roles) documentation
  - Added [Private Page](/private-page) documentation
  - Fixed MariaDB logo display in dark mode

### Improved
- **Caching** - Improved cache TTL (Time To Live) configurations for better performance
- **Database** - Improved database modes with strict mode enforcement
- **SLA Calculation** - Optimized SLA calculation performance
- **Eager Loading** - Improved eager loads for Incidents to reduce database queries
- **License Check** - Improved license validation with better error handling

### Fixed
- **N+1 Issues** - Fixed database N+1 query issues for improved performance
- **File Upload Validation** - Added missing validation for file uploads in appearance settings

# v1.4.3 - 2025-06-03
- **API v3 Performance Improvements**
  - Improved category API endpoint
  - Improved category <-> monitors API endpoint
- **System Improvements**
  - Enhanced monitor check with added chunking support
    - Now supports chunking for large monitor lists, improving performance and reducing load times.
  - Optimized cron execution
  - Enhanced dashboard to incidents loading
  - Improved data iteration in the backend calculation
  - Fixed SLA calculation
  - Added incident archiving for automatic cleanup
    - Incidents are now archived instead of deleted, allowing for long-term statistics
- **New Features**
  - Added SMS notifications via [ClickSend](http://clicksend.com/?u=523222)
    - Setup requires a ClickSend account and API key.
      - Create an account at [ClickSend](http://clicksend.com/?u=523222)
      - Top up your **account balance** to send SMS
      - Add your credentials in the **.env** file
        - `CLICKSEND_USERNAME`
        - `CLICKSEND_API_KEY`
      - Configure your **Phone Number** in the profile settings and run **"Test all configured Notification-Channels"** to verify the setup.
  - Implemented rate limiting for SMS (throttling - intended to cost control)
  - Added phone number to user information (for SMS notifications)
  - Added option to enable/disable newsletter mail confirmation
- **Technical Upgrades**
  - Upgraded build dependencies
  - Added custom PHP.ini configuration
    - Increased PHP memory limit to 512MB
  - Improved MariaDB configuration

# v1.4.2 - 2025-03-18
**When using Docker**: Please **pull** the latest image with following command and **restart** docker-compose stack: 
`cd /opt/livck && docker-compose pull app`

- **Improved Performance**
  - Optimized database queries for better performance.
  - Reduced the number of queries for improved efficiency.
  - Added missing indexes & primaryKeys to improve query performance.
  - Improved Cache Handling
  - **Optimized Server Configuration**
    - OPcache reconfigured
    - PHP-FPM reconfigured
    - php.ini optimized
    - nginx improved rate limiting and caching
    - MariaDB configuration added (innodb increased buffer pool size)
- **Fixed Chart Style** (unstyled percentageChange "badge" )
- **Fixed Eclipse Theme**
  - Header Spacing (Y) on Mobile Devices
  - Layout Spacing (X) on Mobile Devices
  - Fix Empty State on maintenance & alert list page
  - Fixed Dark/Light switch on auth pages
- **Added Incident Update Slide**
  - Now it's possible to update an incident's identifiedAt & resolvedAt

# v1.4.0 - 2025-03-14

## UI/UX Improvements
- **Dashboard Enhancements:**
    - Improved overall dashboard style.
    - Enhanced navbar design for better usability.

## New Settings
- **Monitors:**
    - **Automatic Incident Creation:** Option to automatically create incidents for manual monitors when their status changes to "Unavailable".
    - **Prioritization of Unavailable Monitors:** When enabled, monitors with status "Unavailable" are displayed at the top of their category list, overriding the general sorting rules.

## Discord Status Pager Updates
- **Previous Functionality:**
    - Status information for categories and monitors was combined into a single text message.
- **Updated Functionality:**
    - A dedicated bot now handles all status updates.
    - The webhook logic is exclusively used for updates of individual monitors.
    - The bot can be directly invited to and configured on your server.
    - Extended features include sending alerts and maintenance updates.
- **Open-Source Release:**
    - The Discord-Bot is now available as an open-source project on [GitHub](https://github.com/LIVCK/livck-discord-bot).

## Improved Alert System
- **New Alert States:**
    - INVESTIGATING
    - IDENTIFIED
    - OBSERVING
    - RESOLVED
    - ACKNOWLEDGED
    - IN_PROGRESS
    - UNDER_REVIEW
    - CLOSED
    - SCHEDULED
- **Additional Enhancements:**
    - Added a new alert type: "Maintenance".
    - Introduced functionality to directly update the state of an alert.

## New Theme: Eclipse
- **Modern Design:** Eclipse brings a contemporary, modern look to the status page.
- **Dark & Light Mode:** Seamlessly supports both dark and light mode.
- **Clean & Pleasant Colors:** Features a refined palette that is both clean and visually appealing.
- **Elegant Rounded Corners:** Beautifully rounded design elements add a touch of sophistication.
- **Visual Impact:** An absolute eye-catcher that enhances the overall user experience.
- **Additional Features:**
    - Includes an alert update line to clearly display the history of updates.
    - Provides a dedicated maintenance page for maintenance alerts.
    - Features a skeleton loader for a smooth and seamless loading experience.

## Added Credits Badge
- A credits badge is now displayed in the footer of the status page.
- The badge is only removable with the `Business` plan or higher.

## Tech Stack Upgrade
- Various underlying improvements and updates to the technology stack.




## v1.3.32 - 2025-01-29
- Request Password-Link patched

## v1.3.31 - 2024-07-23
- Fix Table Column Overflow
- Added truncations for texts
- Fix Blank Page on License Expiry

## v1.3.3 - 2024-01-19
- Added PWA `Implemented Progressive Web App (PWA) functionality, enabling the Statuspage to be installed similarly to a mobile application.`
- Fixes
  - Dashboard Available / Unavailable Progress Bar `Hide Zero-Values`
  - Truncate Table `Alerts title`
- Added Env-Vars `.env`
  - APP_TIMEZONE `default: Europe/Berlin`
  - APP_LOCALE `default: en`
  - APP_LOCALE_FALLBACK `default: en`

## v1.3.2 - 2023-12-09
- UI/UX
  - Design Update (Input, Select, Checkboxes)
  - License Expire Page (Prevent Empty Page on Dashboard) / Invalid Page
  - Improved Permission/Roles Management on Member Edit
  - Added new "Password Banner" on Member Create (Preview of the generated password)
  - Improved Designer (Organize Categories and Monitors)
  - Improved Dashboard (New Statistics, Incidents Timeline)
  - Improved Apperance Upload
  - Updated Settings Page
  - Reorganized Sidebar Menu
- Healthcheck Check
  - A new check has been added for checking cronjobs or other services that should be ping a specific URL
- Improved TCP Check
  - Added latency (ping) to TCP Check
- Changed Compieler from `webpack` to `vite`
- New Settings
  - Alerts
    - Scheduled Alerts Display Days (Define max age for scheduled alerts to be displayed on statuspage)
    - Alerts Display Days (Define max age for alerts to be displayed on statuspage by scheduled_at date)
  - Shows Login Button (Show/Hide Login Button on Statuspage)
- Drop Support for Upgrading from livck-v1.2.0 or lower
- Improved Install-Script
  - Added arguments to script (like ./install.sh --license=X --ipv=4 ...)
- Added Export/Import for DB
  - php artisan db:export {filename? : The name of the export file} (optional)
  - php artisan db:import {filename? : The name of the import file} (optional)
  - always stored in `storage/app/dumps` (also for imports)
- Added Download for 2FA Recovery-Codes (Text File)

## 1.3.0 - 2023-03-07
- [App] Upgraded to PHP 8.2 (Old versions not supported!)
- [App] Upgraded Laravel 8 to 9
- [Docker] Updated Docker-Image (PHP 8.2)
- [Docker] Fixed certbot auto-renew certificates

## 1.2.40 - 2023-02-28
- Fixed HTTP/Check

## 1.2.39 - 2022-12-16
- Replaced Google Fonts to "self-hosted" fonts

## 1.2.38 - 2022-08-02
- Added incident-create-trigger to manual monitors
- Improved Alert Section (Showing monitor when incident is selected)

## 1.2.37 - 2022-07-11
- Added Support for non-ssl (http) statuspages
- Improved install.sh

## 1.2.36 - 2022-06-01
- The logic of the check process completely reconceptualized
  - HTTP-Check
    - Reworked:
      - Incident-View
      - Configuration of the monitor
  - Added Incident Log (Currently only for HTTP)
- Added new setting fields
  - SLA hide/show on site
  - Newsletter disable/enable subscription
- Improved Style of Tabs
  - Monitor / HTTP
  - Settings
- Added Notification-Test to Profile for testing all configured Channel


## 1.2.35 - 2021-12-31
- Added autoupdater (Default enabled)
- Improved install.sh
  - Added Port-Check (80 & 443)
  - Added whitelist check
  - Colored error messages
  - Added check if compose stack not running (with timeout)
- Added theming-system
  - Added the "Inception Theme" - A theme similar to the first layout of livck (back to the roots)
- Fixed duration of transitions (divider dark/light switch)
- Added Private-Page feature
- Fixed each selects (default selected)
- Added missing translations keys (german language)
  

## 1.2.34 - 2021-12-14
- Improved monitors load (load if category not hidden)
- Added apperance remove action to logos
- Improved install.sh script (added credentials and login link, check containers state)
- Removed nginx ratelimit
- Fix interval clear to statuspage

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

