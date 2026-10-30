<h1 align="center">Capveriq – Permission & Access Debugger</h1>

<p align="center"><b>Find out why a WordPress user cannot access a page or action: roles, capabilities and permission traces.</b></p>

<p align="center">
  <a href="https://wordpress.org/plugins/capveriq-permission-access-debugger/"><img src="assets/download-wporg.svg" alt="Download on WordPress.org" height="36"></a>
</p>

<p align="center">Free WordPress plugin · Version 1.0.1 · GPLv2 or later</p>

> [!NOTE]
> Capveriq – Permission & Access Debugger is officially distributed through **WordPress.org**. Please download, install and get updates from its [WordPress.org page](https://wordpress.org/plugins/capveriq-permission-access-debugger/) so you always have the latest reviewed version.

## About

Capveriq helps WordPress administrators find out why a user cannot access an admin page or perform an action.

Instead of editing roles blindly, Capveriq inspects roles, effective capabilities, registered admin-menu requirements, mapped capabilities and temporary runtime permission traces.

Capveriq is a diagnostic tool and does not automatically modify user permissions.

**The problem Capveriq is built for**

You have probably seen these messages:

- “Sorry, you are not allowed to access this page.”
- “You do not have permission to perform this action.”

A menu item disappears. A plugin screen becomes unavailable. A user has what looks like the correct role and is still denied. Role editors show you capability checkboxes, but they do not tell you *why* the request failed.

Capveriq answers a different question: which capability did the page require, does this user have it, and did anything change the decision at runtime?

**What Capveriq examines**

- The capability registered by the admin menu or submenu entry for the requested page.
- The selected user’s roles, role-provided capabilities and directly assigned capabilities.
- Meta capability mapping through the WordPress `map_meta_cap` API.
- Runtime capability results through the `user_has_cap` filter.
- Callbacks that other plugins and themes have registered on those permission hooks.
- Multisite and Super Admin context.
- Request context: wp-admin, frontend, AJAX, REST, cron, WP-CLI and Network Admin.

**Honest diagnostics**

Results use Confirmed, Likely, Possible or Unknown confidence labels. Capveriq does not present inference as proof. When evidence is insufficient it reports Inconclusive and recommends Live Trace.

**Read-only by design**

Capveriq never adds, removes or edits roles, capabilities or users. It reads, explains and reports.

**Local only**

Diagnostics run locally. Capveriq uses no external API, telemetry, remote fonts, account or licence key.

### Features

- Access diagnosis for any user against any wp-admin URL.
- Admin menu and submenu capability detection from the live `$menu` and `$submenu` data.
- Core admin page analysis with a maintained fallback map.
- Plugin and custom admin page analysis.
- User capability inspector with search and All / Allowed / Denied / Direct / Inherited filters.
- Role capability inspector (read-only).
- Capability test tool with optional object ID and meta capability mapping.
- Temporary Live Trace for one selected user, with 5, 10 or 15 minute durations.
- `user_has_cap` and `map_meta_cap` observation that never alters permission results.
- Hook callback inventory with plugin, MU-plugin, theme, child theme and core classification.
- Denied admin access logging with retention and record limits.
- Request context detection including AJAX, REST, cron, WP-CLI and Network Admin.
- Multisite and Super Admin awareness.
- Privacy-safe diagnostic report export and a full system report.
- Diagnostic data cleanup tools and optional data removal on uninstall.

### How It Works

- Open **Capveriq > Diagnose Access**.
- Select the affected user and paste the wp-admin URL they cannot open.
- Run the analysis. Capveriq reports the capability the page requires, whether the user has it, and where that capability comes from.
- If static analysis is not conclusive, start a **Live Trace** for that user.
- Ask the affected user to reproduce the problem while the trace is running.
- Return to Capveriq and review the captured capability checks, mapped capabilities and the callbacks registered on the relevant permission hooks.
- Export a privacy-safe report and share it with your developer or with the responsible plugin’s support team.

The trace expires automatically. Nothing about your site’s permissions is changed at any point.

### Privacy

Capveriq stores diagnostic data in your own WordPress database and sends nothing to any external service.

Capveriq never stores passwords, cookies, authorization headers, API keys, application passwords, nonce values, payment data, POST form contents, private messages or any credential from `wp-config.php`.

Trace events record the capability being checked, the mapped capabilities, the result, the request path and context, and the classified source file where one can be determined. Absolute server paths are reduced to site-relative paths such as `wp-content/plugins/example/file.php`, so hosting account names and home directories are never displayed.

With **Privacy-safe Reports** enabled (the default), exported reports mask the site domain, identify users by ID rather than by email address, and exclude server paths, IP addresses and authentication information.

Trace sessions and denied access records are pruned automatically using the retention period you configure, while the denied log also respects its maximum record count. You can clear trace data, the denied access log or all diagnostic data at any time from **Capveriq > Settings**. Capveriq integrates with WordPress personal data export and erasure tools for diagnostic records associated with registered users, and removes those records when the related WordPress user is deleted. When **Delete Data on Uninstall** is enabled, all Capveriq tables and options are removed when the plugin is deleted.

### Developers

Diagnostic data lives in three custom tables created with `dbDelta()`:

- `{prefix}capveriq_sessions`
- `{prefix}capveriq_events`
- `{prefix}capveriq_denied`

When Live Trace is off, Capveriq performs no `debug_backtrace()` calls, no reflection on hook callbacks and no trace database writes, and it loads no frontend CSS or JavaScript. Deep tracing runs only for requests made by the single selected target user while a session is active and within the configured event limit.

**Known limitations**

- Some plugins register admin menu pages conditionally, based on the currently logged-in administrator. Static menu inspection can therefore differ from the target user’s runtime menu. Capveriq says so instead of guessing, and recommends a Live Trace.
- Custom PHP can restrict access without using WordPress capability APIs at all. Such checks are invisible to any capability-based tool, including Capveriq.
- When capability state changes during `user_has_cap` processing, Capveriq reports that the state changed and lists the registered callbacks separately. It does not claim which callback was responsible.

## Requirements

- WordPress 6.4 or higher
- Tested up to WordPress 7.1.4
- PHP 7.4 or higher

## How to install

1. In your WordPress dashboard go to **Plugins → Add New Plugin**.
2. Search for **Capveriq**.
3. Click **Install Now**, then **Activate**.

Or download it directly from **[WordPress.org](https://wordpress.org/plugins/capveriq-permission-access-debugger/)**.

## Support

Questions or problems? Please use the **[support forum on WordPress.org](https://wordpress.org/support/plugin/capveriq-permission-access-debugger/)**.

## Author

Developed by **[Muhammad Mujahid Sarfraz](https://profiles.wordpress.org/mujahidwp/)** · [All my WordPress products](https://profiles.wordpress.org/mujahidwp/) · [LinkedIn](https://www.linkedin.com/in/muhammad-mujahid-sarfraz-2631a43b6)
