---
title: "[CVE-2023-27569]-[CVE-2023-27570] Neutralisation incorrecte des paramètres SQL dans Profileo : module Tracking et Conversions (eo_tags) pour PrestaShop"
short_title: "CVE-2023-27569 - CVE-2023-27570"
categories: module
author:
- Profileo.com
- TouchWeb.fr
- Friends-Of-Presta.org
meta: "CVE,PrestaShop,module,eo_tags"
severity: "critical (9.8)"
date: 2023-03-15T15:24:08+01:00
---

Dans le module Tracking et Conversions (eo_tags) avant la version 1.4.19, un utilisateur anonyme peut effectuer une attaque d'injection SQL.

## Résumé

* **ID CVE**: [CVE-2023-27569](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-27569), [CVE-2023-27570](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2023-27570)
* **Publié le**: 2023-03-15
* **Source de l'avis**: security.profileo.com
* **Plateforme**: PrestaShop
* **Produit**: eo_tags
* **Version impactée**: >= 1.2.0, < 1.4.19 (la vulnérabilité est corrigée dans la version 1.4.19)
* **Auteur du produit**: Profileo
* **Faiblesse**: [CWE-89](https://cwe.mitre.org/data/definitions/89.html)
* **Sévérité**: critique (9.8)

## Description

De la version 1.2.0 publiée le 17 novembre 2017 à la version 1.4.18 publiée le 21 février 2023 (corrigée dans la version 1.4.19, publiée le 28 février 2023), une requête HTTP peut être forgée avec un cookie `_ga` compromis afin d'exploiter un paramètre non sécurisé dans les fonctions `saveGanalyticsCookie()` et `gaParseCookie()`, pouvant conduire à une injection SQL.

De la version 1.2.0 publiée le 17 novembre 2017 à la version 1.2.19 publiée le 22 octobre 2019 (corrigée dans la version 1.3.0), une requête HTTP peut être forgée avec un User-Agent ou un Referer compromis afin d'exploiter des paramètres non sécurisés dans la fonction `trackReferrer()`, pouvant conduire à une injection SQL. À partir de la version 1.2.1, le code a été migré vers classes/EoTagsStats.php (`EoTagsStats::setNewGuest()`) et la vulnérabilité nécessite désormais des privilèges (PR) et une interaction utilisateur (UI) pour être exploitée, réduisant la sévérité à 8.0.

Cette exploitation utilise des cookies (et des referers) pour effectuer l'attaque, donc le nom du module sera caché pendant l'exploitation, vous ne pourrez donc pas identifier cette vulnérabilité dans vos logs frontend conventionnels. **Vous ne verrez que "GET /" ou "POST /" dans vos logs frontend conventionnels.** Le referer compromis sera visible dans vos logs d'accès, mais vous ne pourrez pas voir le cookie compromis.

## Métriques de base CVSS

* **Vecteur d'attaque**: réseau
* **Complexité de l'attaque**: faible
* **Privilèges requis**: aucun
* **Interaction de l'utilisateur**: aucune
* **Portée**: inchangée
* **Confidentialité**: haute
* **Intégrité**: haute
* **Disponibilité**: haute

**Chaîne de vecteur**: [CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H](https://nvd.nist.gov/vuln-metrics/cvss/v3-calculator?vector=AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H)

## Utilisation malveillante possible

* Obtenir un accès administrateur
* Fuites de données techniques et personnelles

## Correctif

Si présent dans `eo_tags.php`

```diff
--- a/eo_tags.php
+++ b/eo_tags.php
@@ -1495,8 +1495,8 @@ class Eo_Tags extends Module
                 $old_cid = $this->getAnalyticsCID($this->context->cart->id);
                 $data = array(
                     'id_cart' => $this->context->cart->id,
-                    'cid'     => $cid,
-                    'cookie'  => serialize($_COOKIE['_ga']),
+                    'cid'     => pSQL($cid),
+                    'cookie'  => pSQL(serialize($_COOKIE['_ga'])),
                 );
                 if (!$old_cid) {
                     Db::getInstance()->insert('eo_tags_ga_cookie', $data);
```

```diff
--- a/eo_tags.php
+++ b/eo_tags.php
@@ -1356,11 +1356,11 @@ class Eo_Tags extends Module
                 ';
                 if ($referral = Db::getInstance()->getRow($sql2)) {
                     $data = array(
-                        'id_guest'     => $cookie->id_guest,
+                        'id_guest'     => (int)$cookie->id_guest,
                         'ip_address'   => $referral['ip_address'],
-                        'http_referer' => $referral['http_referer'],
-                        'request_uri'  => $referral['request_uri'],
-                        'user_agent'   => $user_agent,
+                        'http_referer' => pSQL($referral['http_referer']),
+                        'request_uri'  => pSQL($referral['request_uri']),
+                        'user_agent'   => pSQL($user_agent),
                         'date_add'     => $referral['date_add'],
                     );
                 }
@@ -1397,11 +1397,11 @@ class Eo_Tags extends Module
             $request_uri = substr($request_uri, 0, 255);
 
             $data = array(
-                'id_guest'     => $cookie->id_guest,
+                'id_guest'     => (int)$cookie->id_guest,
                 'ip_address'   => $ip_address,
-                'http_referer' => $http_referer,
-                'request_uri'  => $request_uri,
-                'user_agent'   => $user_agent,
+                'http_referer' => pSQL($http_referer),
+                'request_uri'  => pSQL($request_uri),
+                'user_agent'   => pSQL($user_agent),
                 'date_add'     => date('Y-m-d H:i:s'),
             );
         }
```

Si présent dans `classes/EoTagsStats.php` `EoTagsStats::setNewGuest()`
```diff
--- a/classes/EoTagsStats.php
+++ b/classes/EoTagsStats.php
@@ -26,7 +26,7 @@ class EoTagsStats {
         $data = array(
             'id_customer' => $id_customer,
             'ip_address'  => $ip_address,
-            'user_agent'  => $user_agent,
+            'user_agent'  => pSQL($user_agent),
             'date_add'    => date('Y-m-d H:i:s'),
         );
```

Profileo remercie TouchWeb.fr pour son aide pour la découverte et l'analyse de la vulnérabilité.
N'hésitez pas à contacter security/at/profileo.com si vous souhaitez recevoir un script PHP pour détecter et corriger automatiquement cette vulnérabilité sur votre site web.

## Autres recommandations

* Mettez à jour PrestaShop vers la dernière version pour désactiver les exécutions de multi-requêtes (séparées par “;”) - sachez que cette fonctionnalité **NE** protégera **PAS** votre BOUTIQUE contre l'injection SQL qui utilise la clause UNION pour voler des données.
* Changez le préfixe de base de données par défaut ps_ par un nouveau préfixe arbitraire plus long. Néanmoins, sachez que cela est inutile contre les blackhats avec des compétences DBA senior en raison d'une vulnérabilité de conception dans DBMS.
* Activez les règles OWASP 942 sur votre WAF (pare-feu d'application Web), sachez que vous risquez probablement de casser votre backoffice et que vous devrez pré-configurer certains contournements pour ces règles.

## Chronologie

| Date       | Action                                                  |
|------------|---------------------------------------------------------|
| 2023-02-24 | Vulnérabilité découverte par TouchWeb.fr               |
| 2023-02-25 | Vulnérabilité confirmée par Profileo.com                  |
| 2023-02-28 | Correctif créé par Profileo et sortie de la version 1.4.19 résolvant le problème |
| 2023-03-01 | Correctif distribué aux clients                         |
| 2023-03-15 | Publication sur security.profileo.com                   |

## Liens

* [Profileo.com](https://www.profileo.com/fr/)
* [TouchWeb.fr](https://www.touchweb.fr/)
* [Base de Données Nationale sur les Vulnérabilités - CVE-2023-27569](https://nvd.nist.gov/vuln/detail/CVE-2023-27569)
* [Base de Données Nationale sur les Vulnérabilités - CVE-2023-27570](https://nvd.nist.gov/vuln/detail/CVE-2023-27570)
