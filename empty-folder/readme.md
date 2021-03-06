# Empty Folder
This Jenkins pipeline script uses Groovy to empty a given folder. This script was written for a Windows environment where Robocopy is used as the underlying tool to perform the actually deletion of the folders. Folders are assumed to be located in a shared folder location on a network. Robocopy can perform a deletion of items in a given folder by mirroring it to an empty folder. This is the basic routine that performs the deletion of the folder. Note that this does not delete files located in the target root folder. This is intentional by design.

# Logic
A given root folder, _todeleteFolder_, is enumerated of folders that are available for deletion. The number of folders selected is limited by the _numFoldersToDelete_ variable. Selected folders are marked by prefixing them folder names with ".!" characters. This is required so that subsequent job request do not pick up these folders. Finally, the selected folders are then deleted using Robocopy. The Robocopy copy logs are archived after the build completes.

# Methods
The following methods are used to perform some of the required logic. These are mostly Groovy heavy scripts.

getFolders - Enumerates all folders from a given path. It returns a dictionary of the found folder and its fully qualified path.
markFoldersForDeletion - Tags folders in _todelete folder by prefixing folder with '.$' string and returns a dictionary of marked folders.
getParentPath - A helper method that gets a parent path of a given folder
createEmptyDir - A helper method that creates an empty directory and returns its path.
shellCommand - A helper method that executes a shell command.
deleteFolder - Deletes a folder using Robocopy.
deleteFolders - Deletes a list of given folders.