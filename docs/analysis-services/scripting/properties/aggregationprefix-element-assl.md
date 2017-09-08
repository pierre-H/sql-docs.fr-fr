---
title: "Élément AggregationPrefix (ASSL) | Documents Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- AggregationPrefix Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- AggregationPrefix
helpviewer_keywords:
- AggregationPrefix element
ms.assetid: 1581e0df-ae8e-41ce-9c92-f0f7cac487f2
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8ef1688e23bddf1136775474c93ae62a05bb97ab
ms.contentlocale: fr-fr
ms.lasthandoff: 09/01/2017

---
# <a name="aggregationprefix-element-assl"></a>Élément AggregationPrefix (ASSL)
  Définit le préfixe commun à utiliser pour les noms d'agrégation dans l'ensemble de l'élément parent associé.  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
  
<Cube> <!-- or Database, MeasureGroup, Partition -->  
   ...  
   <AggregationPrefix>...</AggregationPrefix>  
   ...  
</Database>  
```  
  
## <a name="element-characteristics"></a>Caractéristiques de l'élément  
  
|Caractéristique|Description|  
|--------------------|-----------------|  
|Type de données et longueur|Chaîne|  
|Valeur par défaut|Aucune|  
|Cardinalité|0-1: élément facultatif qui peut apparaître une fois et une seule.|  
  
## <a name="element-relationships"></a>Relations entre les éléments  
  
|Relation|Élément|  
|------------------|-------------|  
|Éléments parents|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md), [base de données](../../../analysis-services/scripting/objects/database-element-assl.md), [MeasureGroup](../../../analysis-services/scripting/objects/measuregroup-element-assl.md), [Partition](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|Éléments enfants|Aucune|  
  
## <a name="remarks"></a>Notes  
 Préfixes d’agrégation génèrent des noms d’agrégation dans [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]et également générer des noms de table dans la base de données relationnelle pour les agrégations stockées dans une partition ROLAP (OLAP) relationnel.  
  
 Un nom d'agrégation complètement développé se compose des parties suivantes :  
  
 *\<DatabasePrefix >\<CubePrefix >\<MeasureGroupPrefix >\<PartitionPrefix >\<AggregationID >*  
  
 Les quatre premières parties du nom d'agrégation forment le préfixe d'agrégation. L'utilisateur fournit les quatre premières parties :  
  
-   *DatabasePrefix* représente la valeur de la **AggregationPrefix** élément associé à un **base de données** élément.  
  
-   *CubePrefix* représente la valeur de la **AggregationPrefix** élément associé à un **Cube** élément.  
  
-   *MeasureGroupPrefix* représente la valeur de la **AggregationPrefix** élément associé à un **MeasureGroup** élément.  
  
-   *PartitionPrefix* représente la valeur de la **AggregationPrefix** élément associé à un **Partition** élément.  
  
 La cinquième partie du nom, *AggregationID*, est un identificateur défini par le système et les utilisateurs n’ont aucun contrôle sur cette partie du nom.  
  
 Les éléments qui correspondent aux parents de **AggregationPrefix** dans le modèle d’objet objets AMO (Analysis Management) sont <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.MeasureGroup>, et <xref:Microsoft.AnalysisServices.Partition>.  
  
## <a name="see-also"></a>Voir aussi  
 [Propriétés &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  