### Creating tablespace for utPLSQL  
```sql
create tablespace utplsql
datafile 'D:\Oracle\Tablespaces\utplsql.dbf'
size 10M
    reuse
    autoextend on next 10M maxsize 200M;

```

### Creating schema for utPLSQL  
To create the utPLSQL schema and grant all the required privileges execute script `create_utplsql_owner.sql` from the `source` directory with parameters:  
- `user name` - the name of the user that will own of utPLSQL object  
- `password` - the password to be set for that user  
- `tablespace name` - the tablespace name to hold data created during test execution
```oraclesqlplus
@create_utplsql_owner.sql utplsql <password> utplsql
```

### Installing utPLSQL  
To install the utPLSQL framework into your database, go to `source` directory, run the `install.sql` providing the `schema_name` for utPLSQL as parameter.
```oraclesqlplus
@install.sql utplsql
```

### Installing DDL trigger  
To install DDL trigger go to `source` directory, run the `install_ddl_trigger.sql` providing the `schema_name` for utPLSQL as parameter.

```oraclesqlplus
@install_ddl_trigger.sql utplsql
```

### Allowing other users to access the utPLSQL framework  
To grant utPLSQL to public execute script `source/create_synonyms_and_grants_for_public.sql` and provide `schema_name` where utPLSQL is installed.
```oraclesqlplus
@create_synonyms_and_grants_for_public.sql utplsql
```

### Checking environment and utPLSQL version  
To check the framework version execute the following query:
```sql
select substr(ut.version(),1,60) as ut_version from dual;
```
Additionally you may retrieve more information about your environment by executing the following query:
```sql
select 
  xmlserialize( content xmltype(ut_run_info()) as clob indent size = 2 )
  from dual;
```