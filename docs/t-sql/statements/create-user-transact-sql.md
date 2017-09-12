---
title: "创建用户 (Transact SQL) |Microsoft 文档"
ms.custom:
- SQL2016_New_Updated
ms.date: 07/28/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- WITHOUT_LOGIN_TSQL
- CREATE_USER_TSQL
- SQL13.SWB.DATABASEUSER.OWNEDSCHEMAS.F1
- WITHOUT LOGIN
- CREATE USER
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS
- ALLOW_ENCRYPTED_VALUE_MODIFICATIONS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- adding users
- WITHOUT LOGIN [SQL Server]
- CREATE USER statement
- database user additions [SQL Server]
- USER WITHOUT LOGIN [SQL Server]
- users [SQL Server], adding
- users [SQL Server]
ms.assetid: 01de7476-4b25-4d58-85b7-1118fe64aa80
caps.latest.revision: 111
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47004dfe9ec810fec68a63849755021690f98fdb
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-user-transact-sql"></a>CREATE USER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  向当前数据库添加用户。 使用的最基本的语法示例下面列出了十一种类型的用户：  
  
**用户基于登录名在 master**这是最常见的用户类型。  
  
-   基于登录名基于的 Windows Active Directory 帐户的用户。 `CREATE USER [Contoso\Fritz];`     
-   基于 Windows 组的登录名的用户。 `CREATE USER [Contoso\Sales];`   
-   基于使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的登录名的用户。 `CREATE USER Mary;`  
  
**在数据库进行身份验证的用户**建议以帮助使你的数据库可移植性。  
 始终允许在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。 中包含的数据库中只允许存在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。  
  
-   基于无登录名的 Windows 用户的用户。 `CREATE USER [Contoso\Fritz];`    
-   基于无登录名的 Windows 组的用户。 `CREATE USER [Contoso\Sales];`  
-   中的用户[!INCLUDE[ssSDS](../../includes/sssds-md.md)]或[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]基于 Azure Active Directory 的用户。 `CREATE USER [Contoso\Fritz] FROM EXTERNAL PROVIDER;`     

-   拥有密码的包含数据库用户。 (在中不可用[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]。)`CREATE USER Mary WITH PASSWORD = '********';`   
  
**基于 Windows 主体通过 Windows 组登录名进行连接的用户**  
  
-   基于无登录名但可通过 Windows 组中的成员身份连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]的 Windows 用户的用户。 `CREATE USER [Contoso\Fritz];`  
  
-   基于无登录名但可通过其他 Windows 组中的成员身份连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]的 Windows 组的用户。 `CREATE USER [Contoso\Fritz];`  
  
**无法进行身份验证的用户**这些用户无法登录到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或[!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
-   没有登录名的用户。 不能登录，但可以被授予权限。 `CREATE USER CustomApp WITHOUT LOGIN;`    
-   基于证书的用户。 不能登录，但可以被授予权限，也可以对模块进行签名。 `CREATE USER TestProcess FOR CERTIFICATE CarnationProduction50;`  
-   基于非对称密钥的用户。 不能登录，但可以被授予权限，也可以对模块进行签名。 `CREATE User TestProcess FROM ASYMMETRIC KEY PacificSales09;`   
 
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Syntax Users based on logins in master  
CREATE USER user_name   
    [   
        { FOR | FROM } LOGIN login_name   
    ]  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
--Users that authenticate at the database  
CREATE USER   
    {  
      windows_principal [ WITH <options_list> [ ,... ] ]  
  
    | user_name WITH PASSWORD = 'password' [ , <options_list> [ ,... ]   
    | Azure_Active_Directory_principal FROM EXTERNAL PROVIDER   
    }  
  
 [ ; ]  
  
--Users based on Windows principals that connect through Windows group logins  
CREATE USER   
    {   
          windows_principal [ { FOR | FROM } LOGIN windows_principal ]  
        | user_name { FOR | FROM } LOGIN windows_principal  
}  
    [ WITH <limited_options_list> [ ,... ] ]   
[ ; ]  
  
--Users that cannot authenticate   
CREATE USER user_name   
    {  
         WITHOUT LOGIN [ WITH <limited_options_list> [ ,... ] ]  
       | { FOR | FROM } CERTIFICATE cert_name   
       | { FOR | FROM } ASYMMETRIC KEY asym_key_name   
    }  
 [ ; ]  
  
<options_list> ::=  
      DEFAULT_SCHEMA = schema_name  
    | DEFAULT_LANGUAGE = { NONE | lcid | language name | language alias }  
    | SID = sid   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
<limited_options_list> ::=  
      DEFAULT_SCHEMA = schema_name ]   
    | ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ ON | OFF ] ]  
  
-- SQL Database syntax when connected to a federation member  
CREATE USER user_name  
[;]  
```  

```  
-- Syntax for Azure SQL Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM } { LOGIN login_name }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]

CREATE USER Azure_Active_Directory_principal FROM EXTERNAL PROVIDER  
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]
``` 
  
```  
-- Syntax for Parallel Data Warehouse  
  
CREATE USER user_name   
    [ { { FOR | FROM }  
      {   
        LOGIN login_name   
      }   
      | WITHOUT LOGIN  
    ]   
    [ WITH DEFAULT_SCHEMA = schema_name ]  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *user_name*  
 指定在此数据库中用于识别该用户的名称。 *user_name*是**sysname**。 它的长度最多是 128 个字符。 在创建基于 Windows 主体的用户时，除非指定其他用户名，否则 Windows 主体名称将成为用户名。  
  
 登录名*login_name*  
 指定要为其创建数据库用户的登录名。 *login_name*必须是在服务器中的有效登录名。 可以是基于 Windows 主体（用户或组）的登录名，也可以是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的登录名。 当此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名进入数据库时，它将获取正在创建的这个数据库用户的名称和 ID。 在创建登录名从 Windows 主体映射时，使用格式**[***\<domainName >*  **\\**   *\<loginName >***]**。 有关示例，请参阅[语法摘要](#SyntaxSummary)。  
  
 如果 CREATE USER 语句是 SQL 批处理中唯一的语句，则 Windows Azure SQL Database 将支持 WITH LOGIN 子句。 如果 CREATE USER 语句不是 SQL 批处理中唯一的语句或在动态 SQL 中执行，则不支持 WITH LOGIN 子句。  
  
 DEFAULT_SCHEMA = *schema_name*  
 指定服务器为此数据库用户解析对象名时将搜索的第一个架构。  
  
 *windows_principal*  
 指定正为其创建数据库用户的 Windows 主体。 *Windows_principal*可以是 Windows 用户或 Windows 组。 将创建该用户即使*windows_principal*不具有登录名。 连接到时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，如果*windows_principal*不具有登录名，主体必须在进行身份验证的 Windows[!INCLUDE[ssDE](../../includes/ssde-md.md)]通过 Windows 组的成员具有登录名，或连接字符串必须指定为初始目录包含的数据库。 当从 Windows 主体创建用户，采用格式**[***\<domainName >*  **\\**   *\<loginName >***]**。 有关示例，请参阅[语法摘要](#SyntaxSummary)。 基于 Active Directory 用户的用户仅限于小于 21 个字符的名称。    
  
 *Azure_Active_Directory_principal*  
 **适用于**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]， [!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]。  
  
 指定正在为其创建数据库用户的 Azure Active Directory 主体。 *Azure_Active_Directory_principal*可以是 Azure Active Directory 用户或 Azure Active Directory 组。 (Azure Active Directory 用户不能具有 Windows 身份验证登录名[!INCLUDE[ssSDS](../../includes/sssds-md.md)]; 仅数据库用户。)连接字符串必须指定为初始目录包含的数据库。 

 对于用户，你将使用其主体的域的完整的别名。   
 
-   `CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;`  
  
-   `CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;`

 对于安全组，你使用*显示名称*的安全组。 有关*护士*安全组，你将使用：  
  
-   `CREATE USER [Nurses] FROM EXTERNAL PROVIDER;`  
  
 有关详细信息，请参阅 [使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)。  
  
使用密码 =*密码*  
 **适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 只能在包含数据库中使用。 为正在创建的用户指定密码。 开头[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 存储使用 sha-512 加盐密码的计算密码信息。  
  
WITHOUT LOGIN  
 指定不应将用户映射到现有登录名。  
  
证书*cert_name*  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 指定要为其创建数据库用户的证书。  
  
非对称密钥*asym_key_name*  
 **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 指定要为其创建数据库用户的非对称密钥。  
  
DEFAULT_LANGUAGE = *{NONE |\<lcid > |\<语言名称 > |\<语言别名 >}*  
 **适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。  
  
 为新用户指定默认语言。 如果为用户指定了默认语言并在之后更改数据库的默认语言，则用户的默认语言仍会保留为指定的语言。 如果未指定默认语言，用户的默认语言将为数据库的默认语言。 如果未指定用户的默认语言并在之后更改数据库的默认语言，用户的默认语言将更改为数据库的新默认语言。  
  
> [!IMPORTANT]  
>  *DEFAULT_LANGUAGE*仅用于包含的数据库用户。  
  
SID = *sid*  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 仅适用于包含数据库中具有密码的用户（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证）。 指定新数据库用户的 SID。 如果未选择此选项，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 自动指派 SID。 使用 SID 参数在具有同一标识 (SID) 的多个数据库中创建用户。 若要准备 Always On 故障转移的多个数据库中创建用户时，这很有用。 若要确定用户的 SID，请查询 sys.database_principals。  
  
ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = [ON |**OFF** ]]  
 **适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
 取消在大容量复制操作中的服务器上的加密元数据检查。 这样无需解密数据之间的表或数据库，大容量复制加密数据的用户。 默认为 OFF。  
  
> [!WARNING]  
>  错误使用此选项可能导致数据损坏。 有关详细信息，请参阅[迁移保护的敏感数据的始终加密](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。  
  
## <a name="remarks"></a>注释  
 如果已忽略 FOR LOGIN，则新的数据库用户将被映射到同名的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。  
  
 默认架构将是服务器为此数据库用户解析对象名时将搜索的第一个架构。 除非另外指定，否则默认架构将是此数据库用户创建的对象所属的架构。  
  
 如果用户具有默认架构，则将使用默认架构。 如果用户不具有默认架构，但该用户是具有默认架构的组的成员，则将使用该组的默认架构。 如果用户不具有默认架构而且是多个组的成员，则该用户的默认架构将是具有最低 principle_id 的 Windows 组的架构和一个显式设置的默认架构。 （不可能将可用的默认架构之一显式选作首选架构。）如果没有默认的架构可以确定用户， **dbo**将使用架构。  
  
 DEFAULT_SCHEMA 可在创建它所指向的架构前进行设置。  
  
 在创建映射到证书或非对称密钥的用户时，不能指定 DEFAULT_SCHEMA。  
  
 如果用户是 sysadmin 固定服务器角色的成员，则忽略 DEFAULT_SCHEMA 的值。 sysadmin 固定服务器角色的所有成员都有默认架构 `dbo`。  
  
 WITHOUT LOGIN 子句可创建不映射到 SQL Server 登录名的用户。 它可以作为 guest 连接到其他数据库。 可以将权限分配给这一没有登录名的用户，当安全上下文更改为没有登录名的用户时，原始用户将收到无登录名用户的权限。 请参阅示例[D.创建和使用不具有登录名的用户](#withoutLogin)。  
  
 只有映射到 Windows 主体的用户可以包含反斜杠字符 (**\\**)。  
  
 不能使用 CREATE USER 创建 guest 用户，因为每个数据库中均已存在 guest 用户。 可通过授予 guest 用户 CONNECT 权限来启用该用户，如下所示：  
  
```  
GRANT CONNECT TO guest;  
GO  
```  
  
 数据库用户的信息会显示在[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)目录视图。  
  
##  <a name="SyntaxSummary"></a>语法摘要  
 **基于在母版中的登录名的用户**  
  
 下面的列表显示基于登录名的用户的可能语法。 未列出默认架构选项。  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FOR LOGIN SQLAUTHLOGIN`  
-   `CREATE USER SQLAUTHLOGIN FROM LOGIN SQLAUTHLOGIN`  
  
**在数据库进行身份验证的用户**  
  
 下面的列表显示只能在包含数据库中使用的用户的可能语法。 创建的用户将不与中的任何登录名相关**master**数据库。 未列出默认架构和语言选项。  
  
> [!IMPORTANT]  
>  此语法授予用户对数据库的访问权限，并且还将授予对[!INCLUDE[ssDE](../../includes/ssde-md.md)]的新访问权限。  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER Barry WITH PASSWORD = 'sdjklalie8rew8337!$d'`  
  
**基于 Windows 主体不具有在母版中的登录名的用户**  
  
 以下列表显示为有权访问的用户可能语法[!INCLUDE[ssDE](../../includes/ssde-md.md)]通过 Windows 组，但没有登录名**master**。 此语法可用于所有类型的数据库中。 未列出默认架构和语言选项。  
  
 此语法与基于 master 数据库中登录名的用户相似，但此用户类别在 master 中没有登录名。 该用户必须可以通过 Windows 组登录名访问[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
 此语法类似于基于 Windows 主体的包含数据库用户，但此用户类别未获得对[!INCLUDE[ssDE](../../includes/ssde-md.md)]的新访问权限。  
  
-   `CREATE USER [Domain1\WindowsUserBarry]`  
-   `CREATE USER [Domain1\WindowsUserBarry] FOR LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsUserBarry] FROM LOGIN Domain1\WindowsUserBarry`  
-   `CREATE USER [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FOR LOGIN [Domain1\WindowsGroupManagers]`  
-   `CREATE USER [Domain1\WindowsGroupManagers] FROM LOGIN [Domain1\WindowsGroupManagers]`  
  
**无法进行身份验证的用户**  
  
 下面的列表显示无法登录 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的用户的可能语法。  
  
-   `CREATE USER RIGHTSHOLDER WITHOUT LOGIN`  
-   `CREATE USER CERTUSER FOR CERTIFICATE SpecialCert`  
-   `CREATE USER CERTUSER FROM CERTIFICATE SpecialCert`  
-   `CREATE USER KEYUSER FOR ASYMMETRIC KEY SecureKey`  
-   `CREATE USER KEYUSER FROM ASYMMETRIC KEY SecureKey`  
  
## <a name="security"></a>安全性  
 创建用户会授予对数据库的访问权限，但不会自动授予对数据库中对象的任何访问权限。 创建用户后，常见操作是将用户添加到有权访问数据库对象的数据库角色中或向用户授予对象权限。 有关设计权限系统的信息，请参阅 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
### <a name="special-considerations-for-contained-databases"></a>包含数据库的特殊注意事项  
 当连接到包含数据库中，如果用户没有登录名**master**数据库，则连接字符串必须包含为初始目录包含的数据库名称。 拥有密码的包含数据库用户始终需要使用初始目录参数。  
  
 在包含数据库中，创建用户有助于将数据库与[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例分离，以便可以轻松地将数据库移动到其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中。 有关详细信息，请参阅[Contained Databases](../../relational-databases/databases/contained-databases.md)和[包含数据库用户-使你数据库可移植](../../relational-databases/security/contained-database-users-making-your-database-portable.md)。 若要更改的数据库用户从基于用户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证登录到包含的数据库用户使用密码，请参阅[sp_migrate_user_to_contained &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql.md).  
  
 在包含数据库中，用户无需具有登录名**master**数据库。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]管理员应该了解，可在数据库级别而非[!INCLUDE[ssDE](../../includes/ssde-md.md)]级别授予对包含数据库的访问权限。 有关详细信息，请参阅 [Security Best Practices with Contained Databases](../../relational-databases/databases/security-best-practices-with-contained-databases.md)。  
  
 对 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 使用包含的数据库用户时，使用数据库级别防火墙规则（而不服务器级别防火墙规则）配置访问权限。 有关详细信息，请参阅[sp_set_database_firewall_rule &#40;Azure SQL Database &#41;](../../relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database.md).
 
有关[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]和[!INCLUDE[ssSDW_md](../../includes/sssdw-md.md)]包含的数据库用户，SSMS 可以支持多因素身份验证。 有关详细信息，请参阅 [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](https://azure.microsoft.com/documentation/articles/sql-database-ssms-mfa-authentication/)（SSMS 支持使用 SQL 数据库和 SQL 数据仓库的 Azure AD MFA）。  
  
### <a name="permissions"></a>Permissions  
 需要对数据库具有 ALTER ANY USER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-database-user-based-on-a-sql-server-login"></a>A. 基于 SQL Server 登录名创建数据库用户  
 下面的示例首先创建一个名为 `AbolrousHazem` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，然后在 `AbolrousHazem` 中创建对应的数据库用户 `AdventureWorks2012`。  
  
```  
CREATE LOGIN AbolrousHazem   
    WITH PASSWORD = '340$Uuxwp7Mcxo7Khy';  
```   
将更改为用户数据库。 例如，在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用`USE AdventureWorks2012`语句。 在[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，必须建立新连接到用户数据库。

```   
CREATE USER AbolrousHazem FOR LOGIN AbolrousHazem;  
GO   
```  
  
### <a name="b-creating-a-database-user-with-a-default-schema"></a>B. 创建具有默认架构的数据库用户  
 下面的示例首先创建名为 `WanidaBenshoof` 且具有密码的服务器登录名，然后创建具有默认架构 `Wanida` 的对应数据库用户 `Marketing`。  
  
```  
CREATE LOGIN WanidaBenshoof   
    WITH PASSWORD = '8fdKJl3$nlNv3049jsKK';  
USE AdventureWorks2012;  
CREATE USER Wanida FOR LOGIN WanidaBenshoof   
    WITH DEFAULT_SCHEMA = Marketing;  
GO  
```  
  
### <a name="c-creating-a-database-user-from-a-certificate"></a>C. 从证书创建数据库用户  
 下面的示例从证书 `JinghaoLiu` 创建数据库用户 `CarnationProduction50`。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE AdventureWorks2012;  
CREATE CERTIFICATE CarnationProduction50  
    WITH SUBJECT = 'Carnation Production Facility Supervisors',  
    EXPIRY_DATE = '11/11/2011';  
GO  
CREATE USER JinghaoLiu FOR CERTIFICATE CarnationProduction50;  
GO   
```  
  
###  <a name="withoutLogin"></a> D. 创建和使用不含登录名的用户  
 以下示例创建一个数据库用户 `CustomApp`，该用户不映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 然后，该示例向用户 `adventure-works\tengiz0` 授予相应的权限以便模拟 `CustomApp` 用户。  
  
```  
USE AdventureWorks2012 ;  
CREATE USER CustomApp WITHOUT LOGIN ;  
GRANT IMPERSONATE ON USER::CustomApp TO [adventure-works\tengiz0] ;  
GO   
```  
  
 为了使用 `CustomApp` 凭据，用户 `adventure-works\tengiz0` 执行以下语句。  
  
```  
EXECUTE AS USER = 'CustomApp' ;  
GO  
```  
  
 为了恢复到 `adventure-works\tengiz0` 凭据，该用户执行以下语句。  
  
```  
REVERT ;  
GO  
```  
  
### <a name="e-creating-a-contained-database-user-with-password"></a>E. 创建拥有密码的包含数据库用户  
 下面的示例创建一个拥有密码的包含数据库用户。 该示例只能在包含数据库中执行。  
  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。 如果删除了 DEFAULT_LANGUAGE，则此示例可在 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 中正常运行。  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER Carlo  
WITH PASSWORD='RN92piTCh%$!~3K9844 Bl*'  
    , DEFAULT_LANGUAGE=[Brazilian]  
    , DEFAULT_SCHEMA=[dbo]  
GO   
```  
  
### <a name="f-creating-a-contained-database-user-for-a-domain-login"></a>F. 为域登录名创建包含数据库用户  
 下面的示例为 Contoso 域中名为 Fritz 的登录名创建一个包含数据库用户。 该示例只能在包含数据库中执行。  
  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER [Contoso\Fritz] ;  
GO   
```  
  
### <a name="g-creating-a-contained-database-user-with-a-specific-sid"></a>G. 创建具有特定 SID 的包含数据库用户  
 下面的示例创建名为 CarmenW 的 SQL Server 经过身份验证的包含数据库用户。 该示例只能在包含数据库中执行。  
  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE AdventureWorks2012 ;  
GO  
CREATE USER CarmenW WITH PASSWORD = 'a8ea v*(Rd##+'  
, SID = 0x01050000000000090300000063FF0451A9E7664BA705B10E37DDC4B7;  
  
```  
  
### <a name="h-creating-a-user-to-copy-encrypted-data"></a>H. 创建用户复制加密的数据  
 下面的示例创建用户，可以将其复制的表，一个集合中的始终加密功能通过受保护的数据包含加密的列，到另一台具有 （相同或不同的数据库） 中的加密列的表。  有关详细信息，请参阅[迁移保护的敏感数据的始终加密](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。  
  
**适用于**:[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]， [!INCLUDE[ssSDS](../../includes/sssds-md.md)]。  
  
```  
CREATE USER [Chin]   
WITH   
      DEFAULT_SCHEMA = dbo  
    , ALLOW_ENCRYPTED_VALUE_MODIFICATIONS = ON ;  
```  
  

## <a name="next-steps"></a>后续步骤  
一旦创建了用户，请考虑将用户添加到数据库角色使用[ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md)语句。  
你可能还想到[GRANT 对象权限](../../t-sql/statements/grant-object-permissions-transact-sql.md)到角色，以便他们可以访问表。 有关 SQL Server 安全模型的常规信息，请参阅[权限](../../relational-databases/security/permissions-database-engine.md)。   
  
## <a name="see-also"></a>另请参阅  
 [创建数据库用户](../../relational-databases/security/authentication-access/create-a-database-user.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [ALTER USER (Transact-SQL)](../../t-sql/statements/alter-user-transact-sql.md)   
 [删除用户 &#40;Transact SQL &#41;](../../t-sql/statements/drop-user-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [包含的数据库](../../relational-databases/databases/contained-databases.md)   
 [使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)   
 [数据库引擎权限入门](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)  
  
  


