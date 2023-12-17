### Hi there 👋
LizardRush here
I'm a python programmer
Copy the code below to use my **BETA** unfinished terminal
(wind.terminal import command doesn't work)
```python
import os
import shutil
from git import Repo

def clone_terminal_folder(repo_url):
    target_directory = 'my_terminal_folder'

    try:
        repo = Repo.clone_from(repo_url, target_directory, depth=1, single_branch=True)
        
        terminal_folder_path = os.path.join(target_directory, '.terminal')
        shutil.move(terminal_folder_path, os.path.join(os.getcwd(), '.terminal'))
        
        shutil.rmtree(target_directory)
        
        print(".terminal folder cloned successfully!")
        replit_file_path = os.path.join(os.getcwd(), '.replit')
        if os.path.exists(replit_file_path):
            with open(replit_file_path, 'r') as replit_file:
                lines = replit_file.readlines()
                
                modified_lines = []
                for line in lines:
                    if line.startswith('entrypoint'):
                        modified_lines.append('entrypoint = ".terminal/terminal.py"\n')
                    elif line.startswith('run'):
                        modified_lines.append('run = ["python3", ".terminal/terminal.py"]\n')
                    else:
                        modified_lines.append(line)
                
                with open(replit_file_path, 'w') as replit_file:
                    replit_file.writelines(modified_lines)
        else:
            print("Skipping .replit modification as .py files exist in directories other than .pythonlibs or .terminal.")

        file_path = os.path.abspath(__file__)
        os.remove(file_path)
    except Exception as e:
        print("An error occurred:", e)

repository_url = 'https://github.com/LizardRush/terminal.git'

clone_terminal_folder(repository_url)
```
I play GD (beat about 30 demons, mostly extremes)
idk what to put here
