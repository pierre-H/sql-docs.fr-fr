---
title: DROP MASTER KEY (Transact-SQL) | Documents Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP MASTER KEY
- DROP_MASTER_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- removing Database Master Keys
- database master key [SQL Server], removing
- encryption [SQL Server], Database Master Key
- DROP MASTER KEY statement
- cryptography [SQL Server], Database Master Key
- dropping Database Master Keys
- deleting Database Master Keys
ms.assetid: 5ccef797-408f-4964-80da-965d8e1ccba7
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bf519ae4d69429338522a98805616352f3c57cf5
ms.contentlocale: fr-fr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-master-key-transact-sql"></a>DROP MASTER KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw_md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Permet de supprimer la clé principale de la base de données active.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
-- Syntax for SQL Server, Azure SQL Data Warehouse, Parallel Data Warehouse  
  
DROP MASTER KEY  
```  
  
## <a name="arguments"></a>Arguments  
 Cette instruction n'accepte aucun argument.  
  
## <a name="remarks"></a>Notes  
 La suppression échoue si une clé privée dans la base de données est protégée par la clé principale.  
  
## <a name="permissions"></a>Permissions  
 Requiert l'autorisation CONTROL sur la base de données.  
  
## <a name="examples"></a>Exemples  
 Dans l'exemple ci-dessous, la clé principale de la base de données `AdventureWorks2012` est supprimée.  
  
```  
USE AdventureWorks2012;  
DROP MASTER KEY;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Exemples : [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] et[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 L’exemple suivant supprime la clé principale.  
  
```  
USE master;  
DROP MASTER KEY;  
GO  
```  
  
## <a name="see-also"></a>Voir aussi  
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md)   
 [Ouvrez MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/open-master-key-transact-sql.md)   
 [CLOSE MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/close-master-key-transact-sql.md)   
 [BACKUP MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/backup-master-key-transact-sql.md)   
 [RESTORE MASTER KEY &#40; Transact-SQL &#41;](../../t-sql/statements/restore-master-key-transact-sql.md)   
 [ALTER MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)   
 [Hiérarchie de chiffrement](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

