j2recover can be used to restore deleted files for mounted or unmounted jfs2 file system.

When j2recover is used for unmounted file system,
it will try best to recover inodes in their original location(i.e, no copy action),
thus greatly improved the performance since it minimized the IO activity,
and this feature also greatly saved disk space for restore.

Sometimes some file systems of production system can not be unmounted even files are wrongly deleted.
In such case j2recover can be used for mounted file system,
and j2recover will copy restored files to specified location.

Sometimes deleted files maybe has been overwritten by other files.
But some files(such as text file) might still valuable even it has been partially overwritten.
j2recover can also restore deleted files even they are partially or totally overwritten.
And j2recover will report what blocks are overwritten in the file.  
Thus user can check the file and get those valuable data without overwriting.

To recover complete file as much as possible, user may run j2recover with following option:
./j2recover -c <copydir> /dev/lvname

To recover data as much as possible, user may run j2recover with following option:
./j2recover -c <copydir> -p all -x <partialdir> /dev/lvname


Usage:
j2recover [--fast | -f] [--rptonly | -r] [--wrstate | -s] [--rdstate | -u] [--inofile | -i :filename] [--lfdir | -L :dirname]
          [--copydir | -c :dirname] [--partdir | -x :dirname] [--output | -o:filename] [--partial | -p :no|yes|all] <file system>

Options:
        --fast    | -f   Only scan inodes (exclude blocks). Some files might be not found.
        --rptmode | -r   List what file could be restored.
        --cpmode  | -m   Copy all restored files to user specified directory.
        --wrstate | -s   Save satus in report mode.
        --rdstate | -u   Use satus file generated in report mode.
        --partial | -p   'no'   only scan complete file. This is default.
                         'yes'  also scan partial file(but skip full-overwritten file).
                         'all'  scan all files(include full-overwritten file).
        --lfdir   | -L   Where to store complete files in original fs, default is '//lost+found'
        --copydir | -c   Where to copy complete files in other fs. No default value
        --partdir | -x   Where to copy partial files in other fs. No default value
        --inofile | -i   Input file which contains inode number that need to be restored
        --output  | -o   Report file, default is '/var/j2recover/report.log'
        --keyfile | -k   License file, default is './license.key'
