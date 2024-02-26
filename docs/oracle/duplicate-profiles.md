# Duplicate Oracle Profiles

Create `profiles.sql` with below contents
```
SET serveroutput ON

DECLARE
 CURSOR c_profiles IS
  SELECT PROFILE, RESOURCE_NAME, LIMIT
  FROM dba_profiles
  ORDER BY PROFILE, resource_name;

  s_PROFILE                     dba_profiles.PROFILE%TYPE ;
  s_prev_PROFILE        dba_profiles.PROFILE%TYPE ;
  s_RESOURCE_NAME       dba_profiles.RESOURCE_NAME%TYPE ;
  s_LIMIT                       dba_profiles.LIMIT%TYPE ;
BEGIN

s_prev_PROFILE := 'no_such_profile' ;

dbms_output.enable(1000000);
OPEN c_profiles;
LOOP
  FETCH c_profiles INTO s_PROFILE,s_RESOURCE_NAME,s_LIMIT ;
  IF ( s_prev_profile <> s_profile ) THEN
    BEGIN
      dbms_output.put_line ( '--');
      dbms_output.put_line ( 'create profile "'||s_profile||'" limit ' ||s_RESOURCE_NAME|| ' ' || s_LIMIT||';' ) ;
      s_prev_profile := s_profile ;
    END;
  ELSE
       dbms_output.put_line ( 'alter profile "'||s_profile|| '" limit ' ||s_RESOURCE_NAME|| ' ' || s_LIMIT || ';' ) ;
  END IF;
  EXIT WHEN c_profiles%NOTFOUND ;
END LOOP ;

CLOSE c_profiles ;

END;
/
```

Sample execution

```
$ sqlplus / as sysdba

SQL*Plus: Release 11.2.0.2.0 Production on Thu Aug 18 10:36:46 2022

Copyright (c) 1982, 2010, Oracle.  All rights reserved.


Connected to:
Oracle Database 11g Release 11.2.0.2.0 - Production

SQL> @profiles.sql
--
create profile "DEFAULT" limit COMPOSITE_LIMIT UNLIMITED;
alter profile "DEFAULT" limit CONNECT_TIME UNLIMITED;
alter profile "DEFAULT" limit CPU_PER_CALL UNLIMITED;
alter profile "DEFAULT" limit CPU_PER_SESSION UNLIMITED;
alter profile "DEFAULT" limit FAILED_LOGIN_ATTEMPTS 10;
alter profile "DEFAULT" limit IDLE_TIME UNLIMITED;
alter profile "DEFAULT" limit LOGICAL_READS_PER_CALL UNLIMITED;
alter profile "DEFAULT" limit LOGICAL_READS_PER_SESSION UNLIMITED;
alter profile "DEFAULT" limit PASSWORD_GRACE_TIME 7;
alter profile "DEFAULT" limit PASSWORD_LIFE_TIME 180;
alter profile "DEFAULT" limit PASSWORD_LOCK_TIME 1;
alter profile "DEFAULT" limit PASSWORD_REUSE_MAX UNLIMITED;
alter profile "DEFAULT" limit PASSWORD_REUSE_TIME UNLIMITED;
alter profile "DEFAULT" limit PASSWORD_VERIFY_FUNCTION NULL;
alter profile "DEFAULT" limit PRIVATE_SGA UNLIMITED;
alter profile "DEFAULT" limit SESSIONS_PER_USER UNLIMITED;
--
create profile "NO_PWD_EXPIRE" limit COMPOSITE_LIMIT UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit CONNECT_TIME UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit CPU_PER_CALL UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit CPU_PER_SESSION UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit FAILED_LOGIN_ATTEMPTS UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit IDLE_TIME UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit LOGICAL_READS_PER_CALL UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit LOGICAL_READS_PER_SESSION UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit PASSWORD_GRACE_TIME UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit PASSWORD_LIFE_TIME UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit PASSWORD_LOCK_TIME UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit PASSWORD_REUSE_MAX UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit PASSWORD_REUSE_TIME UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit PASSWORD_VERIFY_FUNCTION NULL;
alter profile "NO_PWD_EXPIRE" limit PRIVATE_SGA UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit SESSIONS_PER_USER UNLIMITED;
alter profile "NO_PWD_EXPIRE" limit SESSIONS_PER_USER UNLIMITED;

PL/SQL procedure successfully completed.

SQL> quit
```
