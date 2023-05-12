---
title: "PrestaScan Security"
categories: advisories
author:
- Profileo.com
meta: "PrestaShop,security,module,prestascan,scan,malware,virus,hack"
date: 2023-05-05T17:20:48+01:00
---

In the ever-evolving digital landscape, ensuring the security of your online store has become more critical than ever. As a company committed to protecting our customers from various threats, we developed **PrestaScan Security**, a powerful **PrestaShop module** designed to identify malware and known vulnerabilities in the PrestaShop core and its modules.

Thanks to the support of the Friends Of Presta association (FOP), we decided not only to **share this module to the entire PrestaShop community, but also to make it free**. PrestaScan Security is now a free and open-source module that provides all users with the best possible alert system for their online stores.  

The module is easy to install and use, keeping you updated on the latest security threats to your website.  

{{< image
src="/images/prestascansecurity/prestascansecurity-logo.png"
alt="PrestaScan Security Logo"
class="center-img head-img">}}

## Features

- Scan your modules to identify vulnerabilities and required updates
- Identify unused modules, with the ability to disable and remove modules in one place
- Be alerted when a new vulnerability is discovered in your module (email and back office notification)
- List known vulnerabilities in PrestaShop Core for your current version
- List unprotected directories

With even more features coming.

## User Guide

### How to install the module

1. [Download the latest version of the module from this link](https://security.prestascan.com/prestashop).
2. Log in to your PrestaShop back office.
3. Go to the "Modules" section.
4. Click on "Upload a module" and select the downloaded ZIP file.
5. Depending of your PrestaShop version, the module will be installed automatically or you will need to click the install button

### How to use the module

1. Once installed, go to the "Modules" section in your back office.
2. Find "PrestaScan Security" in the list of modules and click on "Configure."
3. Follow the instructions to register and run your first scan.

## FAQ

### How can I update the module?

When an update is available, a notification will be displayed in your back office.  

A button will allow you to update the module in one click.  

It's required to maintain the module up to date to continue being alerted to new vulnerabilities.

You may also check the latest change from [our GitHub repository](https://github.com/prestascan/prestascansecurity/releases).  

### How does the module handle vulnerability alerts?

When a vulnerability is discovered and publicly revealed or known to be exploited, a security notification is sent to all users that have done at least one scan of module vulnerabilities in the module. Be sure to run this scan at least once.

### Are there any paid plans or limitations?

The module will always remain free. However, we may introduce paid plans in the future to unlock specific features such as automated scans and reduce some limitations (e.g., the number of scans that can be performed within a specific timeframe). No paid plans are defined yet, but ads from partners might be displayed from time to time.

For more information, visit the [PrestaScan Security GitHub repository](https://github.com/prestascan/prestascansecurity).

### Compatibility

As the security targets all kinds of merchants, using sometimes outdated versions of PrestaShop, we do our best for the moment to keep the module at least compatible with PrestaShop 1.6, 1.7, and 8. Additional work is required to support PS 1.5.

| PrestaShop version tested | Status | Comments |
| -------- | ------ | ------ |
| **8.X** (8.0.2) | OK | Stable
| **1.7.X** (1.7.8.8) | OK | Stable
| **1.6.1.X** (1.6.1.24) | OK | Stable
| **1.6.0.X** (1.6.0.9) | OK | Stable
| **1.5** | In progress (expected in 1.1.2)  | Not supported as of now due to JS issues

### Main contributors

This module is fueled by the collective energy of the members of the Friends Of Presta security cell. Here is the list of the most significant contributors in terms of security research, publication of CVE, or development:

{{< inline_images_prestascansecurity
class="center-img head-img">}}
