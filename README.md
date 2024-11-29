# project_01
### Documentation for File Organization Project

---

#### **Project Overview**

This Python script organizes files in a given directory into various folders based on file types (for example, images, documents, videos, etc.). The project has two primary tasks:

1.  **Create folders** for various file types.
2.  **Organize files** by moving them to the appropriate folders according to their file extensions.

This can be useful for users who have cluttered directories with a variety of file types and want to organize them automatically for better file management.

---

#### **Features**

1. **Dynamic Folder Creation**: 
   The script can automatically create new folders for various file categories (e.g., images, videos, documents, etc.).
   
2. **File Organization**:
Files are sorted into pre-defined types by their extensions and moved accordingly to the respective folders.

3. **Handling Various File Types**:
   The script deals with multiple file types for instance:
   - Images: `.jpg`, `.jpeg`, `.png`, `.gif`
   - Documents: `.pdf`, `.docx`, `.txt`
   - Videos: `.mp4`, `.mkv`, `.flv`
   - Audio: `.mp3, `.wav`
   Archives: `.zip`, `.tar`, `.rar`
- **Spreadsheets**: `.xls`, `.xlsx`, `.csv`

---

#### **Requirements**

- **Python Version**: The script needs Python 3.x (tested with version 3.10.11).
- **Libraries**:
  - `os`: Used for operations in the file system, like listing files, checking directories, and creating folders.
  - `shutil`: Used to move files from one directory to another.

---

#### **Code Explanation**

##### **1. Imports**
```python
import os
import shutil
```
- `os`: Functions used to interact with the operating system, like checking whether directories exist and joining paths.
- `shutil`: Offers a way to move files for general, high-level file functions.

### **2. Defining File Types
```python
directory = './'

file_types = {
    'images': ['.jpg', '.jpeg', '.png', '.gif'],
    'documents': ['.pdf', '.docx', '.txt'],
    'videos': ['.mp4', '.mkv', '.flv'],
    'audios': ['.mp3', '.wav'],
    'archives': ['.zip', '.tar', '.rar'],
    'spreadsheets': ['.xls', '.xlsx', '.csv']
}
```
- **`directory`**: The directory where files are to be found (current directory `./`).
- **`file_types`**: A dictionary mapping folder names to a list of file extensions to be categorized under each folder type.

##### **3. `create_folders` Function**
```python
def create_folders(base_dir, folders):
    for folder in folders:
        folder_path = os.path.join(base_dir, folder)
        if not os.path.exists(folder_path):
```
os.makedirs(folder_path)
```
- **Input**: 
  - `base_dir`: The base directory where folders are to be created.
  - `folders`: A list of folder names (keys of `file_types`).
- **Process**: For each folder name, it checks if the folder already exists; if not, it creates the folder inside the specified directory (`base_dir`).
- **Output**: Creates the necessary folders for organizing files.

**4. `organise_files_by_types` Function**
```python
def organise_files_by_types(base_dir, file_types):
    for filename in os.listdir(base_dir):
        file_path = os.path.join(base_dir, filename)

        if os.path.isdir(file_path):
            continue
        # check the particular file type and move it to an appropriate folder
```
file_ext  = os.path.splitext(filename)[1].lower()

        for folder, extensions in file_types.items():
            if file_ext in extensions:
                target_folder = os.path.join(base_dir, folder)
shutil.move(file_path, target_folder)
            print(f"Moved {filename} to {folder}")
            break
```
- **Input**: 
  - `base_dir`: The directory containing the files to organize.
- `file_types`: A dictionary mapping folder names to file extensions.
- **Process**: 
  - The function iterates over all files in the directory. 
  - If the file is not a directory, it checks its extension.
  - According to the extension, the file moves to the corresponding folder
- **Output**:
- Move files to the correct folder and print a message for each file moved.
  - For instance, a `.mp4` file will be moved to the 'videos' folder.

##### **5. Calling the Functions**
```python
create_folders(directory, file_types.keys())
organise_files_by_types(directory, file_types)
```
- **Execution Flow**: 
  - First, `create_folders` is called to create the required folders.
  - Then, `organise_files_by_types` is called to move the files into the respective folders.

##### **6. Output Example**
```bash
Moved Welcome to CollegeDesire _ Shape The Future - Google Chrome 2023-04-04 22-45-49.mp4 to videos
```
- This indicates that the script successfully moved a `.mp4` video file to the `videos` folder.

---

#### **Error Handling**

- The code doesn't explicitly handle errors (e.g., file system errors or permission issues), but in production environments, it's a good practice to add error handling to ensure robustness.
- For instance, `shutil.move` will raise an error in case the file cannot be moved due to permission or because the destination folder is not writable.

---

#### **Future Improvements**


1.  **Recursive File Handling**: Add support for file handling in subdirectories.
2.  **Log File Creation**: Implement logging for tracking activities related to the movement of files so users can review operations made by the script.
3. **Enhanced User Interface Interaction**: Allow users to enter a directory path and specify their desired file types and folder mapping.
4. **Exceptions Handling**: Implement particular exceptions for potential problems, for example, read-only files or missing permissions.

Conclusion

This is a simple and efficient Python project that automatically organizes files into categorized folders according to their types. This reduces the amount of effort required to keep a directory structured, making it a good option for users with many files to manage. Possible future updates include handling subdirectories, more advanced logging, and improved error handling for robustness.
