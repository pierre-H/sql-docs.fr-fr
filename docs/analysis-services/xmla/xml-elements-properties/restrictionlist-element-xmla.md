---
title: Élément RestrictionList (XMLA) | Documents Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 70c42fe34a3ca825087d4965269dda004ef3f886
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/10/2018
---
# <a name="restrictionlist-element-xmla"></a>Élément RestrictionList (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Contient une collection de colonnes et de valeurs de restriction utilisées par la méthode [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) .  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>Caractéristiques de l'élément  
  
|Caractéristique|Description|  
|--------------------|-----------------|  
|Type de données et longueur|Aucune|  
|Valeur par défaut|Aucune|  
|Cardinalité|0-1: élément facultatif qui peut apparaître une fois et une seule.|  
  
## <a name="element-relationships"></a>Relations entre les éléments  
  
|Relation|Élément|  
|------------------|-------------|  
|Éléments parents|[Restrictions](../../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
|Éléments enfants|Colonnes et valeurs de restriction (voir la section « Notes »).|  
  
## <a name="remarks"></a>Notes  
 L'élément **RestrictionList** contient une collection de colonnes de restriction sur lesquelles les données retournées par la méthode **Discover** peuvent être filtrées. Chaque colonne de restriction dans l'élément **RestrictionList** est définie par un élément XML distinct. La valeur de la colonne de restriction correspond aux données figurant dans l'élément XML et le nom de la colonne de restriction correspond au nom de l'élément XML.  
  
## <a name="see-also"></a>Voir aussi  
 [Propriétés & #40 ; XMLA & #41 ;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
