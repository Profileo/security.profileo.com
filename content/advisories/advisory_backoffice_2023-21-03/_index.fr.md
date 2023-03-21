---
title: "Recrudescence des piratages via les comptes BackOffice"
categories: advisories
author:
- Profileo.com
meta: "PrestaShop,backoffice,sécurité,2FA,employés"
date: 2023-03-21T15:49:24+01:00
---

## Introduction

Nous avons récemment constaté une **augmentation significative des piratages de boutiques PrestaShop**, exploitant des comptes BackOffice compromis suite au vol d'identifiants. En fin d'année 2022, Profileo avait déjà alerté sur cette problématique et recommandé de changer les mots de passe des BackOffice. Malheureusement, nous observons encore des vagues d'intrusions utilisant la même méthodologie.

### Comment les pirates récupèrent les identifiants

Les pirates utilisent diverses techniques pour récupérer les identifiants, notamment :

- **Phishing** : Envoi de faux emails ou messages incitant les destinataires à fournir leurs identifiants sur des sites frauduleux ressemblant à des sites légitimes.
- **Malware** : Logiciels malveillants capables de voler des identifiants stockés sur l'ordinateur de la victime ou d'enregistrer les frappes au clavier pour récupérer les mots de passe.

Ces identifiants sont parfois vendus sur le darknet, permettant à d'autres cybercriminels de les exploiter. Un seul employé compromis peut compromettre l'ensemble de la boutique.

### Conséquences d'un accès au BackOffice

L'accès au BackOffice permet aux pirates d'avoir un contrôle total de la boutique et d'infecter en profondeur le site. Ils peuvent ainsi détourner des transactions, voler des données sensibles et propager d'autres malwares.

## Mesures de sécurité à adopter

### Activez la double authentification (2FA) pour le BackOffice

La mise en place d'une **double authentification (2FA)** est la protection la plus efficace pour sécuriser l'accès à votre BackOffice. Cette méthode ajoute une étape supplémentaire lors de la connexion en demandant un code unique généré par une application d'authentification. Plusieurs modules PrestaShop permettent d'activer cette fonctionnalité.

A titre de référence, voici quelques exemples de modules offrant cette fonctionnalité :
- https://addons.prestashop.com/fr/securite-access/44413-security-pro-all-in-one.html
- https://addons.prestashop.com/fr/securite-access/5831-google-authenticator-two-factor-back-office-security.html
- https://addons.prestashop.com/fr/securite-access/49781-google-two-factor-authenticator-for-back-office.html
- https://addons.prestashop.com/fr/outils-administration/89758-two-factor-authentication-2fa-google-microsoft-token.html
- https://addons.prestashop.com/fr/securite-access/86502-securite-pare-feu-waf-2fa-teneur-protection.html
- https://addons.prestashop.com/fr/securite-access/88502-back-office-security-and-two-factor-authentication-2fa.html

### Changez l'URL du BackOffice

Pour renforcer la sécurité de votre boutique, il est conseillé de changer l'URL du BackOffice. Choisissez une URL unique et difficile à deviner, en combinant des lettres et des chiffres. Pour modifier l'URL, accédez au FTP de votre site et renommez le dossier du BackOffice existant.

### Déconnectez les sessions employées existantes

Après avoir activé la 2FA et changé l'URL du BackOffice, il est essentiel de déconnecter les sessions employées existantes pour rendre ces changements efficaces. En effet, la session (cookie) reste active même si on change l'URL du BO et on active le 2FA. Pour forcer la déconnexion des employés, modifiez le nom du cookie `psAdmin` en créant une surcharge de la classe Cookie.

Voici un exemple de surcharge de Cookie :

```php
<?php

class Cookie extends CookieCore
{
    public function __construct($name, $path = '', $expire = null, $shared_urls = null, $standalone = false, $secure = false)
    {
        // If the cookie name is `psAdmin`, add a suffix
        if ($name == 'psAdmin') {
            $name .= "1"; // To improve the security, the suffix can also be random
        }

        parent::__construct($name, $path , $expire , $shared_urls, $standalone, $secure);
    }
}
```

N'oubliez pas également de supprimer le fichier class_index pour que la surcharge soit prise en compte.

### Bonnes pratiques à adopter

Outre la 2FA, le changement d'URL du BackOffice et la déconnexion des sessions employées, nous vous conseillons d'adopter les bonnes pratiques suivantes :

- Utilisez des mots de passe complexes et uniques pour chaque compte administrateur
- Changez régulièrement les mots de passe
- Ne partagez pas vos identifiants avec des tiers

N'hésitez pas à [contacter notre équipe](https://www.profileo.com/fr/contactez-nous) si vous souhaitez que nous effectuions ces actions sur votre boutique.
