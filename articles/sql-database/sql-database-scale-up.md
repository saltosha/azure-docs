---
title: Change the service tier and performance level of an Azure SQL database | Microsoft Docs
description: Change the service tier and performance level of an Azure SQL database shows how to scale your SQL database up or down. Changing the pricing tier of an Azure SQL database.
services: sql-database
documentationcenter: ''
author: stevestein
manager: jhubbard
editor: ''

ms.assetid: cbd67e88-08d5-40e2-a223-0fb0c718a782
ms.service: sql-database
ms.custom: monitor and tune
ms.devlang: NA
ms.date: 10/12/2016
ms.author: sstein
ms.workload: data-management
ms.topic: article
ms.tgt_pltfrm: NA

---
# Change the service tier and performance level (pricing tier) of a SQL database using the Azure portal
> [!div class="op_single_selector"]
> * [**Azure portal**](sql-database-scale-up.md)
> * [PowerShell](sql-database-scale-up-powershell.md)
> 
> 

Service tiers and performance levels describe the features and resources available for your SQL database and can be updated as the needs of your application change. For details, see [Service Tiers](sql-database-service-tiers.md).

Note that changing the service tier and/or performance level of a database creates a replica of the original database at the new performance level, and then switches connections over to the replica. No data is lost during this process but during the brief moment when we switch over to the replica, connections to the database are disabled, so some transactions in flight may be rolled back. This window varies, but is on average under 4 seconds, and in more than 99% of cases is less than 30 seconds. Very infrequently, especially if there are large numbers of transactions in flight at the moment connections are disabled, this window may be longer.  

The duration of the entire scale-up process will, in most cases, take less than 5 minutes. 

Use the information in [Azure SQL Database Service Tiers and Performance Levels](sql-database-service-tiers.md) to determine the appropriate service tier and performance level for your Azure SQL Database.

* To downgrade a database, the database should be smaller than the maximum allowed size of the target service tier. 
* When upgrading a database with [Geo-Replication](sql-database-geo-replication-overview.md) enabled, you must first upgrade its secondary databases to the desired performance tier before upgrading the primary database.
* When downgrading a service tier, you must first terminate all Geo-Replication relationships. 
* The restore service offerings are different for the various service tiers. If you are downgrading you may lose the ability to restore to a point in time, or have a lower backup retention period. For more information, see [Azure SQL Database Backup and Restore](sql-database-business-continuity.md).
* Changing your database pricing tier does not change the max database size. To change your database max size use [Transact-SQL (T-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) or [PowerShell](https://msdn.microsoft.com/library/mt619433.aspx).
* The new properties for the database are not applied until the changes are complete.

**To complete this article you need the following:**

* An Azure SQL database. If you do not have a SQL database, create one following the steps in this article: [Create your first Azure SQL Database](sql-database-get-started.md).

## Change the service tier and performance level of your database
Open the SQL Database blade for the database you want to scale up or down:

1. In the [Azure portal](https://portal.azure.com), click **More services** > **SQL databases**.
2. Click the database you want to change.
3. On the **SQL database** blade click **Pricing tier (scale DTUs)**:
   
   ![pricing tier][1]
4. Choose a new tier and click **Select**:
   
   Clicking **Select** submits a scale request to change the pricing tier. Depending on the size of your database the scale operation can take some time to complete (see the info at the top of this article).
   
   > [!NOTE]
   > Changing your database pricing tier does not change the max database size. To change your database max size use [Transact-SQL (T-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) or [PowerShell](https://msdn.microsoft.com/library/mt619433.aspx).
   > 
   > 
   
   ![select pricing tier][2]
5. Click the notification icon (bell), in the upper right:
   
   ![notifications][3]
   
   Click the notification text to open the details pane where you can see the status of the request.

## Next steps
* Change your database max size using [Transact-SQL (T-SQL)](https://msdn.microsoft.com/library/mt574871.aspx) or [PowerShell](https://msdn.microsoft.com/library/mt619433.aspx).
* [Scale out and in](sql-database-elastic-scale-get-started.md)
* [Connect and query a SQL database with SSMS](sql-database-connect-query-ssms.md)
* [Export an Azure SQL database](sql-database-export.md)

## Additional resources
* [Business Continuity Overview](sql-database-business-continuity.md)
* [SQL Database documentation](https://azure.microsoft.com/documentation/services/sql-database/)

<!--Image references-->
[1]: ./media/sql-database-scale-up/new-tier.png
[2]: ./media/sql-database-scale-up/choose-tier.png
[3]: ./media/sql-database-scale-up/scale-notification.png
[4]: ./media/sql-database-scale-up/new-tier.png
