# howtoinstallordsapex201
First download apex 20.1
downloa dords 20.1
EXEC dbms_xdb.sethttpport(0);
apexins sysaux sysaux temp /i/
ed n1
Declare
   Acl_Path Varchar2(4000);
Begin
   -- Look for the ACL currently assigned to '*' and give APEX_050000
   -- the "connect" privilege if APEX_050000 does not have the privilege yet.
   Select Acl
   Into   Acl_Path
   From   Dba_Network_Acls
   Where  Host = '*'
   And    Lower_Port Is Null
   And    Upper_Port Is Null;
   If Dbms_Network_Acl_Admin.Check_Privilege(Acl_Path
                                            ,'APEX_200200'
                                            ,'connect') Is Null Then
      Dbms_Network_Acl_Admin.Add_Privilege(Acl_Path
                                          ,'APEX_200200'
                                          ,True
                                          ,'connect');
   End If;
Exception
   -- When no ACL has been assigned to '*'.
   When No_Data_Found Then
      Dbms_Network_Acl_Admin.Create_Acl('power_users.xml'
                                       ,'ACL that lets power users to connect to everywhere'
                                       ,'APEX_200200'
                                       ,True
                                       ,'connect');
      Dbms_Network_Acl_Admin.Assign_Acl('power_users.xml'
                                       ,'*');
End;
/
 
Commit;
n2 
Declare
   Acl_Path Varchar2(4000);
Begin
   -- Look for the ACL currently assigned to '*' and give APEX_050000
   -- the "connect" privilege if APEX_050000
   --does not have the privilege yet.
   Select Acl
   Into   Acl_Path
   From   Dba_Network_Acls
   Where  Host = '*'
   And    Lower_Port Is Null
   And    Upper_Port Is Null;
   If Dbms_Network_Acl_Admin.Check_Privilege(Acl_Path
                                            ,'APEX_200200'
                                            ,'connect') Is Null Then
      Dbms_Network_Acl_Admin.Add_Privilege(Acl_Path
                                          ,'APEX_200200'
                                          ,True
                                          ,'connect');
   End If;
Exception
   -- When no ACL has been assigned to '*'.
   When No_Data_Found Then
      Dbms_Network_Acl_Admin.Create_Acl('power_users.xml'
                                       ,'ACL that lets power users to connect to everywhere'
                                       ,'APEX_200200'
                                       ,True
                                       ,'connect');
      Dbms_Network_Acl_Admin.Assign_Acl('power_users.xml'
                                       ,'*');
End;
/
 
Commit;
n3

BEGIN
dbms_network_acl_admin.assign_acl(acl => 'power_users.xml',host => '*');
END;
/
after apex installation using apexins 


start apex_rest_config


Make sure to make sys account as 123 some bug .. it only accepts number as password

unlock all your accounts
alter user  account unlock identified by Adoni#123;

alter user APEX_PUBLIC_USER ACCOUNT unlock identified by Adoni#123;
alter user APEX_REST_PUBLIC_USER account unlock identified by Adoni#123;
alter user APEX_PUBLIC_USER ACCOUNT account unlock identified by Adoni#123;
alter user APEX_INSTANCE_ADMIN_USER account unlock identified by Adoni#123;
alter user APEX_INSTANCE_ADMIN_USER account unlock identified by Adoni#123;
alter user APEX_2000200 account unlock identified by Adoni#123;


how memory issues
java -jar  -Xmx800M ords.war install advanced

and that shall make itwork

