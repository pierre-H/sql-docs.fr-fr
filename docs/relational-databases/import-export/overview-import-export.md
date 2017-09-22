---
title: "Importer et exporter des données dans SQL Server et Azure SQL Database | Microsoft Docs"
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 6e754198cf82a7ba0752fe8f20c3780a8ac551d7
ms.openlocfilehash: 3c41be0642b13b63367c5601b716b506808472e7
ms.contentlocale: fr-fr
ms.lasthandoff: 09/14/2017

---
# <a name="import-and-export-data-from-sql-server-and-azure-sql-database"></a>Importer et exporter des données dans SQL Server et Azure SQL Database
Plusieurs méthodes sont possibles pour importer et exporter des données dans SQL Server et Azure SQL Database. Vous pouvez notamment utiliser des instructions Transact-SQL, des outils en ligne de commande et des Assistants.

De plus, vous pouvez importer et exporter des données de formats différents, tels que les fichiers plats, les fichiers Excel, les principales bases de données relationnelles et divers services cloud.

## <a name="methods-for-importing-and-exporting-data"></a>Méthodes pour l’importation et l’exportation de données

### <a name="use-transact-sql-statements"></a>Utilisation d’instructions Transact-SQL
Vous pouvez importer des données à l’aide des commandes `BULK INSERT` ou `OPENROWSET(BULK...)`. En général, vous exécutez ces commandes dans SQL Server Management Studio (SSMS). Pour plus d’informations, consultez [Importer des données en bloc à l’aide de BULK INSERT ou OPENROWSET(BULK...)](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

### <a name="use-bcp-from-the-command-prompt"></a>Utilisation de BCP à partir de l’invite de commandes
Vous pouvez importer et exporter des données avec l’utilitaire en ligne de commande BCP. Pour plus d’informations, consultez [Importer et exporter des données en bloc à l’aide de l’utilitaire BCP](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

### <a name="use-the-sql-server-import-and-export-wizard"></a>Utilisation de l’Assistant Importation et Exportation SQL Server
L’Assistant Importation et Exportation SQL Server vous permet d’importer des données de diverses sources ou d’en exporter vers diverses destinations. Pour utiliser cet Assistant, vous devez avoir installé SQL Server Integration Services (SSIS) ou SQL Server Data Tools (SSDT). Pour plus d’informations, consultez [Importer et exporter des données avec l’Assistant Importation et Exportation SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

### <a name="design-your-own-import-or-export"></a>Conception de votre propre importation ou exportation
Si vous souhaitez concevoir une importation de données personnalisée, utilisez l’un des services ou fonctionnalités suivants :
-   SQL Server Integration Services. Pour plus d’informations, consultez [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).
-   Azure Data Factory. Pour plus d’informations, consultez [Présentation d’Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-introduction).

## <a name="data-formats-for-import-and-export"></a>Formats des données à importer ou exporter

### <a name="supported-formats"></a>Formats pris en charge

Vous pouvez importer et exporter des données de ou vers des fichiers plats ou divers autres formats de fichiers, bases de données relationnelles et services cloud. Pour en savoir plus sur ces options disponibles pour les outils spécifiques, consultez les rubriques suivantes :
-   Pour l’Assistant Importation et Exportation SQL Server, consultez [Se connecter aux sources de données avec l’Assistant Importation et Exportation SQL Server](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md).
-   Pour SQL Server Integration Services, consultez [Connexions Integration Services (SSIS)](../../integration-services/connection-manager/integration-services-ssis-connections.md).
-   Pour Azure Data Factory, consultez [Connecteurs Azure Data Factory](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-amazon-redshift-connector).

### <a name="commonly-used-data-formats"></a>Formats de données courants

Il existe des exemples et des considérations spécifiques relatifs à certains formats de données couramment utilisés. Pour en savoir plus sur ces formats de données, consultez les rubriques suivantes :
-   Pour Excel, consultez [Importer des données d’Excel](import-data-from-excel-to-sql.md).
-   Pour JSON, consultez [Importer des documents JSON](../json/import-json-documents-into-sql-server.md).
-   Pour XML, consultez [Importer et exporter des documents XML](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md).
-   Pour le Stockage Blob Azure, consultez [Importer et exporter des données à partir du Stockage Blob Azure](examples-of-bulk-access-to-data-in-azure-blob-storage.md).

## <a name="next-steps"></a>Étapes suivantes
Si vous ne savez pas comment démarrer une importation ou une exportation, utilisez l’Assistant Importation et Exportation SQL Server. Pour avoir une présentation générale, consultez [Bien démarrer avec cet exemple simple de l’Assistant Importation et Exportation](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).
