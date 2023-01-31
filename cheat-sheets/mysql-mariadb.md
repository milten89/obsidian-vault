# MySQL and MariaDB common fixes

## Recover database from system that can't boot

1. Copy database files

    Extract all **IDB** files located on failing device. Files should be located in:

    - **MySQL** - `C:\ProgramData\MySQL\MySQL Server [version]\Data\[database name]`
    - **MariaDB**- `TBD`

2. Recreate database schema

    You need to recreate database schema manually. Without valid schema files can't be imported or data will be corrupted.

3. Delete the new **IBD** File

    Run the following command to delete the new **IBD** file:

    ```sql
    ALTER TABLE [table name] DISCARD TABLESPACE;
    ```

    This command breaks the link between **MySQL** and the tablespace to remove the **IBD** file.

4. Copy the old **IBD** file

    Now, copy the original **IBD** file in the new database.

5. Import the Tablespace

    Restore the link between the **MySQL** table and the tablespace by executing the below command:

    ```sql
    ALTER TABLE [table name] IMPORT TABLESPACE;
    ```

    Depends of complexity of database or table recreation order, there is a chance of error `Error Code: 1451. Cannot delete or update a parent row: a foreign key constraint fails ()`. To disable foreign key constraint check use command 

    ```sql
    SET foreign_key_checks = 0;
    ```

    and after import use

    ```sql
    SET foreign_key_checks = 1;
    ```

    to enable constraint.
