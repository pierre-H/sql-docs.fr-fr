---
title: Élément Statement (XMLA) | Documents Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9acece21cf1542c8da8134fa0771ae37b836444f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/10/2018
---
# <a name="statement-element-xmla"></a>Élément Statement (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contient une requête ou une instruction à envoyer à l’aide de la **Execute** (méthode) à une instance de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
  
<Command>  
   <Statement>...</Statement>  
</Command>  
```  
  
## <a name="element-characteristics"></a>Caractéristiques de l'élément  
  
|Caractéristique|Description|  
|--------------------|-----------------|  
|Type de données et longueur|Chaîne|  
|Valeur par défaut|Aucune|  
|Cardinalité|0-n : élément facultatif pouvant apparaître plusieurs fois.|  
  
## <a name="element-relationships"></a>Relations entre les éléments  
  
|Relation|Élément|  
|------------------|-------------|  
|Éléments parents|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Éléments enfants|Aucune|  
  
## <a name="remarks"></a>Notes  
 Le **instruction** commande exécute une requête ou une instruction sur le [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instance. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] prend en charge les langages suivants :  
  
-   MDX (Multidimensional Expressions)  
  
-   DMX (Data Mining Extensions)  
  
-   Un sous-ensemble de SQL (Structured Query Language)  
  
## <a name="see-also"></a>Voir aussi  
 [Commandes & #40 ; XMLA & #41 ;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
