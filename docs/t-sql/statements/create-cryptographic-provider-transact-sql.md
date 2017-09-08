---
title: "CRÉER le fournisseur de chiffrement (Transact-SQL) | Documents Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_CRYPTOGRAPHIC_TSQL
- CRYPTOGRAPHIC PROVIDER
- PROVIDER_TSQL
- CREATE CRYPTOGRAPHIC
- CREATE CRYPTOGRAPHIC PROVIDER
- CRYPTOGRAPHIC_PROVIDER_TSQL
- CREATE_CRYPTOGRAPHIC_PROVIDER_TSQL
- PROVIDER
dev_langs:
- TSQL
helpviewer_keywords:
- 33085 (Database Engine error)
- CREATE CRYPTOGRAPHIC PROVIDER statement
- 33032 (Database Engine error)
ms.assetid: 059a39a6-9d32-4d3f-965b-0a1ce75229c7
caps.latest.revision: 20
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a7252786522ef4e0b4206db06d7dc8aa76cf308
ms.contentlocale: fr-fr
ms.lasthandoff: 09/01/2017

---
# <a name="create-cryptographic-provider-transact-sql"></a>CREATE CRYPTOGRAPHIC PROVIDER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crée un fournisseur de services de chiffrement dans [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à partir d'un fournisseur EKM (Extensible Key Management).  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
CREATE CRYPTOGRAPHIC PROVIDER provider_name   
    FROM FILE = path_of_DLL  
```  
  
## <a name="arguments"></a>Arguments  
 *Nom_Fournisseur*  
 Nom du fournisseur EKM (Extensible Key Management)  
  
 *path_of_DLL*  
 Chemin d'accès du fichier .dll qui implémente l'interface [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] EKM. Lorsque vous utilisez la **connecteur SQL Server pour Microsoft Azure Key Vault** l’emplacement par défaut est **'C:\Program Files\Microsoft SQL Server Connector pour Microsoft Azure clé Vault\Microsoft.AzureKeyVaultService.EKM.dll'**.  
  
## <a name="remarks"></a>Notes  
 Toutes les clés créées par un fournisseur référenceront ce dernier par son GUID. Le GUID est conservé dans toutes les versions de la DLL.  
  
 La DLL qui implémente l'interface SQLEKM doit être signée numériquement à l'aide de n'importe quel certificat. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vérifiera la signature. Cela inclut sa chaîne de certificats, qui doit avoir sa racine installé sur le **autorités de certificat racine de confiance** emplacement sur un système Windows. Si la signature n’est pas vérifiée correctement, l’instruction CREATE CRYPTOGRAPHIC PROVIDER échoue. Pour plus d’informations sur les certificats et les chaînes de certificats, consultez [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md).  
  
 Lorsqu'une DLL de fournisseur EKM n'implémente pas toutes les méthodes nécessaires, CREATE CRYPTOGRAPHIC PROVIDER peut retourner l'erreur 33085 :  
  
 `One or more methods cannot be found in cryptographic provider library '%.*ls'.`  
  
 Lorsque le fichier d'en-tête utilisé pour créer la DLL de fournisseur EKM est obsolète, CREATE CRYPTOGRAPHIC PROVIDER peut retourner l'erreur 33032 :  
  
 `SQL Crypto API version '%02d.%02d' implemented by provider is not supported. Supported version is '%02d.%02d'.`  
  
## <a name="permissions"></a>Permissions  
 Requiert l’autorisation CONTROL SERVER ou l’appartenance à la **sysadmin** rôle serveur fixe.  
  
## <a name="examples"></a>Exemples  
 L’exemple suivant crée un fournisseur de services de chiffrement appelé `SecurityProvider` dans [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à partir d’un fichier .dll. Le fichier .dll est nommé `c:\SecurityProvider\SecurityProvider_v1.dll` et il est installé sur le serveur. Le certificat du fournisseur doit d'abord être installé sur le serveur.  
  
```  
-- Install the provider  
CREATE CRYPTOGRAPHIC PROVIDER SecurityProvider  
    FROM FILE = 'C:\SecurityProvider\SecurityProvider_v1.dll';  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Gestion de clés extensible &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [ALTER CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-cryptographic-provider-transact-sql.md)   
 [DROP CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/drop-cryptographic-provider-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [Gestion de clés extensible à l’aide d’Azure Key Vault &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)  
  
  