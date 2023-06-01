---
title: "[CVE-2023-30149] Mauvaise neutralisation de paramètres SQL dans le module City Autocomplete (cityautocomplete) d'ebewe.net pour PrestaShop"
categories: module
author:
- Profileo.com
- Friends-Of-Presta.org
meta: "CVE,PrestaShop,cityautocomplete"
severity: "critical (9.8)"
date: 2023-06-01T17:49:02+01:00
---

Vulnérabilité d'injection SQL dans le module City Autocomplete (cityautocomplete) d'ebewe.net pour PrestaShop, avant la version 1.8.12 (pour PrestaShop version 1.5/1.6) ou avant la 2.0.3 (pour PrestaShop version 1.7), permettant aux attaquants distants d'exécuter des commandes SQL arbitraires via le paramètre `type`, `input_name` ou `q` dans le contrôleur frontal autocompletion.php.

## Summary

* **CVE ID**: [CVE-2023-30149](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-30149)
* **Published at**: 2023-06-01
* **Advisory source**: Friends-Of-Presta
* **Vendor**: PrestaShop
* **Product**: cityautocomplete
* **Impacted release**: PS 1.5/1.6 : < 1.8.12 (corrigé sur la version 1.8.12), PS 1.7 : < 2.0.3 (corrigé sur la version 2.0.3)
* **Product author**: ebewe.net
* **Weakness**: [CWE-89](https://cwe.mitre.org/data/definitions/89.html)
* **Severity**: critical (9.8)

## Description

Une requête HTTP peut être manipulée à l'aide des paramètres GET `type` ou `q`, dans le point de terminaison du FrontController `/module/cityautocomplete/autocompletion`, permettant à un attaquant distant de réaliser une injection SQL. Le problème est résolu dans les versions 1.8.12 et 2.0.3, publiées en octobre 2022.

Note : La version 2.X inclut également un paramètre supplémentaire `input_name`. Voir le patch ci-dessous pour plus de détails.

**ATTENTION** : Cette exploitation est activement utilisée pour déployer des webskimmers afin de voler massivement des cartes de crédit.

Cette exploitation utilise un contrôleur frontal PrestaShop et la plupart des attaquants peuvent masquer le chemin du contrôleur de module lors de l'exploitation, de sorte que vous ne saurez jamais à partir de vos journaux de frontend conventionnels qu'elle exploite cette vulnérabilité. **Vous ne verrez que "POST /" dans vos journaux de frontend conventionnels**. L'activation d'AuditEngine de mod_security (ou similaire) est le seul moyen d'obtenir des données pour confirmer cette exploitation.

## CVSS base metrics

* **Attack vector**: network
* **Attack complexity**: low
* **Privilege required**: none
* **User interaction**: none
* **Scope**: unchanged
* **Confidentiality**: high
* **Integrity**: high
* **Availability**: high

**Vector string**: [CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator?vector=AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H)

## Possible malicious usage

* Obtain admin access
* Remove data on the associated PrestaShop
* Copy/paste data from sensitive tables to FRONT to exposed tokens and unlock admins's ajax scripts
* Rewrite SMTP settings to hijacked emails

## Proof of concept

```bash
https://example.test/module/cityautocomplete/autocompletion?q=39000&type=1;select(0x73656C65637420736C656570283432293B)INTO@a;prepare`b`from@a;execute`b`;--;&input_name=postcode&limit=10
```

## Patch 

**For versions > 2.0.0 and < 2.0.3**:
```diff
--- a/controllers/front/autocompletion.php
+++ b/controllers/front/autocompletion.php
@@ -43,13 +43,23 @@ class CityAutocompleteAutocompletionModuleFrontController extends ModuleFrontCon
             && Tools::getIsset('limit')) {
             $id_lang = Context::getContext()->language->id;
 
+            $type = Tools::getValue('type');
+            if (!in_array($type, array('postcode', 'city'))) {
+                die(Tools::jsonEncode(array()));
+            }
+
+            $inputName = Tools::getValue('input_name');
+            if (!in_array($inputName, array('postcode', 'city'))) {
+                die(Tools::jsonEncode(array()));
+            }
+
             $sql = 'SELECT ca.postcode, ca.city, ca.iso_code, c.id_country, cl.name,
-                "'.(string)Tools::getValue('input_name').'" as input_name
+                `'.bqSQL($inputName).'` as input_name
                 FROM `'._DB_PREFIX_.'cityautocomplete` ca
                 LEFT JOIN `'._DB_PREFIX_.'country` c ON (ca.iso_code = c.iso_code)
                 LEFT JOIN `'._DB_PREFIX_.'country_lang` cl ON (c.id_country = cl.id_country)
                 WHERE id_lang='.(int)$id_lang.'
-                AND '.(string)Tools::getValue('type').' LIKE "'.(string)Tools::getValue('q').'%"
+                AND `'.bqSQL($type).'` LIKE "'.pSQL(Tools::getValue('q')).'%"
                 LIMIT 0, '.(int)Tools::getValue('limit');
 
             $result = Db::getInstance()->ExecuteS($sql);
```

**For versions < 1.8.12**:
```diff
--- a/controllers/front/autocompletion.php
+++ b/controllers/front/autocompletion.php
@@ -39,13 +39,18 @@ class CityAutocompleteAutocompletionModuleFrontController extends ModuleFrontCon
     {
         parent::initContent();
         if (Tools::getIsset('q') && Tools::getIsset('type') && Tools::getIsset('limit')) {
+
+            $type = Tools::getValue('type');
+            if (!in_array($type, array('postcode', 'city'))) {
+                die(Tools::jsonEncode(array()));
+            }
+
             $id_lang = Context::getContext()->language->id;
             $sql = 'SELECT ca.postcode, ca.city, ca.iso_code, c.id_country, cl.name
                 FROM `'._DB_PREFIX_.'cityautocomplete` ca
                 LEFT JOIN `'._DB_PREFIX_.'country` c ON (ca.iso_code = c.iso_code)
                 LEFT JOIN `'._DB_PREFIX_.'country_lang` cl ON (c.id_country = cl.id_country)
                 WHERE id_lang='.(int)$id_lang.'
-                AND '.Tools::getValue('type').' LIKE "'.Tools::getValue('q').'%"
+                AND `'.bqSQL($type).'` LIKE "'.pSQL(Tools::getValue('q')).'%"
                 LIMIT 0, '.(int)Tools::getValue('limit');
             $result = Db::getInstance()->ExecuteS($sql);
             die(Tools::jsonEncode($result));
```

## Other recommandations

* Upgrade the module to the most recent version
* Upgrade PrestaShop to the latest version to disable multiquery executions (separated by “;”)
* Change the default database prefix `ps_` by a new longer arbitrary prefix. Nethertheless, be warned that this is useless against blackhat with DBA senior skilled because of a design vulnerability in DBMS
* Activate OWASP 942's rules on your WAF (Web application firewall), be warned that you will probably break your backoffice and you will need to pre-configure some bypasses against these set of rules.

## Timeline

| Date | Action |
| -- | -- |
| 2022-09-08 | Discovery of the vulnerability by Profileo |
| 2022-09-10 | Security issue reported to the author, using addons support platform |
| 2022-09-17 | Issue confirmed by the author |
| 2022-10-07 | Release of version 1.8.12 fixing the issue |
| 2023-03-25 | Request for additional details concerning impacted versions |
| 2023-04-02 | Update the patch to adapt to version 2.X |
| 2023-04-13 | Get additional details concerning impacted versions |
| 2023-06-01 | Publication of the security advisory |

## Links

* [Module City Autocomplete on addons](https://addons.prestashop.com/en/registration-ordering-process/6097-city-autocomplete.html)
* [National Vulnerability Database CVE-2023-30149](https://nvd.nist.gov/vuln/detail/CVE-2023-30149)
* [Publication Friends Of Presta](https://friends-of-presta.github.io/security-advisories/module/2023/06/01/cityautocomplete.html)
