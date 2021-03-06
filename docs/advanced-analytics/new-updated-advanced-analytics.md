---
title: Updated - Advanced Analytics for SQL Server docs | Microsoft Docs
description: Display snippets of updated content for recently changed in documentation, for Advanced Analytics for Microsoft SQL Server.

author: "HeidiSteen"
ms.author: "heidist"
manager: "cgronlun"
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified

ms.component: advanced-analytics
ms.date: 02/03/2018
---
# New and Recently Updated: Advanced Analytics for SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Nearly every day Microsoft updates some of its existing articles on its [Docs.Microsoft.com](http://docs.microsoft.com/) documentation website. This article displays excerpts from recently updated articles. Links to new articles might also be listed.

This article is generated by a program that is rerun periodically. Occasionally an excerpt can appear with imperfect formatting, or as markdown from the source article. Images are never displayed here.

Recent updates are reported for the following date range and subject:



- *Date range of updates:* &nbsp; **2017-12-03** &nbsp; -to- &nbsp; **2018-02-03**
- *Subject area:* &nbsp; **Advanced Analytics for SQL Server**.

<!-- Repo = 'MicrosoftDocs/sql-docs'.   Branch = 'live'. -->



&nbsp;

## New Articles Created Recently

The following links jump to new articles that have been added recently.


1. [Install new Python packages on SQL Server](python/install-additional-python-packages-on-sql-server.md)



&nbsp;

## Updated Articles with Excerpts

This section displays the excerpts of updates gathered from articles that have recently experienced a large update.

The excerpts displayed here appear separated from their proper semantic context. Also, sometimes an excerpt is separated from important markdown syntax that surrounds it in the actual article. Therefore these excerpts are for general guidance only. The excerpts only enable you to know whether your interests warrant taking the time to click and visit the actual article.

For these and other reasons, do not copy code from these excerpts, and do not take as exact truth any text excerpt. Instead, visit the actual article.





&nbsp;

<a name="compactupdatedlist"/>

### Compact List of Articles Updated Recently

This compact list provides links to all the updated articles that are listed in the Excerpts section.

1. [Known issues in Machine Learning Services](#TitleNum_1)
2. [Converting R code for execution in-database](#TitleNum_2)
3. [Determine which R packages are installed on SQL Server](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### 1. &nbsp; [Known issues in Machine Learning Services](known-issues-for-sql-server-machine-learning-services.md)

*Updated: 2018-02-02* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 163.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c6f46adcf795c43f818120b88407a3a89304cb27 c781562605f5cd77f6c43bfe5e89810cb72ceae0  (PR=4789  ,  Filename=known-issues-for-sql-server-machine-learning-services.md  ,  Dirpath=docs\advanced-analytics\  ,  MergeCommitSha40=386bfb688843bac7fa4d83dc1cfef94dd19db110) -->



For additional known issues that might affect R solutions, see the [Machine Learning Server](https://docs.microsoft.com/machine-learning-server/resources-known-issues) site.

**Access denied warning when executing R scripts on SQL Server in a non default location**


If the instance of SQL Server has been installed to a non-default location, such as outside the `Program Files` folder, the warning ACCESS_DENIED is raised when you try to run scripts that install a package. For example:

> *In normalizePath(path.expand(path), winslash, mustWork) : path[2]="~ExternalLibraries/R/8/1": Access is denied*

The reason is that an R function attempts to read the path, and fails if the built-in users group **SQLRUserGroup**, does not have read access. The warning that is raised does not block execution of the current R script, but the warning might recur repeatedly whenever the user runs any other R script.

If you have installed SQL Server to the default location, this error does not occur, because all Windows users have read permissions on the `Program Files` folder.

This issue will be addressed in an upcoming service release. As a workaround, provide the group, **SQLRUserGroup**, with read access for all parent folders of `ExternalLibraries`.

**Serialization error between old and new versions of RevoScaleR**


When you pass a model using a serialized format to a remote SQL Server instance, you might get the error:

> *Error in memDecompress(data, type = decompress) internal error -3 in memDecompress(2).*

This error is raised if you saved the model using a recent version of the serialization function, [rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel), but the SQL Server instance where you deserialize the model has an older version of the RevoScaleR APIs, from SQL Server 2017 CU2 or earlier.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### 2. &nbsp; [Converting R code for execution in-database](r/converting-r-code-for-use-in-sql-server.md)

*Updated: 2018-01-08* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1) | [Next](#TitleNum_3))

<!-- Source markdown line 136.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a1d156fac1af5813ef75965071686b177e2aede7 fc8beff0aa0d7ea298e493b90984875e81e9143e  (PR=4493  ,  Filename=converting-r-code-for-use-in-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=f486d12078a45c87b0fcf52270b904ca7b0c7fc8) -->



**Package your R code in a stored procedure**

+ If your code is relatively simple, you can embed it in a T-SQL user-defined function without modification, as described in these samples:

    + [Create an R function that runs in rxExec](r/../tutorials/deepdive-create-a-simple-simulation.md)
    + [Feature engineering using T-SQL and R](r/../tutorials/sqldev-create-data-features-using-t-sql.md)

+ If the code is more complex, use the R package **sqlrutils** to convert your code. This package is designed to help experienced R users write good stored procedure code.

    The first step is to rewrite your R code as a single function with clearly defined inputs and outputs.

    Then, use the **sqlrutils** package to generate the input and outputs in the correct format. The **sqlrutils** package generates the complete stored procedure code for you, and can also register the stored procedure in the database.

    For more information and examples, see [SqlRUtils](r/../r/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md).

**Integrate with other workflows**

+ Leverage T-SQL tools and ETL processes. Perform feature engineering, feature extraction, and data cleansing in advance as part of data workflows.

    When you are working in a dedicated R development environment such as R Tools for Visual Studio or RStudio, you might pull data to your computer, analyze the data iteratively, and then write out or display the results.

    However, when standalone R code is migrated to SQL Server, much of this process can be simplified or delegated to other SQL Server tools.

+ Use secure, asynchronous visualization strategies.

    Users of SQL Server often cannot access files on the server, and SQL client tools typically do not support the R graphics device. If you generate plots or other graphics as part of the solution, consider exporting the plots as binary data and saving to a table, or writing.



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### 3. &nbsp; [Determine which R packages are installed on SQL Server](r/determine-which-packages-are-installed-on-sql-server.md)

*Updated: 2018-01-24* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_2))

<!-- Source markdown line 78.  ms.author= "jeannt".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9a065066398843a4bed318fa46d4982d712915a9 7a1df11f57e7bbf0abc37d3aa240dedd2b88c45f  (PR=4715  ,  Filename=determine-which-packages-are-installed-on-sql-server.md  ,  Dirpath=docs\advanced-analytics\r\  ,  MergeCommitSha40=9e6a029456f4a8daddb396bc45d7874a43a47b45) -->




**Get library location and version**


The following example gets the library location of RevoScaleR in the local compute context, and the package version.

```
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

**Determine path of library used by SQL Server**


If you have upgraded the machine learning components using binding, the path to the R library might change. When this happens, previous shortcuts to R tools might reference an earlier version. To be sure of the path and package version used by SQL Server, you can run a command such as the following:

```
EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    sql_r_path <- rxSqlLibPaths("local")
	  print(sql_r_path)
    version_info <-packageVersion("RevoScaleR")
	  print(version_info)'
```

**Results**

```
STDOUT message(s) from external script:
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```







## Similar articles about new or updated articles

This section lists very similar articles for recently updated articles in other subject areas, within our public GitHub.com repository: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).


#### Subject areas that *do* have new or recently updated articles


- [New + Updated (1+3):&nbsp; **Advanced Analytics for SQL** docs](../advanced-analytics/new-updated-advanced-analytics.md)
- [New + Updated (0+1):&nbsp; **Analytics Platform System for SQL** docs](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [New + Updated (0+1):&nbsp; **Connect to SQL** docs](../connect/new-updated-connect.md)
- [New + Updated (0+1):&nbsp; **Database Engine for SQL** docs](../database-engine/new-updated-database-engine.md)
- [New + Updated (12+1): **Integration Services for SQL** docs](../integration-services/new-updated-integration-services.md)
- [New + Updated (6+2):&nbsp; **Linux for SQL** docs](../linux/new-updated-linux.md)
- [New + Updated (15+0): **PowerShell for SQL** docs](../powershell/new-updated-powershell.md)
- [New + Updated (2+9):&nbsp; **Relational Databases for SQL** docs](../relational-databases/new-updated-relational-databases.md)
- [New + Updated (1+0):&nbsp; **Reporting Services for SQL** docs](../reporting-services/new-updated-reporting-services.md)
- [New + Updated (1+1):&nbsp; **SQL Operations Studio** docs](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [New + Updated (1+1):&nbsp; **Microsoft SQL Server** docs](../sql-server/new-updated-sql-server.md)
- [New + Updated (0+1):&nbsp; **SQL Server Data Tools (SSDT)** docs](../ssdt/new-updated-ssdt.md)
- [New + Updated (1+2):&nbsp; **SQL Server Management Studio (SSMS)** docs](../ssms/new-updated-ssms.md)
- [New + Updated (0+2):&nbsp; **Transact-SQL** docs](../t-sql/new-updated-t-sql.md)



#### Subject areas that do *not* have any new or recently updated articles


- [New + Updated (0+0): **Data Migration Assistant (DMA) for SQL** docs](../dma/new-updated-dma.md)
- [New + Updated (0+0): **ActiveX Data Objects (ADO) for SQL** docs](../ado/new-updated-ado.md)
- [New + Updated (0+0): **Analysis Services for SQL** docs](../analysis-services/new-updated-analysis-services.md)
- [New + Updated (0+0): **Data Quality Services for SQL** docs](../data-quality-services/new-updated-data-quality-services.md)
- [New + Updated (0+0): **Data Mining Extensions (DMX) for SQL** docs](../dmx/new-updated-dmx.md)
- [New + Updated (0+0): **Master Data Services (MDS) for SQL** docs](../master-data-services/new-updated-master-data-services.md)
- [New + Updated (0+0): **Multidimensional Expressions (MDX) for SQL** docs](../mdx/new-updated-mdx.md)
- [New + Updated (0+0): **ODBC (Open Database Connectivity) for SQL** docs](../odbc/new-updated-odbc.md)
- [New + Updated (0+0): **Samples for SQL** docs](../sample/new-updated-sample.md)
- [New + Updated (0+0): **SQL Server Migration Assistant (SSMA)** docs](../ssma/new-updated-ssma.md)
- [New + Updated (0+0): **Tools for SQL** docs](../tools/new-updated-tools.md)
- [New + Updated (0+0): **XQuery for SQL** docs](../xquery/new-updated-xquery.md)


