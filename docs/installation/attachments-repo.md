# Attachments repository

From Squash TM 1.18.0 release, it was made possible to store attachments outside the database directly in a file system. By default, the storage of attachments remains within the database because this is the simplest solution, and because it fits standard data quantities perfectly.

For a new installation of Squash TM, only a configuration is necessary for you to benefit from this new means of storage.
On an existing instance, you will first need to extract the existing attachments before you change the configuration.

!!! WARNING
    Changing from a storage in a database to a file storage does have consequences, more specifically concerning data back-ups. The system administrator therefore absolutely needs to make the necessary modifications as follows:
    - make sure you think of an attachment back-up system which works simultaneously with the database system
    - make sure you have enough space to store the attachments and follow the evolution of this space
    - give the right to read and write to the user launching the Squash TM process on the repository you picked to store the attachments

## Configuration

!!! WARNING
    If you already have existing attachements in a database, you absolutely need to extract them BEFORE you change the Squash TM configuration.

`~SQUASH` is the deployment repository of Squash TM

1. Stop Squash and edit the file squash.tm.cfg.properties within the ~SQUASH/conf repository
2. Add the squashtm.feature.file.repository = true attribute
3. Optionally, add the attribute squash.path.file.repository=<Chosen path for the repository storage>. This step is necessary after the database attachments were extracted. By default, if this attribute is absent, Squash TM will store the attachments within the ~SQUASH/attachments repository
4. Make all necessary system modifications, especially of the chosen path is not the default path (this targets more specifically the attribution of rights to the user, who needs to be allowed to write and edit the processes not only from the side of Squash, but also from the side of the machine)
5. Relaunch Squash TM
6. Make a test from the application by downloading an existing attachment. Add a new attachment, download it, and then erase it

## Extracting the existing attachments

If you decide to change from a database storage to a file system storage on an existing Squash TM installation, you need to migrate the attachments from your database towards the file format supported by Squash TM.

A migration tool made by Henix is available at : http://repo.squashtest.org/distribution

!!! WARNING
Save your database BEFORE you start the migration procedure, so as to still be able to restore it in case you should have a problem

### Process on Windows

1. Stop Squash TM
2. Unzip the tool. If you wish to keep the default attachement storing path, you may directly unzip the tool in the Squash TM root repository and not change REPO_PATH. Your attachements will be directly put in your file (~SQUASH/squash-tm-extract-attachment-tool/attachments)
3. Edit the file extract-attachment.bat
4. Find the following lines:
   ```shell
    set DB_TYPE=h2
    set DB_URL=jdbc:h2:./data/squash-tm
    set DB_USERNAME=sa
    set DB_PASSWORD=sa
    ```
    Edit with the needed values to access the database of your Squash TM instance. They should all be similar to the ones in your Squash TM startup script.
5. Find the following line:
          REPO_PATH=./attachments
   Edit path if necessary. The attachments will be extracted in this repository.
6. Run the file extract-attachment.bat
    The migration starts automatically. It involves three steps:
    - the extraction of the attachments
    - the verification of the extracted files
    - the deletion of the attachements in the database
7. Once the migration is finished, please configure Squash TM as indicated in section 6.1


### Process on Linux

1. Stop Squash TM
2. Unzip the tool. If you wish to keep the default attachement storing path, you may directly unzip the tool in the Squash TM root repository and not change REPO_PATH. Your attachements will be directly put in your file (~SQUASH/attachments)
3. Edit the file extract-attachment.sh
4. Find the following lines:
   ```sql 
    DB_TYPE=h2
    DB_URL=jdbc:h2:../data/squash-tm
    DB_USERNAME=sa
    DB_PASSWORD=sa
    ```
    Edit with the needeed values to access the database of your Squash TM instance. They should all be similar to the ones in your Squash TM startup script.
5. Find the following line: REPO_PATH=./attachments
   Edit path if necessary. The attachments will be extracted in this repository.
6. Run the file extract-attachment.sh
   The migration starts automatically. It involves three steps:
    - the extraction of the attachments
    - the verification of the extracted files
    - the deletion of the attachements in the database
7. Once the migration is finished, please configure Squash TM as indicated in section 6.1

### Post-migration

Depending on the RDBMS, you might need to maintain the database to free the disk space the attachments take, even if the migrator deleted them by means of SQL requests. For instance, vacuumlo or vaccumdb for the PostgreSQL database, or to execute an «optimize table» from the Table Inspector for the MySQL database. 
Please see the documentation regarding your RDBMS for more information.