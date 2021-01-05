GitHub limits files to 100 mb. Be very careful storing data of any consequential size in here as it will break your repository.

- data/postgresql is ignored as this will have large postgres databases.
- data/spark-warehouse is ignored as this will have large spark files.
- data/Open990 is ignored as well.
- data/big is also ignored.

Makes sure any files bigger than 100 mb are not included in the base data directory.  If you add another folder with big files, you will need to add it to the `.gitignore`.