---
title: Curseur et les caractéristiques de verrou | Documents Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- locks [ADO], characteristics
- adOpenDynamic [ADO]
- cursors [ADO], characteristics
ms.assetid: 459c29cb-4230-42bf-8cc2-f3132ccc7aba
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 494532b71b708f59c4ba3e09960b977cecec7c16
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="cursor-and-lock-characteristics"></a>Curseur et les caractéristiques de verrou
Alors que les caractéristiques d’un curseur dépendent des fonctionnalités du fournisseur, les avantages et inconvénients suivants s’appliquent généralement aux différents types de curseurs et des verrous.  
  
|Type de curseur ou de verrou|Avantages|Inconvénients|  
|-------------------------|----------------|-------------------|  
|**adOpenForwardOnly**|-Besoins en ressources faible|-Impossible de faire défiler vers l’arrière<br />-Aucun accès concurrentiel aux données|  
|**adOpenStatic**|-Permettant le défilement|-Aucun accès concurrentiel aux données|  
|**adOpenKeyset**|-Certains accès concurrentiel aux données<br />-Permettant le défilement|-Besoins en ressources supérieur<br />-N’est pas disponible dans un scénario déconnecté|  
|**adOpenDynamic**|-Accès concurrentiel aux données élevé<br />-Permettant le défilement|-Besoins en ressources la plus élevés<br />-N’est pas disponible dans un scénario déconnecté|  
|**adLockReadOnly**|-Besoins en ressources faible<br />-Hautement évolutive|-À jour des données via un curseur|  
|**adLockBatchOptimistic**|-Mises à jour lot<br />: Permet les scénarios déconnectés<br />-Les autres utilisateurs en mesure d’accéder aux données|-Les données peuvent être modifiées par plusieurs utilisateurs à la fois|  
|**adLockPessimistic**|-Les données ne peut pas être modifiées par d’autres utilisateurs lors du verrouillage|-Empêche les autres utilisateurs d’accéder aux données lors du verrouillage|  
|**adLockOptimistic**|-Les autres utilisateurs en mesure d’accéder aux données|-Les données peuvent être modifiées par plusieurs utilisateurs à la fois|
