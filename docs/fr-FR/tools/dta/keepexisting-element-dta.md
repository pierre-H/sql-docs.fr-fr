---
title: Keepexisting, élément (DTA) | Documents Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b426c32b4573ed0b30ae4180b3b782de9f553dae
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/26/2018
---
# <a name="keepexisting-element-dta"></a>KeepExisting, élément (Assistant Paramétrage de base de données)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Spécifie les structures PDS (index, vues indexées ou partitions) que l'Assistant Paramétrage du moteur de base de données doit conserver lors de la génération de sa recommandation.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <KeepExisting>...</KeepExisting>  
```  
  
## <a name="element-characteristics"></a>Caractéristiques de l'élément  
  
|Caractéristique|Description|  
|--------------------|-----------------|  
|**Type de données et longueur**|**string**, limite de longueur appliquée par le serveur.|  
|**Valeurs autorisées**|**NONE**<br /> Aucune structure existante.<br /><br /> **ALL**<br /> Toutes les structures existantes.<br /><br /> **ALIGNED**<br /> Toutes les structures alignées sur les partitions.<br /><br /> **CL_IDX**<br /> Tous les index cluster sur les tables.<br /><br /> **IDX**<br /> Tous les index cluster et non cluster sur les tables.<br /><br /> Utilisez une seule de ces valeurs avec cet élément.|  
|**Valeur par défaut**|Aucun.|  
|**Occurrence**|Facultatif. Ne peut être utilisé qu'une seule fois pour chaque élément **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relations entre les éléments  
  
|Relation|Éléments|  
|------------------|--------------|  
|**Élément parent**|[Élément TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Éléments enfants**|Aucun.|  
  
## <a name="example"></a> Exemple  
 Pour obtenir un exemple d’utilisation de cet élément, consultez [Exemple de fichier d’entrée XML simple &#40;Assistant Paramétrage de base de données&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a> Voir aussi  
 [Référence des fichiers d’entrée XML &#40;Assistant Paramétrage du moteur de base de données&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
