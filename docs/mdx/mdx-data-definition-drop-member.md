---
title: Instruction DROP MEMBER (MDX) | Documents Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP
- Member
- DROP_MEMBER
- DROP MEMBER
dev_langs:
- kbMDX
helpviewer_keywords:
- deleting calculated members
- calculated members [MDX]
- DROP MEMBER statement
- dropping calculated members
- removing calculated members
ms.assetid: e9819976-a9ec-4c48-b0b5-3f6938e200f5
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: ec70f001a25719393c08a24dc0348b0092a0c3db
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="mdx-data-definition---drop-member"></a>Définition de données MDX - suppression de membre
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Supprime un membre calculé.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
DROP MEMBER   
   CURRENTCUBE | Cube_Name  
      .Member_Name   
               [,CURRENTCUBE | Cube_Name.Member_Name ...n]  
```  
  
## <a name="arguments"></a>Arguments  
 *Cube_Name*  
 Expression de chaîne valide qui précise le nom d'un cube.  
  
 *Member_Identifier*  
 Une expression de chaîne valide qui fournit un nom de membre ou une clé de membre.  
  
## <a name="see-also"></a>Voir aussi  
 [CRÉER une instruction MEMBER & #40 ; MDX & #41 ;](../mdx/mdx-data-definition-create-member.md)   
 [Instructions MDX de définition de données &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
