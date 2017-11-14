# utl_variable_and_table_attributes_at_compile_time
Variable and table attributes, length/type/format/informat/label/number of variables at compile time

    ```  Variable and table attributes, length/type/format/informat/label/number of variables at compile time                                                         ```
    ```                                                                                                                                                               ```
    ```     INPUT                                                                                                                                                     ```
    ```     =====                                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```       data iris;                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```         set sashelp.iris;                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```         informat SEPALLENGTH 5.;                                                                                                                              ```
    ```         format SEPALLENGTH 3.;                                                                                                                                ```
    ```         length SEPALLENGTH 3;                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```       run;quit;                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```     WORKING CODE                                                                                                                                              ```
    ```     ============                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```         %put Number of vars               =   %utl_varcount(iris);                                                                                            ```
    ```         %put Sepallength type             =   %utl_vartype(iris,sepallength);                                                                                 ```
    ```         %put Sepallength length in bytes  =   %utl_varlen(iris,sepallength);                                                                                  ```
    ```         %put Sepallength format           =   %utl_varfmt(iris,sepallength);                                                                                  ```
    ```         %put Sepallength label            =   %utl_varlabel(iris,sepallength);                                                                                ```
    ```         %put Sepallength informat         =   %utl_varinfmt(iris,sepallength);                                                                                ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```     WANT this information at compile time                                                                                                                     ```
    ```     ======================================                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```        Number of vars               =   5                                                                                                                     ```
    ```        Sepallength type             =   N                                                                                                                     ```
    ```        Sepallength length in bytes  =   3                                                                                                                     ```
    ```        Sepallength format           =   3.                                                                                                                    ```
    ```        Sepallength label            =   Sepal Length (mm)                                                                                                     ```
    ```        Sepallength informat         =   5.                                                                                                                    ```
    ```                                                                                                                                                               ```
    ```  *                _                _       _                                                                                                                  ```
    ```   _ __ ___   __ _| | _____      __| | __ _| |_ __ _                                                                                                           ```
    ```  | '_ ` _ \ / _` | |/ / _ \    / _` |/ _` | __/ _` |                                                                                                          ```
    ```  | | | | | | (_| |   <  __/   | (_| | (_| | || (_| |                                                                                                          ```
    ```  |_| |_| |_|\__,_|_|\_\___|    \__,_|\__,_|\__\__,_|                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```       data iris;                                                                                                                                              ```
    ```                                                                                                                                                               ```
    ```         set sashelp.iris;                                                                                                                                     ```
    ```                                                                                                                                                               ```
    ```         informat SEPALLENGTH 5.;                                                                                                                              ```
    ```         format SEPALLENGTH 3.;                                                                                                                                ```
    ```         length SEPALLENGTH 3;                                                                                                                                 ```
    ```                                                                                                                                                               ```
    ```       run;quit;                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  *          _       _   _                                                                                                                                     ```
    ```   ___  ___ | |_   _| |_(_) ___  _ __                                                                                                                          ```
    ```  / __|/ _ \| | | | | __| |/ _ \| '_ \                                                                                                                         ```
    ```  \__ \ (_) | | |_| | |_| | (_) | | | |                                                                                                                        ```
    ```  |___/\___/|_|\__,_|\__|_|\___/|_| |_|                                                                                                                        ```
    ```                                                                                                                                                               ```
    ```  ;                                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```                                                                                                                                                               ```
    ```  %macro utl_vartype(dsn,var)/des="Variable type returns N or C";                                                                                              ```
    ```    %local dsid posv rc;                                                                                                                                       ```
    ```     %let dsid = %sysfunc(open(&dsn,i));                                                                                                                       ```
    ```     %let posv = %sysfunc(varnum(&dsid,&var));                                                                                                                 ```
    ```     %sysfunc(vartype(&dsid,&posv))                                                                                                                            ```
    ```     %let rc = %sysfunc(close(&dsid));                                                                                                                         ```
    ```  %mend utl_vartype;                                                                                                                                           ```
    ```                                                                                                                                                               ```
    ```  %macro utl_varlen(dsn,var)/des="Variable length";                                                                                                            ```
    ```    %local dsid posv rc;                                                                                                                                       ```
    ```     %let dsid = %sysfunc(open(&dsn,i));                                                                                                                       ```
    ```     %let posv = %sysfunc(varnum(&dsid,&var));                                                                                                                 ```
    ```     %sysfunc(varlen(&dsid,&posv))                                                                                                                             ```
    ```     %let rc = %sysfunc(close(&dsid));                                                                                                                         ```
    ```  %mend utl_varlen;                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  %macro utl_varfmt(dsn,var)/des="Variable format";                                                                                                            ```
    ```    %local dsid posv rc;                                                                                                                                       ```
    ```     %let dsid = %sysfunc(open(&dsn,i));                                                                                                                       ```
    ```     %let posv = %sysfunc(varnum(&dsid,&var));                                                                                                                 ```
    ```     %sysfunc(varfmt(&dsid,&posv))                                                                                                                             ```
    ```     %let rc = %sysfunc(close(&dsid));                                                                                                                         ```
    ```  %mend utl_varfmt;                                                                                                                                            ```
    ```                                                                                                                                                               ```
    ```  %macro utl_varinfmt(dsn,var)/des="Variable informat";                                                                                                        ```
    ```    %local dsid posv rc;                                                                                                                                       ```
    ```     %let dsid = %sysfunc(open(&dsn,i));                                                                                                                       ```
    ```     %let posv = %sysfunc(varnum(&dsid,&var));                                                                                                                 ```
    ```     %sysfunc(varinfmt(&dsid,&posv))                                                                                                                           ```
    ```     %let rc = %sysfunc(close(&dsid));                                                                                                                         ```
    ```  %mend utl_varinfmt;                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  %macro utl_varlabel(dsn,var)/des="Variable label";                                                                                                           ```
    ```    %local dsid posv rc;                                                                                                                                       ```
    ```     %let dsid = %sysfunc(open(&dsn,i));                                                                                                                       ```
    ```     %let posv = %sysfunc(varnum(&dsid,&var));                                                                                                                 ```
    ```     %sysfunc(varlabel(&dsid,&posv))                                                                                                                           ```
    ```     %let rc = %sysfunc(close(&dsid));                                                                                                                         ```
    ```  %mend utl_varlabel;                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  %macro utl_varcount(dsn)/des="Number of variables";                                                                                                          ```
    ```    %local dsid posv rc;                                                                                                                                       ```
    ```      %let dsid = %sysfunc(open(&dsn,i));                                                                                                                      ```
    ```      %sysfunc(attrn(&dsid,NVARS));                                                                                                                            ```
    ```      %let rc = %sysfunc(close(&dsid));                                                                                                                        ```
    ```  %mend utl_varcount;                                                                                                                                          ```
    ```                                                                                                                                                               ```
    ```  %utlnopts;                                                                                                                                                   ```
    ```  %put Number of vars               =   %utl_varcount(iris);                                                                                                   ```
    ```  %put Sepallength type             =   %utl_vartype(iris,sepallength);                                                                                        ```
    ```  %put Sepallength length in bytes  =   %utl_varlen(iris,sepallength);                                                                                         ```
    ```  %put Sepallength format           =   %utl_varfmt(iris,sepallength);                                                                                         ```
    ```  %put Sepallength label            =   %utl_varlabel(iris,sepallength);                                                                                       ```
    ```  %put Sepallength informat         =   %utl_varinfmt(iris,sepallength);                                                                                       ```
    ```  %utlopts;                                                                                                                                                    ```

