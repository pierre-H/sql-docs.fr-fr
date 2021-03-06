---
title: "Initialiser automatiquement le groupe de disponibilit&#233; Always On | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 67c6a601-677a-402b-b3d1-8c65494e9e96
caps.latest.revision: 18
ms.author: "v-saume"
manager: "jhubbard"
---
# Initialiser automatiquement le groupe de disponibilit&#233; Always On
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]


 SQL Server 2016 propose un amorçage automatique des groupes de disponibilité. Quand vous créez un groupe de disponibilité par amorçage automatique, SQL Server crée automatiquement les réplicas secondaires de chaque base de données du groupe. Vous n’avez plus besoin de sauvegarder ni de restaurer manuellement les réplicas secondaires. Pour activer l’amorçage automatique, créez le groupe de disponibilité avec T-SQL.
 
## Conditions préalables

L’amorçage automatique exige que le chemin des fichiers de données et des fichiers journaux soit le même sur chaque instance de SQL Server qui participe au groupe de disponibilité. 

L’amorçage du groupe de disponibilité communique par le biais du point de terminaison de mise en miroir de bases de données. Ouvrez des règles de pare-feu pour le trafic entrant dans le port du point de terminaison de mise en miroir sur chaque serveur.

Les bases de données incluses dans un groupe de disponibilité doivent être en mode de récupération complet. La base de données a besoin d’une sauvegarde complète actualisée et d’une sauvegarde du journal des transactions. Ces fichiers de sauvegarde ne sont pas utilisés pour l’amorçage automatique, mais ils sont exigés avant d’inclure la base de données dans un groupe de disponibilité. 
 
## Créer un groupe de disponibilité par amorçage automatique

Pour créer un groupe de disponibilité par amorçage automatique, définissez `SEEDING_MODE=AUTOMATIC`. 

L’exemple suivant crée un groupe de disponibilité sur un cluster de basculement Windows Server à deux nœuds. Avant d’exécuter les scripts, mettez à jour les valeurs conformément à votre environnement.

1. Créez les points de terminaison. Chaque serveur a besoin d’un point de terminaison. Le script suivant crée un point de terminaison qui utilise le port TCP 5022 pour l’écouteur. Définissez `<endpoint_name>` et `LISTENER_PORT` conformément à votre environnement et exécutez le script :

    ```
    --Create the endpoint on both servers
    -- Run this script twice, once on each server. 
    CREATE ENDPOINT [<endpoint_name>] 
    STATE=STARTED
    AS TCP (LISTENER_PORT = 5022, LISTENER_IP = ALL)
    FOR DATA_MIRRORING (ROLE = ALL, AUTHENTICATION = WINDOWS NEGOTIATE, ENCRYPTION = REQUIRED ALGORITHM AES)
    GO
    ```

1. Créez le groupe de disponibilité. Le script suivant crée le groupe de disponibilité. Mettez à jour les valeurs du nom du groupe, des noms de serveur et des noms de domaine, puis exécutez-le sur l’instance principale de SQL Server.  

    ```
    ---Run On Primary
    CREATE AVAILABILITY GROUP [<availability_group_name>]
    FOR DATABASE db1
    REPLICA ON'<*primary_server*>'
    WITH (ENDPOINT_URL = N'TCP://<primary_server>.<fully_qualified_domain_name>:5022', 
    FAILOVER_MODE = AUTOMATIC, 
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
    BACKUP_PRIORITY = 50, 
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO), 
    SEEDING_MODE = AUTOMATIC),
    N'<secondary_server>' WITH (ENDPOINT_URL = N'TCP://<secondary_server>.<fully_qualified_domain_name>:5022', 
    FAILOVER_MODE = AUTOMATIC, 
    AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
    BACKUP_PRIORITY = 50, 
    SECONDARY_ROLE(ALLOW_CONNECTIONS = NO), 
    SEEDING_MODE = AUTOMATIC);
    GO
    ``` 

1. Joignez le serveur secondaire au groupe de disponibilité et octroyez à ce dernier une autorisation de créer des bases de données. Exécutez le script suivant sur l’instance secondaire de SQL Server : 
 
    ```
    --Run on Secondary Replica to join to the availability group
    ALTER AVAILABILITY GROUP [<availability_group_name>] JOIN
    GO  
    ALTER AVAILABILITY GROUP [<availability_group_name>] GRANT CREATE ANY DATABASE
    GO
    ```

SQL Server crée automatiquement le réplica de base de données sur le serveur secondaire. Si la base de données est volumineuse, sa synchronisation peut prendre un certain temps. Si une base de données se trouve dans un groupe de disponibilité configuré pour l’amorçage automatique, vous pouvez interroger la vue système `sys.dm_hadr_automatic_seeding` pour surveiller la progression de l’amorçage. La requête suivante renvoie une seule ligne pour chaque base de données présente dans un groupe de disponibilité configuré pour l’amorçage automatique.

```
 SELECT start_time,
       ag.name,
       db.database_name,
       current_state,
       performed_seeding,
       failure_state,
       failure_state_desc
 FROM sys.dm_hadr_automatic_seeding autos 
    JOIN sys.availability_databases_cluster db ON autos.ag_db_id = db.group_database_id
    JOIN sys.availability_groups ag ON autos.ag_id = ag.group_id
```

## Empêcher l’amorçage automatique sur un groupe de disponibilité

Pour empêcher temporairement le serveur principal d’amorcer davantage de bases de données sur le réplica secondaire, vous pouvez refuser au groupe de disponibilité l’autorisation de créer des bases de données. Exécutez la requête suivante sur l’instance qui héberge le réplica secondaire pour refuser au groupe de disponibilité l’autorisation de créer des bases de données.

```
ALTER AVAILABILITY GROUP [<availability_group_name>] DENY CREATE ANY DATABASE
GO
```


## Activer l’amorçage automatique sur un groupe de disponibilité existant

Vous pouvez définir l’amorçage automatique sur une base de données existante. La commande suivante modifie un groupe de disponibilité pour qu’il utilise l’amorçage automatique. 

```
ALTER AVAILABILITY GROUP [<availability_group_name>] 
MODIFY REPLICA ON '<primary_node>' WITH (SEEDING_MODE = AUTOMATIC)
GO
```

Elle force une base de données à redémarrer l’amorçage, si besoin. Par exemple, si l’amorçage échoue en raison d’un espace disque insuffisant sur le réplica secondaire, vous pouvez exécuter `ALTER AVAILABILITY GROUP ... WITH (SEEDING_MODE=AUTOMATIC)` pour redémarrer l’amorçage après avoir ajouté de l’espace libre.

## Arrêter l’amorçage automatique

Pour arrêter l’amorçage automatique pour un groupe de disponibilité, exécutez le script suivant sur l’instance qui héberge le réplica principal :

```
ALTER AVAILABILITY GROUP [<availability_group_name>] 
    MODIFY REPLICA ON '<primary_node>'   
    WITH (SEEDING_MODE = MANUAL)
GO
```

Tous les réplicas en cours d’amorçage sont annulés et SQL Server ne peut plus initialiser automatiquement les réplicas de ce groupe de disponibilité. La synchronisation de tous les réplicas déjà initialisés n’est quant à elle pas interrompue. 


## Surveiller un groupe de disponibilité à amorçage automatique

### Utiliser les vues de gestion dynamique du système pour surveiller l’amorçage

Les vues système suivantes indiquent l’état de l’amorçage automatique SQL Server.

**sys.dm_hadr_automatic_seeding** 

Sur le réplica principal, interrogez `sys.dm_hadr_automatic_seeding` pour vérifier l’état du processus d’amorçage automatique. La vue retourne une seule ligne pour chaque processus d’amorçage. Par exemple :

``` 
SELECT start_time, 
        completion_time
        is_source,
        current_state,
        failure_state,
        failure_state_desc
FROM sys.dm_hadr_automatic_seeding
```
 
**sys.dm_hadr_physical_seeding_stats** 

Sur le réplica principal, interrogez la vue de gestion dynamique `sys.dm_hadr_physical_seeding_stats` pour voir les statistiques physiques de chaque processus d’amorçage en cours d’exécution. La requête suivante retourne des lignes quand l’amorçage est en cours d’exécution :

```
SELECT * FROM sys.dm_hadr_physical_seeding_stats;
```

### Diagnostiquer l’initialisation de bases de données à l’aide de l’amorçage automatique dans le journal des erreurs

Quand vous ajoutez une base de données à un groupe de disponibilité configuré pour l’amorçage automatique, SQL Server effectue une sauvegarde VDI sur le point de terminaison du groupe de disponibilité. Consultez le journal des erreurs SQL Server pour déterminer quand la sauvegarde a été effectuée et le serveur secondaire synchronisé.

### Diagnostiquer l’intégrité au niveau de la base de données avec des événements étendus

L’amorçage automatique comporte de nouveaux événements étendus pour le suivi des modifications d’état, des échecs et des statistiques de performance pendant l’initialisation. 

Par exemple, ce script crée une session d’événements étendus qui capture les événements liés à l’amorçage automatique : 

```
CREATE EVENT SESSION [AlwaysOn_autoseed] ON SERVER 
    ADD EVENT sqlserver.hadr_automatic_seeding_state_transition,
    ADD EVENT sqlserver.hadr_automatic_seeding_timeout,
    ADD EVENT sqlserver.hadr_db_manager_seeding_request_msg,
    ADD EVENT sqlserver.hadr_physical_seeding_backup_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_failure,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_forwarder_target_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_progress,
    ADD EVENT sqlserver.hadr_physical_seeding_restore_state_change,
    ADD EVENT sqlserver.hadr_physical_seeding_submit_callback
    ADD TARGET package0.event_file(SET filename=N’autoseed.xel’,max_file_size=(5),max_rollover_files=(4))
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=30 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=ON)
GO 

ALTER EVENT SESSION AlwaysOn_autoseed ON SERVER STATE=START
GO 
```


Le tableau suivant répertorie les événements étendus liés à l’amorçage automatique : 

| Nom | Description|
|------------ |---------------| 
|hadr_db_manager_seeding_request_msg |  Message de demande d’amorçage.
|hadr_physical_seeding_backup_state_change |    Modification d’état côté sauvegarde d’amorçage physique.
|hadr_physical_seeding_restore_state_change |Modification d’état côté restauration d’amorçage physique.
|hadr_physical_seeding_forwarder_state_change | Modification d’état côté redirecteur d’amorçage physique.
|hadr_physical_seeding_forwarder_target_state_change |  Modification d’état côté cible du redirecteur d’amorçage physique.
|hadr_physical_seeding_submit_callback  |Événement de rappel de soumission d’amorçage physique.
|hadr_physical_seeding_failure  |Événement d’échec d’amorçage physique.
|hadr_physical_seeding_progress |   Événement de progression d’amorçage physique.
|hadr_physical_seeding_schedule_long_task_failure   |Événement d’échec de longue tâche de planification d’amorçage physique.
|hadr_automatic_seeding_start   |Se produit quand une opération d’amorçage automatique est soumise.
|hadr_automatic_seeding_state_transition    |Se produit quand une opération d’amorçage automatique change d’état.
|hadr_automatic_seeding_success |Se produit quand une opération d’amorçage automatique aboutit.
|hadr_automatic_seeding_failure |Se produit quand une opération d’amorçage automatique échoue.
|hadr_automatic_seeding_timeout |Se produit quand une opération d’amorçage automatique expire.

### Autres considérations liées à la résolution des problèmes

**Surveiller la fin de l’amorçage automatique**

Interrogez `sys.dm_hadr_physical_seeding_stats` pour connaître les processus d’amorçage automatique en cours d’exécution. La vue retourne une seule ligne pour chaque base de données. Par exemple :

```
SELECT local_database_name, 
       role_desc, 
       internal_state_desc, 
       transfer_rate_bytes_per_second, 
       transferred_size_bytes, 
       database_size_bytes, 
       start_time_utc, 
       end_time_utc, estimate_time_complete_utc, 
       total_disk_io_wait_time_ms, 
       total_network_wait_time_ms, 
       is_compression_enabled 
FROM sys.dm_hadr_physical_seeding_stats
```

**Résoudre les problèmes liés à l’absence d’une base de données dans un groupe de disponibilité configuré pour l’amorçage automatique**


Quand une base de données n’apparaît pas dans un groupe de disponibilité pour lequel l’amorçage automatique est activé, ce dernier a probablement échoué. La base de données n’est donc pas ajoutée au groupe de disponibilité sur les réplicas principal et secondaire. Interrogez `sys.dm_hadr_automatic_seeding` sur les réplicas principaux et secondaires. Par exemple, exécutez la requête suivante pour identifier l’état d’échec de l’amorçage automatique.

```
SELECT start_time, 
       completion_time, 
       is_source, 
       current_state, 
       failure_state, 
       failure_state_desc, 
       error_code 
FROM sys.dm_hadr_automatic_seeding
```

## Considérations liées à l’amorçage automatique et aux performances

SQL Server utilise un nombre fixe de threads pour l’amorçage automatique. Sur l’instance principale, SQL Server utilise un seul thread par numéro d’unité logique pour lire les modifications. Sur l’instance secondaire, SQL Server utilise un seul thread par numéro d’unité logique pour initialiser la base de données.

Définissez l’indicateur de trace 9567 sur le réplica principal pour activer la compression du flux de données pendant l’amorçage automatique. Le temps de transfert de l’amorçage automatique est alors considérablement réduit, mais l’utilisation du processeur est quant à elle accrue. Pour plus d’informations, consultez [Régler la compression pour le groupe de disponibilité](../../../database-engine/availability-groups/windows/tune-compression-for-availability-group.md). 


## Quand ne pas utiliser l’amorçage automatique

Dans certains scénarios, l’amorçage automatique ne s’avère pas optimal pour initialiser un réplica secondaire. Au cours de l’amorçage automatique, SQL Server effectue une sauvegarde sur le réseau à des fins d’initialisation. Ce processus peut être lent si les bases de données sont très volumineuses ou si le réplica secondaire est distant. Le journal des transactions de ces bases de données ne peut pas être tronqué pendant le processus de sauvegarde. Par conséquent, tout processus d’initialisation qui se prolonge sur une base de données volumineuse peut entraîner une croissance importante du journal des transactions.
Avant d’ajouter une base de données à un groupe de disponibilité par amorçage automatique, évaluez la taille de la base de données, le chargement et la distance de site entre les réplicas.

## Ressources

[CREATE AVAILABILITY GROUP (Transact-SQL)
-](https://msdn.microsoft.com/library/ff878399.aspx)

[Guide de surveillance et de résolution des problèmes des groupes de disponibilité Always On](http://technet.microsoft.com/library/dn135328.aspx)
