---
title: "PrestaScan Security"
categories: avis
author:
- Profileo.com
meta: "PrestaShop,sécurité,module,prestascan,scan,logiciel malveillant,virus,piratage"
date: 2023-05-05T17:20:48+01:00
---

{{< image
src="/images/prestascansecurity/dashboard-fr.png"
alt="PrestaScan Dashboard"
class="center-img head-img">}}

Dans un paysage numérique en constante évolution, assurer la sécurité de votre boutique en ligne est devenu plus crucial que jamais. En tant qu'entreprise engagée à protéger nos clients contre diverses menaces, nous avons développé **PrestaScan Security**, un puissant **module PrestaShop** conçu pour identifier les logiciels malveillants et les vulnérabilités connues dans le noyau PrestaShop et ses modules.

Grâce au soutien de l'association Friends Of Presta (FOP), nous avons décidé non seulement de **partager ce module avec l'ensemble de la communauté PrestaShop, mais aussi de le rendre gratuit**. PrestaScan Security est désormais un module gratuit et open source qui offre à tous les utilisateurs le meilleur système d'alerte possible pour leurs boutiques en ligne.

Le module est facile à installer et à utiliser, vous permettant de rester informé des dernières menaces de sécurité pour votre site Web.

## Sommaire

- [Contributeurs principaux](#contributeurs-principaux)
- [Fonctionnalités](#fonctionnalités)
  - [Modules à risque](#modules-à-risque)
  - [Modules inutilisés](#modules-inutilisés)
  - [Vulnérabilités du cœur de PrestaShop](#vulnérabilités-du-cœur-de-prestashop)
- [Guide de l'utilisateur](#guide-de-lutilisateur)
  - [Comment installer le module](#comment-installer-le-module)
  - [Comment utiliser le module](#comment-utiliser-le-module)
- [FAQ](#faq)
- [Compatibilité](#compatibilité)

## Contributeurs principaux

Ce module est alimenté par l'énergie collective des membres de la cellule sécurité de Friends Of Presta. Voici la liste des contributeurs les plus significatifs, que ce soit en termes de recherche, de publication ou de développement :

{{< inline_images_prestascansecurity
class="center-img head-img">}}

## Fonctionnalités

- Scannez vos modules pour identifier les vulnérabilités et les mises à jour nécessaires
- Identifiez les modules inutilisés, avec la possibilité de désactiver et de supprimer les modules en un seul endroit
- Soyez alerté lorsqu'une nouvelle vulnérabilité est découverte dans votre module (notification par e-mail et back office)
- Liste des vulnérabilités connues dans le noyau PrestaShop pour votre version actuelle
- Liste des répertoires non protégés

Et encore plus de fonctionnalités à venir.

### Modules à risque

Ce scan listera les modules à risque. Cela comprend les modules vulnérables et les modules nécessitant des mises à jour.

{{< image
src="/images/prestascansecurity/at-risk-modules-fr.png"
alt="Capture d'écran des modules à risque"
class="center-img head-img">}}

Lorsqu'un module est vulnérable dans sa version actuelle, il sera affiché dans la liste avec une étiquette de couleur indiquant le niveau de risque (rouge = critique, jaune = moyen, vert = faible). Le nombre sur l'étiquette indique le nombre de vulnérabilités détectées dans le module pour votre version. Vous pouvez cliquer sur la flèche à côté de la liste des modules pour obtenir les détails :

{{< image
src="/images/prestascansecurity/module-vulnerability-detail-fr.png"
alt="Capture d'écran des détails de la vulnérabilité du module"
class="center-img head-img">}}

### Modules inutilisés

Ce scan fournit une liste de tous les modules désactivés et désinstallés dans votre boutique. Vous pouvez également désinstaller et supprimer un module directement à partir de cette liste (assurez-vous cependant de confirmer l'action d'abord avec votre agence/ développeur web).

{{< image
src="/images/prestascansecurity/unused-modules-fr.png"
alt="Capture d'écran des modules inutilisés"
class="center-img head-img">}}

### Vulnérabilités du cœur de PrestaShop

Ce scan répertorie toutes les vulnérabilités du cœur de PrestaShop pour votre version actuelle de PrestaShop.

{{< image
src="/images/prestascansecurity/prestashop-cve-fr.png"
alt="Capture d'écran des vulnérabilités du cœur de PrestaShop"
class="center-img head-img">}}


## Guide de l'utilisateur

{{< image
src="/images/prestascansecurity/prestascansecurity-logo.png"
alt="Logo PrestaScan Security"
class="center-img head-img">}}

### Comment installer le module

1. [Téléchargez la dernière version du module à partir de ce lien](https://security.prestascan.com/prestashop).
2. Connectez-vous à votre back office PrestaShop.
3. Allez dans la section "Modules".
4. Cliquez sur "Ajouter un module" et sélectionnez le fichier ZIP téléchargé.
5. Selon votre version de PrestaShop, le module sera installé automatiquement ou vous devrez cliquer sur le bouton d'installation.

### Comment utiliser le module

1. Une fois installé, allez dans la section "Modules" de votre back office.
2. Trouvez "PrestaScan Security" dans la liste des modules et cliquez sur "Configurer".
3. Suivez les instructions pour vous inscrire et effectuer votre premier scan.

## FAQ

### Comment puis-je mettre à jour le module?

Lorsqu'une mise à jour est disponible, une notification sera affichée dans votre back office.

Un bouton vous permettra de mettre à jour le module en un clic.

Il est nécessaire de maintenir le module à jour pour continuer à être alerté des nouvelles vulnérabilités.

Vous pouvez également consulter les derniers changements sur [notre dépôt GitHub](https://github.com/prestascan/prestascansecurity/releases).

### Comment le module gère-t-il les alertes de vulnérabilité?

Lorsqu'une vulnérabilité est découverte et publiquement révélée ou connue pour être exploitée, une notification de sécurité est envoyée à tous les utilisateurs qui ont effectué au moins un scan de vulnérabilités de module dans le module. Assurez-vous d'effectuer ce scan au moins une fois.

### J'ai un message d'erreur lors de la création de mon compte, que puis-je faire ?

Les messages d'erreur lors de la création de compte sont affichés directement dans le formulaire. La plupart du temps, le problème est lié au site web auquel vous essayez de vous connecter, qui bloque notre serveur de scan. Le module ne fonctionnera pas avec des sites qui ne sont pas accessibles publiquement (comme les environnements de développement ou les sites en maintenance).

Il se peut également que vous essayiez de créer un second compte avec la même adresse e-mail. Actuellement, le système ne permet qu'une seule adresse e-mail et un seul site peut être lié à cette adresse e-mail. Vous pouvez, pour le moment, contourner cette restriction en créant un alias de votre e-mail (tel que monemail+alias@testcompany.test).

### Je n'ai pas reçu l'e-mail de vérification pour valider mon e-mail, que puis-je faire ?

Lors de l'inscription, nous nous assurons que votre e-mail est valide car vous recevrez ultérieurement des alertes de sécurité dessus. Si vous n'avez pas reçu l'e-mail de vérification, veuillez vérifier votre dossier SPAM. Si vous ne trouvez pas l'e-mail dans le SPAM, essayez de renvoyer l'e-mail de vérification à partir du bouton vert dédié.

Si vous n'avez toujours pas reçu l'e-mail, assurez-vous d'avoir entré une adresse e-mail valide. Vous pouvez vérifier votre profil [à partir de ce lien](https://security.prestascan.com/user/profile):
{{< image
src="/images/prestascansecurity/registration-edit-profile.png"
alt="Capture d'écran de la modification du profil d'inscription PrestaScan Security"
class="center-img head-img">}}

### J'ai pu m'inscrire mais je ne peux pas terminer la configuration ou démarrer un scan à cause d'une erreur de token ou de connectivité, que puis-je faire ?

Si vous rencontrez des erreurs lors de la finalisation de la configuration, veuillez suivre les étapes suivantes :
1. Supprimez votre compte PrestaScan.
Vous pouvez le faire à partir de [votre profil utilisateur](https://security.prestascan.com/user/profile):
{{< image
src="/images/prestascansecurity/delete-account.png"
alt="Capture d'écran de la suppression du compte PrestaScan Security"
class="center-img head-img">}}

2. Déconnectez le compte dans le module (dans le coin supérieur droit, cliquez sur "déconnexion")

3. Vérifiez si vous utilisez la dernière version du module, et réinitialisez le module (ou désinstallez-le et réinstallez-le), cela supprimera toutes les données/sessions existantes.

4. Répétez le processus d'inscription.

Si le problème persiste, contactez notre support.

### Le scan semble ne jamais se terminer, quel est le problème ?

Si vous voyez que le scan est en cours et ne se termine pas après un certain temps (typiquement plus de 5~10 minutes), il pourrait y avoir un problème de communication (votre serveur n'est plus accessible par notre serveur) ou un autre problème lors du scan.

{{< image
src="/images/prestascansecurity/scan-in-progress-en.png"
alt="Capture d'écran du scan en cours PrestaScan Security"
class="center-img head-img">}}

Tout d'abord, notez que le module détectera les scans qui sont bloqués et affichera une option pour forcer la récupération du résultat du scan.

Si vous avez toujours le scan en cours après avoir réessayé, pensez à vérifier les journaux de votre serveur pour vérifier si la notification (webhook) est reçue. Vous pouvez contacter notre support pour plus de détails.

### Y a-t-il des plans payants ou des limitations?

Le module restera toujours gratuit. Cependant, nous pourrions introduire des plans payants à l'avenir pour débloquer des fonctionnalités spécifiques telles que les scans automatisés et réduire certaines limitations (par exemple, le nombre de scans pouvant être effectués dans un laps de temps spécifique). Aucun plan payant n'est défini pour le moment, mais des publicités de partenaires pourraient être affichées de temps en temps.

Pour plus d'informations, visitez le [dépôt GitHub PrestaScan Security](https://github.com/prestascan/prestascansecurity).

## Compatibilité

Comme la sécurité cible tous les types de commerçants, utilisant parfois des versions obsolètes de PrestaShop, nous faisons de notre mieux pour le moment pour maintenir le module au moins compatible avec PrestaShop 1.5, 1.6, 1.7 et 8.

| Versions PrestaShop testées | Statut | Commentaires |
| -------- | ------ | ------ |
| **8.X** (8.0.2) | OK | Stable
| **1.7.X** (1.7.8.8) | OK | Stable
| **1.6.1.X** (1.6.1.24) | OK | Stable
| **1.6.0.X** (1.6.0.9) | OK | Stable
| **1.5** | OK depuis 1.1.2 | Stable (Mais ne sera pas maintenu de façon actif)
