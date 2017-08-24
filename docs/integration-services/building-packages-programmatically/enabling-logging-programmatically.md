---
title: Activation de la journalisation par programme | Documents Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- Integration Services packages, logs
- SSIS logging
- log providers [Integration Services]
- logs [Integration Services], enabling
- LoggingMode property
- LogProvider object
- packages [Integration Services], logs
ms.assetid: 3222a1ed-83eb-421c-b299-a53b67bba740
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: dd512f022832b57aa3fdcb85260926dd8354298c
ms.contentlocale: fr-fr
ms.lasthandoff: 08/03/2017

---
# <a name="enabling-logging-programmatically"></a>Activation de la journalisation par programme
  Le moteur d'exécution fournit une collection d'objets <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> qui permettent la capture d'informations spécifiques à un événement au cours de la validation et de l'exécution de package. Les objets <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> sont disponibles pour les objets <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer>, y compris les objets <xref:Microsoft.SqlServer.Dts.Runtime.TaskHost>, <xref:Microsoft.SqlServer.Dts.Runtime.Package>, <xref:Microsoft.SqlServer.Dts.Runtime.ForLoop> et <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop>. La journalisation est activée sur des conteneurs individuels, ou sur l'ensemble du package.  
  
 Un conteneur peut utiliser plusieurs types des modules fournisseurs d'informations disponibles. Il est donc possible de créer et stocker des informations de journal dans de multiples formats. L'inscription d'un objet conteneur dans la journalisation s'effectue en deux étapes : d'abord l'activation de la journalisation, puis la sélection d'un module fournisseur d'informations. Les propriétés <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingOptions%2A> et <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> du conteneur permettent de spécifier les événements enregistrés et sélectionner le module fournisseur d'informations.  
  
## <a name="enabling-logging"></a>Activation de la journalisation  
 La propriété <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A>, disponible dans chaque conteneur capable d'exécuter la journalisation, détermine si les informations d'événements du conteneur doivent être enregistrées dans le journal des événements. Cette propriété est affectée d'une valeur issue de la structure <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode> et est héritée du parent du conteneur par défaut. Si le conteneur est un package et par conséquent n’a aucun parent, la propriété utilise la <xref:Microsoft.SqlServer.Dts.Runtime.DTSLoggingMode.UseParentSetting>, qui utilise par défaut **désactivé**.  
  
### <a name="selecting-a-log-provider"></a>Sélection d'un module fournisseur d'informations  
 Après le <xref:Microsoft.SqlServer.Dts.Runtime.DtsContainer.LoggingMode%2A> est définie sur **activé**, un module fournisseur d’informations est ajouté à la <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> collection du conteneur pour terminer le processus. La collection <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> est disponible sur l'objet <xref:Microsoft.SqlServer.Dts.Runtime.LoggingOptions> et contient les modules fournisseurs d'informations sélectionnés pour le conteneur. La méthode <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders.Add%2A> est appelée pour créer un fournisseur et l'ajouter à la collection. La méthode retourne ensuite le module fournisseur d'informations qui a été ajouté à la collection. Chaque fournisseur a des paramètres de configuration spécifiques et ces propriétés sont définies à l'aide de la propriété <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A>.  
  
 Le tableau suivant répertorie les modules fournisseurs d'informations disponibles, leur description et leurs informations <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider.ConfigString%2A>.  
  
|Fournisseur| Description|Propriété ConfigString|  
|--------------|-----------------|---------------------------|  
|SQL Server Profiler|Génère des traces SQL qui peuvent être capturées et affichées dans [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler. L'extension de nom de fichier par défaut de ce fournisseur est .trc.|Aucune configuration n'est requise.|  
|SQL Server|Enregistre les entrées de journal des événements dans le **sysssislog** table dans les [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] base de données.|Le fournisseur [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requiert que la connexion à la base de données soit spécifiée, ainsi que le nom de la base de données cible.|  
|Fichier texte|Écrit les entrées du journal des événements dans des fichiers texte ASCII au format CSV. L'extension de nom de fichier par défaut de ce fournisseur est .log.|Nom d'un gestionnaire de connexions de fichiers.|  
|Journal des événements Windows|Enregistre dans le journal des événements Windows standard sur l'ordinateur local dans le journal des applications.|Aucune configuration n'est requise.|  
|Fichier XML|Écrit les entrées du journal des événements dans un fichier au format XML. L'extension de nom de fichier par défaut de ce fournisseur est .xml.|Nom d'un gestionnaire de connexions de fichiers.|  
  
 Les événements sont inclus ou exclus du journal des événements en définissant le **eventfilterkind du** et **EventFilter** propriétés du conteneur. Le **eventfilterkind du** structure contient deux valeurs, **ExclusionFilter** et **InclusionFilter**, qui indiquent si les événements qui sont ajoutés à la **EventFilter** sont inclus dans le journal des événements. Le **EventFilter** propriété est ensuite assignée un tableau de chaînes qui contient les noms des événements qui font l’objet du filtrage.  
  
 Le code suivant active la journalisation sur un package, ajoute le module fournisseur d'informations pour les fichiers texte à la collection <xref:Microsoft.SqlServer.Dts.Runtime.SelectedLogProviders> et spécifie une liste d'événements à inclure dans la sortie de la journalisation.  
  
## <a name="sample"></a>Exemple  
  
```csharp  
using System;  
using Microsoft.SqlServer.Dts.Runtime;  
  
namespace Microsoft.SqlServer.Dts.Samples  
{  
  class Program  
  {  
    static void Main(string[] args)  
    {  
      Package p = new Package();  
  
      ConnectionManager loggingConnection = p.Connections.Add("FILE");  
      loggingConnection.ConnectionString = @"C:\SSISPackageLog.txt";  
  
      LogProvider provider = p.LogProviders.Add("DTS.LogProviderTextFile.2");  
      provider.ConfigString = loggingConnection.Name;  
      p.LoggingOptions.SelectedLogProviders.Add(provider);  
      p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion;  
      p.LoggingOptions.EventFilter = new String[] { "OnPreExecute",   
         "OnPostExecute", "OnError", "OnWarning", "OnInformation" };  
      p.LoggingMode = DTSLoggingMode.Enabled;  
  
      // Add tasks and other objects to the package.  
  
    }  
  }  
}  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
  
Module Module1  
  
  Sub Main()  
  
    Dim p As Package = New Package()  
  
    Dim loggingConnection As ConnectionManager = p.Connections.Add("FILE")  
    loggingConnection.ConnectionString = "C:\SSISPackageLog.txt"  
  
    Dim provider As LogProvider = p.LogProviders.Add("DTS.LogProviderTextFile.2")  
    provider.ConfigString = loggingConnection.Name  
    p.LoggingOptions.SelectedLogProviders.Add(provider)  
    p.LoggingOptions.EventFilterKind = DTSEventFilterKind.Inclusion  
    p.LoggingOptions.EventFilter = New String() {"OnPreExecute", _  
       "OnPostExecute", "OnError", "OnWarning", "OnInformation"}  
    p.LoggingMode = DTSLoggingMode.Enabled  
  
    ' Add tasks and other objects to the package.  
  
  End Sub  
  
End Module  
```  
  
## <a name="see-also"></a>Voir aussi  
 [Integration Services &#40; SSIS &#41; Journalisation](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  