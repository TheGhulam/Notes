## OS path commands

	• os.path.join('folder1', 'folder2', 'file.png')

	# Returns PATH based on the OS:

	• os.getcwd()
		○ Returns the current working directory

	• os.chdir('c:\\')
		○ Changes the current working directory

	• os.path.abspath('spam.png')
		○ Returns the ABS file path
		
	• os.path.isabs('c:\\folder\\folder')
		○ Return whether the file path is the ABS path
	
	• os.path.relpath(target path, current path)
		○ Returns the relative path to the target path
	
	• os.path.dirname()
		○ Returns the parent directories of the given path
		
	• os.path.basename()
		○ Returns the last file/folder in the given path

	• os.path.exists()
		○ Returns whether the path exists in the drive

	• os.path.isfile()
		○ Returns whether the file path is a file

	• os.path.isdir()
		○ Returns whether the file path is a folder

	• os.path.getsize()
		○ Returns of the size of the last file/folder in path
	
	• os.listdir()
		○ Returns a list of files/folders strings in the given path

	• os.makedirs('c:\\folder')
create files/folders for the given path



![](os-hierarchy.png)

```python
for foldername, subfolders, filenames  in os.walk('c:\\folder'):
	print('The folder is ' + foldername)
	print('The subfolders in ' + foldername + ' are: ' + str(subfolders))
	print('The filenames in ' + foldername + ' are: ' + str(filenames))
print()
```

