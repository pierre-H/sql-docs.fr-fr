---
title: "SQLGetDescField et SQLGetDescRec (bibliothèque de curseurs) | Documents Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLGetDescField function [ODBC], Cursor Library
- SQLGetDescRec function [ODBC], Cursor Library
ms.assetid: 1a801f22-6fea-48aa-a723-3187a2ad852b
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ff32edcc14799980c1d8ec9e05bd27456d71a132
ms.contentlocale: fr-fr
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdescfield-and-sqlgetdescrec-cursor-library"></a>SQLGetDescField et SQLGetDescRec (bibliothèque de curseurs)
> [!IMPORTANT]  
>  Cette fonctionnalité sera supprimée dans une future version de Windows. Évitez d’utiliser cette fonctionnalité dans tout nouveau développement et prévoyez de modifier les applications qui utilisent actuellement cette fonctionnalité. Microsoft recommande d’utiliser les fonctionnalités de curseur du pilote.  
  
 Cette rubrique décrit l’utilisation de la **SQLGetDescField** et **SQLGetDescRec** fonctions dans la bibliothèque de curseurs. Pour obtenir des informations générales sur ces fonctions, consultez [fonction SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) et [SQLGetDescRec, fonction](../../../odbc/reference/syntax/sqlgetdescrec-function.md).  
  
 La bibliothèque de curseurs exécute **SQLGetDescRec** pour retourner des métadonnées pour les colonnes à signets. La bibliothèque de curseurs exécute **SQLGetDescField** pour retourner les mêmes champs retournés par **SQLGetDescRec**, qui sont SQL_DESC_NAME, SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE et SQL_DESC_NULLABLE. Par souci de cohérence, **SQLGetDescField** SQL_DESC_UNNAMED retourne également la valeur.  
  
 La bibliothèque de curseurs exécute **SQLGetDescField** lorsqu’elle est appelée pour retourner la valeur de ces champs qui sont définis pour la liaison de colonnes à signets : SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR, SQL_DESC_OCTET_LENGTH_PTR et SQL_DESC_LENGTH.  
  
 La bibliothèque de curseurs exécute **SQLGetDescField** lorsqu’elle est appelée pour retourner la valeur du champ SQL_DESC_BIND_OFFSET_PTR, SQL_DESC_BIND_TYPE, SQL_DESC_ROW_ARRAY_SIZE ou SQL_DESC_ROW_STATUS_PTR. Ces champs peuvent être retournées pour toute ligne, et pas seulement la ligne du signet.  
  
 Si une application appelle **SQLGetDescField** pour retourner la valeur de n’importe quel champ autres que celles mentionnées précédemment, la bibliothèque de curseurs passe l’appel au pilote.