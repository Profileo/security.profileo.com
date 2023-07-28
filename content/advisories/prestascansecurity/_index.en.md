---
title: "PrestaScan Security"
categories: advisories
author:
- Profileo.com
meta: "PrestaShop,security,module,prestascan,scan,malware,virus,hack"
date: 2023-05-05T17:20:48+01:00
---

{{< image
src="/images/prestascansecurity/dashboard-en.png"
alt="PrestaScan Dashboard"
class="center-img head-img">}}

In the ever-evolving digital landscape, ensuring the security of your online store has become more critical than ever. As a company committed to protecting our customers from various threats, we developed **PrestaScan Security**, a powerful **PrestaShop module** designed to identify malware and known vulnerabilities in the PrestaShop core and its modules.

Thanks to the support of the Friends Of Presta association (FOP), we decided not only to **share this module to the entire PrestaShop community, but also to make it free**. PrestaScan Security is now a free and open-source module that provides all users with the best possible alert system for their online stores.  

The module is easy to install and use, keeping you updated on the latest security threats to your website.  

# Summary

- [Main contributors](#main-contributors)
- [Features](#features)
  - [At-risk modules](#at-risk-modules)
  - [Unused modules](#unused-modules)
  - [Core vulnerabilities](#core-vulnerabilities)
- [User Guide](#user-guide)
  - [How to install the module](#how-to-install-the-module)
  - [How to use the module](#how-to-use-the-module)
- [FAQ](#faq)
- [Compatibility](#compatibility)

# Main contributors

This module is fueled by the collective energy of the members of the Friends Of Presta security cell. Here is the list of the most significant contributors in terms of security research, publication of CVE, or development:

{{< inline_images_prestascansecurity
class="center-img head-img">}}

# Features

- Scan your modules to identify vulnerabilities and required updates
- Identify unused modules, with the ability to disable and remove modules in one place
- Be alerted when a new vulnerability is discovered in your module (email and back office notification)
- List known vulnerabilities in PrestaShop Core for your current version
- List unprotected directories

With even more features coming.

## At-risk modules

This scan will list at-risk modules. These include vulnerable modules and modules that require updates.

{{< image
src="/images/prestascansecurity/at-risk-modules-en.png"
alt="At-risk modules screenshot"
class="center-img head-img">}}

When a module is vulnerable in its current version, it will be displayed in the list with a color label indicating the risk level (red = critical, yellow = medium, green = low). The number in the label indicates the number of vulnerabilities detected in the module for your version. You may click on the arrow next to the module list to get the details:

{{< image
src="/images/prestascansecurity/module-vulnerability-detail-en.png"
alt="Module vulnerability details screenshot"
class="center-img head-img">}}

## Unused modules

This scan provides a list of all disabled and uninstalled modules in your shop. You can also uninstall and delete a module directly from this list (however, make sure to confirm the action first with your web agency/developer).

{{< image
src="/images/prestascansecurity/unused-modules-en.png"
alt="Unused modules screenshot"
class="center-img head-img">}}

## Core vulnerabilities

This scan lists all core vulnerabilities for your current version of PrestaShop.

{{< image
src="/images/prestascansecurity/prestashop-cve-en.png"
alt="PrestaShop core vulnerabilities screenshot"
class="center-img head-img">}}

# User Guide

{{< image
src="/images/prestascansecurity/prestascansecurity-logo.png"
alt="PrestaScan Security Logo"
class="center-img head-img">}}

## How to install the module

1. [Download the latest version of the module from this link](https://security.prestascan.com/prestashop).
2. Log in to your PrestaShop back office.
3. Go to the "Modules" section.
4. Click on "Upload a module" and select the downloaded ZIP file.
5. Depending of your PrestaShop version, the module will be installed automatically or you will need to click the install button

## How to use the module

1. Once installed, go to the "Modules" section in your back office.
2. Find "PrestaScan Security" in the list of modules and click on "Configure."

{{< image
src="/images/prestascansecurity/module-installed.png"
alt="PrestaScan Security Logo"
class="center-img head-img">}}

3. Follow the instructions to register and run your first scan.

**Check the FAQ below if you need any additional information or help to use the module.**

# FAQ

## How can I update the module?

When an update is available, a notification will be displayed in your back office.  

A button will allow you to update the module in one click.  

It's required to maintain the module up to date to continue being alerted to new vulnerabilities.

You may also check the latest change from [our GitHub repository](https://github.com/prestascan/prestascansecurity/releases).  

## How does the module handle vulnerability alerts?

When a vulnerability is discovered and publicly revealed or known to be exploited, a security notification is sent to all users that have done at least one scan of module vulnerabilities in the module. Be sure to run this scan at least once.  

## I have an error message trying to create my account, what can I do?

Error messages during account creation are displayed directly in the form. Most of the time, the issue is related to the website you are trying to connect, which is blocking our scan server. The module will not work with sites that are not publicly accessible (such as development environments or websites in maintenance).

You may also be trying to create a second account from the same email address. Currently, the system allows only one email address to be used, and only one site can be linked to this email. You can, for the time being, overcome this restriction by creating an alias of your email (such as myemail+alias@testcompany.test).

## I didn't receive the verification email to validate my email, what can I do?

During registration, we make sure your email is valid as you will later receive security alerts on it. If you didn't receive the verification email, please check your SPAM folder. If you do not find the email in SPAM, try to resend the verification email from the dedicated green button.

If you have still not received the email, make sure you entered a valid email. You can check your profile [from this link](https://security.prestascan.com/user/profile):
{{< image
src="/images/prestascansecurity/registration-edit-profile.png"
alt="PrestaScan Security Registration Edit Profile screenshot"
class="center-img head-img">}}

## I was able to register but cannot finish the setup or cannot start a scan due to token or connectivity error, what can I do?

If you encounter errors trying to finish the setup, please follow the steps below:
1. Delete your PrestaScan account.
You can do that from [your user profile](https://security.prestascan.com/user/profile):
{{< image
src="/images/prestascansecurity/delete-account.png"
alt="PrestaScan Security Delete Account screenshot"
class="center-img head-img">}}

2. Disconnect the account in the module (in the top right corner, click on "log out")

3. Check if you are using the latest version of the module, and reset the module (or uninstall it and install it again), this will remove all existing data/sessions.

4. Repeat the registration process.

If the problem persists, contact our support.

## The scan seems to never complete, what's the issue?

If you see that the scan is in progress and does not complete after some time (typically more than 5~10 minutes), there might be a communication issue (your server is no longer reachable by our server) or another issue during the scan.

{{< image
src="/images/prestascansecurity/scan-in-progress-en.png"
alt="PrestaScan Security Scan in progress screenshot"
class="center-img head-img">}}

Firstly, note that the module will detect scans that are stuck and will display an option to force retrieving the result of the scan.

If you still have the scan in progress after trying again, consider checking your server logs to verify if the notification (webhook) is received. You can contact our support for more details.

## Are there any paid plans or limitations?

The module will always remain free. However, we may introduce paid plans in the future to unlock specific features such as automated scans and reduce some limitations (e.g., the number of scans that can be performed within a specific timeframe). No paid plans are defined yet, but ads from partners might be displayed from time to time.

For more information, visit the [PrestaScan Security GitHub repository](https://github.com/prestascan/prestascansecurity).

# Compatibility

As the security targets all kinds of merchants, using sometimes outdated versions of PrestaShop, we do our best for the moment to keep the module at least compatible with PrestaShop 1.5, 1.6, 1.7, and 8.

| PrestaShop version tested | Status | Comments |
| -------- | ------ | ------ |
| **8.X** (8.0.2) | OK | Stable
| **1.7.X** (1.7.8.8) | OK | Stable
| **1.6.1.X** (1.6.1.24) | OK | Stable
| **1.6.0.X** (1.6.0.9) | OK | Stable
| **1.5** | OK since 1.1.2 | Stable (but will not be actively maintained)
