---
title: "GRANT-autorisations texte intégral (Transact-SQL) | Documents Microsoft"
ms.custom: 
ms.date: 06/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- granting permissions [SQL Server], full-text
- full-text search [SQL Server], permissions
- full-text catalogs [SQL Server], permissions
- full-text stoplist [SQL Server], permissions
- GRANT statement, full-text permissions
ms.assetid: fdb64e09-222a-47fe-b08b-999264ca261d
caps.latest.revision: 26
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 624b779b088008076360e12ed96c450fc3e91b50
ms.contentlocale: fr-fr
ms.lasthandoff: 09/01/2017

---
# <a name="grant-full-text-permissions-transact-sql"></a>GRANT - Autorisations relatives au texte intégral (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Accorde des autorisations sur un catalogue de texte intégral ou une liste de mots vides de texte intégral.  
  

  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
GRANT permission [ ,...n ] ON  
    FULLTEXT   
        {  
           CATALOG :: full-text_catalog_name  
           |  
           STOPLIST :: full-text_stoplist_name  
        }  
    TO database_principal [ ,...n ]  
    [ WITH GRANT OPTION ]  
    [ AS granting_principal ]  
```  
  
## <a name="arguments"></a>Arguments  
 *autorisation*  
 Nom d'une autorisation. Les mappages valides des autorisations des éléments sécurisables sont décrits dans la section « Notes », plus loin dans cette rubrique.  
  
 DANS le catalogue de texte intégral **::***intégral-text_catalog_name*  
 Indique le catalogue de texte intégral pour lequel l'autorisation est accordée. Le qualificateur d’étendue **::** est requis.  
  
 SUR FULLTEXT STOPLIST **::***intégral-text_stoplist_name*  
 Indique la liste de mots vides de texte intégral pour laquelle l'autorisation est accordée. Le qualificateur d’étendue **::** est requis.  
  
 *principal_base_de_données*  
 Spécifie le principal auquel l'autorisation est accordée. Il peut s'agir :  
  
-   d'un utilisateur de base de données ;  
-   d'un rôle de base de données ;  
-   d'un rôle d'application ;  
-   d'un utilisateur de base de données mappé sur une connexion Windows ;  
-   d'un utilisateur de base de données mappé sur un groupe Windows ;  
-   d'un utilisateur de base de données mappé sur un certificat ;  
-   d'un utilisateur de base de données mappé à une clé asymétrique ;  
-   d'un utilisateur de base de données qui n'est pas mappé sur le principal d'un serveur.  
  
GRANT OPTION  
 Indique que le principal a également la possibilité d'accorder l'autorisation spécifiée à d'autres principaux.  
  
En tant que *granting_principal*  
 Spécifie un principal dont le principal qui exécute cette requête dérive son droit d'accorder l'autorisation. Il peut s'agir :  
  
-   d'un utilisateur de base de données ;  
-   d'un rôle de base de données ;  
-   d'un rôle d'application ;  
-   d'un utilisateur de base de données mappé sur une connexion Windows ;  
-   d'un utilisateur de base de données mappé sur un groupe Windows ;  
-   d'un utilisateur de base de données mappé sur un certificat ;  
-   d'un utilisateur de base de données mappé à une clé asymétrique ;  
-   d'un utilisateur de base de données qui n'est pas mappé sur le principal d'un serveur.  
  
## <a name="remarks"></a>Notes  
  
## <a name="fulltext-catalog-permissions"></a>Autorisations FULLTEXT CATALOG  
 Un catalogue de texte intégral est un élément sécurisable au niveau base de données contenu dans la base de données parente dans la hiérarchie des autorisations. Les autorisations les plus spécifiques et limitées qu'il est possible d'accorder pour un catalogue de texte intégral sont répertoriées dans le tableau ci-dessous, avec les autorisations plus générales qui les incluent de manière implicite.  
  
|Autorisation pour un catalogue de texte intégral|Déduite d'une autorisation pour un catalogue de texte intégral|Impliquée par une autorisation de base de données|  
|-----------------------------------|----------------------------------------------|------------------------------------|  
|CONTROL|CONTROL|CONTROL|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|REFERENCES|CONTROL|REFERENCES|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="fulltext-stoplist-permissions"></a>Autorisations FULLTEXT STOPLIST  
 Une liste de mots vides de texte intégral est un élément sécurisable au niveau base de données contenu dans la base de données parente dans la hiérarchie des autorisations. Les autorisations les plus spécifiques et limitées qu'il est possible d'accorder pour une liste de mots vides de texte intégral sont répertoriées dans le tableau ci-dessous, avec les autorisations plus générales qui les incluent de manière implicite.  
  
|Autorisation pour une liste de mots vides de texte intégral|Impliquée par une autorisation pour une liste de mots vides de texte intégral|Impliquée par une autorisation de base de données|  
|------------------------------------|-----------------------------------------------|------------------------------------|  
|ALTER|CONTROL|ALTER ANY FULLTEXT CATALOG|  
|CONTROL|CONTROL|CONTROL|  
|REFERENCES|CONTROL|REFERENCES|  
|TAKE OWNERSHIP|CONTROL|CONTROL|  
|VIEW DEFINITION|CONTROL|VIEW DEFINITION|  
  
## <a name="permissions"></a>Permissions  
 Le fournisseur d'autorisations (ou le principal spécifié avec l'option AS) doit posséder l'autorisation elle-même avec l'option GRANT OPTION ou une autorisation plus élevée qui implique l'autorisation accordée.  
  
 En cas d'utilisation de l'option AS, ces critères s'appliquent.  
  
|En tant que *granting_principal*|Autres autorisations nécessaires|  
|------------------------------|------------------------------------|  
|Utilisateur de base de données|Autorisation IMPERSONATE sur l'utilisateur, appartenance au rôle de base de données fixe db_securityadmin, appartenance au rôle de base de données fixe db_owner ou appartenance au rôle serveur fixe sysadmin.|  
|Utilisateur de base de données mappé à une connexion Windows|Autorisation IMPERSONATE sur l'utilisateur, appartenance au rôle de base de données fixe db_securityadmin, appartenance au rôle de base de données fixe db_owner ou appartenance au rôle serveur fixe sysadmin.|  
|Utilisateur de base de données mappé à un groupe Windows|Appartenance au groupe Windows, appartenance aux rôles de base de données fixe db_securityadmin ou db_owner ou appartenance au rôle serveur fixe sysadmin.|  
|Utilisateur de base de données mappé à un certificat|Appartenance aux rôles de base de données fixe db_securityadmin ou db_owner ou appartenance au rôle serveur fixe sysadmin.|  
|Utilisateur de base de données mappé à une clé asymétrique|Appartenance aux rôles de base de données fixe db_securityadmin ou db_owner ou appartenance au rôle serveur fixe sysadmin.|  
|Utilisateur de base de données qui n'est mappé sur aucun principal d'un serveur|Autorisation IMPERSONATE sur l'utilisateur, appartenance au rôle de base de données fixe db_securityadmin, appartenance au rôle de base de données fixe db_owner ou appartenance au rôle serveur fixe sysadmin.|  
|Rôle de base de données|Autorisation ALTER sur le rôle, appartenance au rôle de base de données fixe db_securityadmin, appartenance au rôle de base de données fixe db_owner ou appartenance au rôle serveur fixe sysadmin.|  
|Rôle d'application|Autorisation ALTER sur le rôle, appartenance au rôle de base de données fixe db_securityadmin, appartenance au rôle de base de données fixe db_owner ou appartenance au rôle serveur fixe sysadmin.|  
  
 Les propriétaires d'objets peuvent accorder des autorisations sur les objets qu'ils possèdent. Les principaux ayant l'autorisation CONTROL sur un élément sécurisable peuvent accorder une autorisation sur cet élément.  
  
 Les détenteurs de l'autorisation CONTROL SERVER, tels que les membres du rôle serveur fixe sysadmin, peuvent accorder une autorisation sur n'importe quel élément sécurisable du serveur. Les bénéficiaires de l'autorisation CONTROL sur une base de données, tels que les membres du rôle de base de données fixe db_owner, peuvent accorder une autorisation quelconque sur tout élément sécurisable inclus dans la base de données. Les détenteurs de l'autorisation CONTROL sur un schéma peuvent accorder une autorisation sur n'importe quel objet dans ce schéma.  
  
## <a name="examples"></a>Exemples  
  
### <a name="a-granting-permissions-to-a-full-text-catalog"></a>A. Octroi d'autorisations à un catalogue de texte intégral  
 L'exemple suivant accorde à `Ted` l'autorisation `CONTROL` pour le catalogue de texte intégral `ProductCatalog`.  
  
```  
GRANT CONTROL  
    ON FULLTEXT CATALOG :: ProductCatalog  
    TO Ted ;  
```  
  
### <a name="b-granting-permissions-to-a-stoplist"></a>B. Octroi d'autorisations à une liste de mots vides  
 L'exemple suivant accorde à `Mary` l'autorisation `VIEW DEFINITION` pour la liste de mots vides de texte intégral `ProductStoplist`.  
  
```  
GRANT VIEW DEFINITION  
    ON FULLTEXT STOPLIST :: ProductStoplist  
    TO Mary ;  
```  
  
## <a name="see-also"></a>Voir aussi  
 [CRÉER un rôle d’APPLICATION &#40; Transact-SQL &#41;](../../t-sql/statements/create-application-role-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [CRÉER le catalogue de texte intégral &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md)   
 [CRÉER une liste de mots vides de texte intégral &#40; Transact-SQL &#41;](../../t-sql/statements/create-fulltext-stoplist-transact-sql.md)   
 [Hiérarchie de chiffrement](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [Sys.fn_my_permissions &#40; Transact-SQL &#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)   
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [HAS_PERMS_BY_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/has-perms-by-name-transact-sql.md)   
 [Autorisations &#40;moteur de base de données&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [Principaux &#40;moteur de base de données&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [Sys.fulltext_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [sys.fulltext_stoplists &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql.md)  
  
  
