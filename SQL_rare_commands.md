# SQL server notes
This Note is not for SQL Learning. These are for beginners. 
where these commands might not cover in the initial courseware.

## 1. SQL Replication

**Replication Types:**
- **Snapshot Replication:** Distributes data exactly as it appears at a specific moment in time.
- **Transactional Replication:** Suitable for real-time, low-latency applications.
- **Merge Replication:** Ideal for applications with offline capabilities.

**Basic Commands:**
- Check replication status:
  ```sql
  EXEC sp_replmonitorhelppublication;
  EXEC sp_replmonitorhelpsubscription;
  ```
- Add a publication:
  ```sql
  EXEC sp_addpublication @publication = 'MyPublication', @status = 'active';
  ```
- Add a subscription:
  ```sql
  EXEC sp_addsubscription @publication = 'MyPublication', @subscriber = 'SubscriberServer', @destination_db = 'MyDB';
  ```

## 2. Offline Export and Import

**Exporting Data:**
- Export to `.bak` file:
  ```sql
  BACKUP DATABASE [MyDB] TO DISK = 'C:\Backup\MyDB.bak';
  ```
- Export using BCP (Bulk Copy Program):
  ```bash
  bcp MyDB.dbo.MyTable out C:\Backup\MyTable.dat -c -U username -S servername -P password
  ```

**Importing Data:**
- Restore `.bak` file:
  ```sql
  RESTORE DATABASE [MyDB] FROM DISK = 'C:\Backup\MyDB.bak' WITH REPLACE;
  ```
- Import using BCP:
  ```bash
  bcp MyDB.dbo.MyTable in C:\Backup\MyTable.dat -c -U username -S servername -P password
  ```

## 3. User Management

**Creating Users:**
```sql
CREATE LOGIN MyUser WITH PASSWORD = 'StrongPassword123!';
CREATE USER MyUser FOR LOGIN MyUser;
ALTER ROLE db_datareader ADD MEMBER MyUser;
ALTER ROLE db_datawriter ADD MEMBER MyUser;
```

**Granting Full Access:**
```sql
ALTER SERVER ROLE sysadmin ADD MEMBER MyUser;
-- OR for database-specific full access
ALTER ROLE db_owner ADD MEMBER MyUser;
```

**Modifying Permissions:**
```sql
GRANT SELECT, INSERT, UPDATE, DELETE ON dbo.MyTable TO MyUser;
REVOKE INSERT ON dbo.MyTable FROM MyUser;
```

**Dropping Users:**
```sql
DROP USER MyUser;
DROP LOGIN MyUser;
```

## 4. Other Useful Commands

- Check database size:
  ```sql
  EXEC sp_spaceused;
  ```
- List active sessions:
  ```sql
  SELECT * FROM sys.dm_exec_sessions WHERE status = 'running';
  ```
- Kill a session:
  ```sql
  KILL <session_id>;
  ```
- Check for blocking sessions:
  ```sql
  SELECT blocking_session_id, session_id, wait_type, wait_time, wait_resource
  FROM sys.dm_exec_requests
  WHERE blocking_session_id <> 0;
  ```
- Database integrity check:
  ```sql
  DBCC CHECKDB ('MyDB');
  ```
- Rebuild indexes:
  ```sql
  ALTER INDEX ALL ON dbo.MyTable REBUILD;
  ```

---

This note covers essential SQL Server tasks for replication, data export/import, user management, full access control, and other useful commands.

