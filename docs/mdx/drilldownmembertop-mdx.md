---
title: DrilldownMemberTop (MDX) | Documents Microsoft
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
- DRILLDOWNMEMBERTOP
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownMemberTop function
ms.assetid: b6575544-1fd3-4fa1-aa2e-272d307c7750
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 360b29ba0a3e041cf7fdc381251e34912a667461
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="drilldownmembertop-mdx"></a>DrilldownMemberTop (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Extrait vers le bas les membres dans un jeu spécifié qui sont présents dans un second jeu spécifié, ce qui limite l'ensemble de résultats à un nombre spécifique de membres. Sinon, cette fonction extrait vers le bas sur un jeu de tuples à l’aide de la première hiérarchie de tuple ou de la hiérarchie éventuellement spécifiée.  
  
## <a name="syntax"></a>Syntaxe  
  
```  
  
DrillDownMemberTop(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expression>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>Arguments  
 *Set_Expression1*  
 Une expression MDX (Multidimensional Expressions) valide qui retourne un jeu.  
  
 *Set_Expression2*  
 Une expression MDX (Multidimensional Expressions) valide qui retourne un jeu.  
  
 *Compter*  
 Expression numérique valide qui précise le nombre de tuples à retourner.  
  
 *Numeric_expression*  
 Expression numérique valide qui correspond généralement à une expression MDX (Multidimensional Expressions) des coordonnées des cellules qui retournent un nombre.  
  
 *Hiérarchie*  
 Expression MDX (Multidimensional Expressions) valide qui retourne une hiérarchie.  
  
 *Récursive*  
 Mot clé qui indique une comparaison récursive de jeux.  
  
 *Include_Calc_Members*  
 Mot clé permettant d'activer les membres calculés à inclure dans les résultats de l'extraction vers le bas.  
  
## <a name="remarks"></a>Notes  
 Si une expression numérique est spécifiée, la **DrilldownMemberTop** fonction trie, par ordre décroissant, les enfants de chaque membre dans le premier jeu selon la valeur de l’expression numérique, telle qu’évaluée sur le jeu de membres enfants. Si aucune expression numérique n'est spécifiée, cette fonction trie, par ordre décroissant, les enfants de chaque membre dans le premier jeu selon les valeurs des cellules représentées par le jeu des membres enfants, comme le détermine le contexte de la requête. Ce comportement est semblable aux fonctions TopCount et Head (MDX) qui retournent un jeu de membres dans l'ordre naturel, sans tri.  
  
 Après le tri, le **DrilldownMemberTop** fonction retourne un jeu qui contient les membres parents et le nombre de membres enfants spécifiés dans *Count,* avec la valeur la plus élevée et contenues dans les deux ensembles.  
  
 Si **récursive** est spécifié, la fonction trie le premier jeu comme décrit précédemment, puis compare de manière récursive les membres du premier jeu, organisées dans une hiérarchie, par rapport au deuxième jeu *.* La fonction récupère le premier nombre d’enfants pour chaque membre dans le premier jeu est également présent dans le deuxième jeu.  
  
 Le premier jeu peut contenir des tuples au lieu de membres. Descente de tuple est une extension de OLE DB et retourne un jeu de tuples au lieu de membres.  
  
 Le **DrilldownMemberTop** fonction est similaire à la [DrilldownMember](../mdx/drilldownmember-mdx.md) de fonctionner, mais au lieu d’inclure tous les enfants de chaque membre dans le premier jeu est également présent dans le deuxième jeu, le **DrilldownMemberTop** fonction retourne le premier nombre de membres enfants pour chaque membre.  
  
 Interrogez la propriété XMLA MdpropMdxDrillFunctions vous permet de vérifier le niveau de prise en charge par le serveur pour les fonctions d’extraction ; consultez [pris en charge les propriétés XMLA &#40;XMLA&#41; ](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md) pour plus d’informations.  
  
## <a name="example"></a>Exemple  
 L'exemple suivant effectue une extraction vers le bas dans la catégorie d'habillement pour retourner les trois sous-catégories de vêtements enregistrant le plus grand nombre de commandes expédiées.  
  
```  
SELECT DrilldownMemberTop   ({[Product].[Product Categories].[All Products],        
[Product].[Product Categories].[Category].Bikes,        
[Product].[Product Categories].[Category].Clothing},     
{[Product].[Product Categories].[Category].Clothing},     
3,     
[Measures].[Reseller Order Quantity])     
ON 0     
FROM [Adventure Works]     
WHERE [Measures].[Reseller Order Quantity]  
  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Référence des fonctions MDX & #40 ; MDX & #41 ;](../mdx/mdx-function-reference-mdx.md)  
  
  
