---
title: Liste des bogues corrigés | Documents Microsoft
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
caps.latest.revision: 69
author: v-makouz
ms.author: genemi
manager: kenvh
ms.workload: Active
ms.openlocfilehash: dc71f74ca8e81f370037b82e42fd78957e096775
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/05/2018
---
# <a name="list-of-bugs-fixed"></a>Liste des bogues corrigés

Cette page contient une liste des bogues corrigés dans chaque version, en commençant par [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17 du pilote ODBC pour [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-171-for-includessnoversionincludesssnoversionmdmd"></a>Correctifs de bogues dans le [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17.1 du pilote ODBC pour [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Fixe 1 seconde lors de l’appel SQLFreeHandle lorsque MARS est activé et l’attribut de connexion « Encrypt = yes »
- Fixe une panne de l’erreur 22003 dans SQLGetData lorsque la taille de la mémoire tampon passée est inférieure, les récupération de données (Windows)
- Fixe des messages d’erreur ADAL tronquée
- Correction d’un bogue rare sur Windows 32 bits lors de la conversion flottante point nombre en entier
- Ne correction d’un problème où serait de l’insertion de double dans un champ décimal avec Always Encrypted sur aucune erreur de troncation de données de retour
- Résolution d’un avertissement sur MacOS installer

### <a name="bug-fixes-in-the-includemsconameincludesmsconamemdmd-odbc-driver-17-for-includessnoversionincludesssnoversionmdmd"></a>Correctifs de bogues dans le [!INCLUDE[msCoName](../../includes/msconame_md.md)] 17 du pilote ODBC pour [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]

- Fixe l’envoi d’état incorrect à SQL Server pendant la tentative de récupération de la Session lors de la résilience des connexions et le regroupement de connexions à la fois sont activés, à l’origine de la session de suppression par le serveur
- Correction d’un bogue où lorsque vous utilisez l’authentification Kerberos, l’insertion en bloc peut échouer avec l’erreur « accès refusé »
- Solution de contournement supprimée d’un bogue unixODBC présente dans la version est inférieure à 2.3.1 (pilote a doublé les tailles de certaines mémoires tampon passé à unixODBC)
- Fixe la résilience des connexions (reconnexion) négatif lors de l’utilisation de ColumnEncryption = activé
- Fixe bogue de la création de source de données, où lorsque le « Authentification Interactive Active Directory » option Azure Authentication fenêtre peut devenir ne répond pas (Windows)
- Correction d’un incident rares lors de l’arrêt ODBC lors de l’exécution asynchrone est activée (s’est produite lors de l’effacement du handle de connexion)
- Correction d’un problème où le pilote SQL provoqué la consommation élevée de l’UC lors de l’exécution des procédures stockées de longue
- Incapacité fixe pour récupérer des données dans une colonne varbinary (max) chiffrées sans conversion
- Résolution d’un problème où après un varchar (max) null d’une colonne chiffrée est extraite à l’aide de SQLGetData() sur un curseur statique, la colonne suivante est également annulée même s’il possède des données
- Correction d’un problème avec l’extraction du champ varbinary (max) avec Always Encrypted sur
- Résolution d’un problème de setlocale() ne fonctionne ne pas avec le chiffrement intégral
- Résolution du problème de SQLDescribeParam() retour d’erreur lorsqu’elle est appelée sur le paramètre de procédure stockée de type XML avec Always Encrypted sur
- Fixes avec séquence d’échappement des traits de soulignement ne fonctionne ne pas dans SQLTables
- Correction d’un bogue dans lequel les données hébreu (varchar) sont tronquées lors de la retournées comme les caractères étendus sur Linux
- Correction d’un problème avec une requête codée Shift-JIS char/varchar à partir de l’application de UTF-8
- Les bogues résolus dans laquelle l’appelant SQLGetInfo avec le paramètre SQL_DRIVER_NAME retournée Linux-style de nom de fichier sur MacOS
- Correction d’un problème où le chargement des données de caractères Windows-1252, à l’aide d’entrée fichiers supérieur à 32k octets dans des colonnes VARCHAR à l’aide de l’utilitaire BCP entraînerait des erreurs