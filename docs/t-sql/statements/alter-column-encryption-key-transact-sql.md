---
title: ALTER COLUMN ENCRYPTION KEY (Transact-SQL) | Documents Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 10/28/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER COLUMN ENCRYPTION
- ALTER_COLUMN_ENCRYPTION_TSQL
- ALTER COLUMN ENCRYPTION KEY
- ALTER_COLUMN_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- column encryption key, alter
- ALTER COLUMN ENCRYPTION KEY statement
ms.assetid: c79a220d-e178-4091-a330-c924cc0f0ae0
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6aaa1f85f860272cdb672d29bccdda39380f728a
ms.contentlocale: fr-fr
ms.lasthandoff: 09/01/2017

---
# <a name="alter-column-encryption-key-transact-sql"></a>ALTER COLUMN ENCRYPTION KEY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Modifie une clé de chiffrement de colonne dans une base de données, ajout ou suppression d’une valeur chiffrée. Une clé CEK peut avoir jusqu'à deux valeurs qui permet la rotation de la clé principale de colonne correspondante. Une clé CEK est utilisée lors du chiffrement des colonnes à l’aide de la [Always Encrypted &#40; moteur de base de données &#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md) fonctionnalité. Avant d’ajouter une valeur de clé, vous devez définir la clé principale de colonne qui a été utilisée pour chiffrer la valeur à l’aide de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [CREATE MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) instruction.  
  
 ![Icône de lien de rubrique](../../database-engine/configure-windows/media/topic-link.gif "Icône lien de rubrique") [Conventions de la syntaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntaxe  
  
```  
ALTER COLUMN ENCRYPTION KEY key_name   
    [ ADD | DROP ] VALUE   
    (  
        COLUMN_MASTER_KEY = column_master_key_name   
        [, ALGORITHM = 'algorithm_name' , ENCRYPTED_VALUE =  varbinary_literal ]   
    ) [;]  
```  
  
## <a name="arguments"></a>Arguments  
 *key_name*  
 La clé de chiffrement de colonne que vous modifiez.  
  
 *column_master_key_name*  
 Spécifie le nom de la clé principale de colonne (CMK) utilisée pour chiffrer la clé de chiffrement de colonne (CEK).  
  
 *algorithm_name*  
 Nom de l’algorithme de chiffrement utilisé pour chiffrer la valeur. L’algorithme pour les fournisseurs de système doit être **RSA_OAEP**. Cet argument n’est pas valide lors de la suppression d’une valeur de clé de chiffrement de colonne.  
  
 *varbinary_literal*  
 L’objet BLOB de clé CEK chiffrée avec le masque spécifié la clé de chiffrement. . Cet argument n’est pas valide lors de la suppression d’une valeur de clé de chiffrement de colonne.  
  
> [!WARNING]  
>  Passent jamais en texte clair des valeurs de clé CEK dans cette instruction. Cela comprend l’avantage de cette fonctionnalité.  
  
## <a name="remarks"></a>Notes  
 En règle générale, une clé de chiffrement de colonne est créée avec seulement une valeur chiffrée. Lorsqu’une clé principale de colonne doit être paysage (l’actuel colonne clé principale doit être remplacé par la nouvelle clé principale de colonne), vous pouvez ajouter une nouvelle valeur de la clé de chiffrement de colonne, chiffrées avec la nouvelle clé principale de colonne. Cela vous permettra de garantir les applications clientes peuvent accéder aux données chiffrées avec la clé de chiffrement de colonne, tandis que la nouvelle clé principale de colonne est rendue disponible pour les applications clientes. Un chiffrement intégral activée pilote dans une application cliente qui n’a pas accès à la nouvelle clé principale, sera en mesure d’utiliser la valeur clé de chiffrement de colonne chiffrée avec l’ancienne clé principale de colonne pour accéder aux données sensibles. Les algorithmes de chiffrement, prend en charge Always Encrypted, nécessitent la valeur de texte en clair pour que la longueur de 256 bits. Une valeur chiffrée doit être générée à l’aide d’un fournisseur de magasin de clés qui encapsule le magasin de clés contenant la clé principale de colonne.  
  
 Utilisez [sys.columns &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md), [sys.column_encryption_keys &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) et [sys.column_encryption_key_values &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md) pour afficher des informations sur les clés de chiffrement de colonne.  
  
## <a name="permissions"></a>Permissions  
 Requiert **ALTER ANY COLUMN ENCRYPTION KEY** autorisation sur la base de données.  
  
## <a name="examples"></a>Exemples  
  
### <a name="a-adding-a-column-encryption-key-value"></a>A. Ajout d’une valeur de clé de chiffrement de colonne  
 L’exemple suivant modifie une clé de chiffrement de colonne appelée `MyCEK`.  
  
```  
ALTER COLUMN ENCRYPTION KEY MyCEK  
ADD VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK2,   
    ALGORITHM = 'RSA_OAEP',   
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E00740075007300650072002F006D0079002F0064006500650063006200660034006100340031003000380034006200350033003200360066003200630062006200350030003600380065003900620061003000320030003600610037003800310066001DDA6134C3B73A90D349C8905782DD819B428162CF5B051639BA46EC69A7C8C8F81591A92C395711493B25DCBCCC57836E5B9F17A0713E840721D098F3F8E023ABCDFE2F6D8CC4339FC8F88630ED9EBADA5CA8EEAFA84164C1095B12AE161EABC1DF778C07F07D413AF1ED900F578FC00894BEE705EAC60F4A5090BBE09885D2EFE1C915F7B4C581D9CE3FDAB78ACF4829F85752E9FC985DEB8773889EE4A1945BD554724803A6F5DC0A2CD5EFE001ABED8D61E8449E4FAA9E4DD392DA8D292ECC6EB149E843E395CDE0F98D04940A28C4B05F747149B34A0BAEC04FFF3E304C84AF1FF81225E615B5F94E334378A0A888EF88F4E79F66CB377E3C21964AACB5049C08435FE84EEEF39D20A665C17E04898914A85B3DE23D56575EBC682D154F4F15C37723E04974DB370180A9A579BC84F6BC9B5E7C223E5CBEE721E57EE07EFDCC0A3257BBEBF9ADFFB00DBF7EF682EC1C4C47451438F90B4CF8DA709940F72CFDC91C6EB4E37B4ED7E2385B1FF71B28A1D2669FBEB18EA89F9D391D2FDDEA0ED362E6A591AC64EF4AE31CA8766C259ECB77D01A7F5C36B8418F91C1BEADDD4491C80F0016B66421B4B788C55127135DA2FA625FB7FD195FB40D90A6C67328602ECAF3EC4F5894BFD84A99EB4753BE0D22E0D4DE6A0ADFEDC80EB1B556749B4A8AD00E73B329C95827AB91C0256347E85E3C5FD6726D0E1FE82C925D3DF4A9  
);  
GO  
  
```  
  
### <a name="b-dropping-a-column-encryption-key-value"></a>B. Suppression d’une valeur de clé de chiffrement de colonne  
 L’exemple suivant modifie une clé de chiffrement de colonne appelée `MyCEK` en déposant une valeur.  
  
```  
ALTER COLUMN ENCRYPTION KEY MyCEK  
DROP VALUE  
(  
    COLUMN_MASTER_KEY = MyCMK  
);  
GO  
```  
  
## <a name="see-also"></a>Voir aussi  
 [CREATE COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY &#40; Transact-SQL &#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Always Encrypted &#40;moteur de base de données&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [sys.column_encryption_keys  &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_encryption_key_values &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)   
 [sys.columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)  
  
  
