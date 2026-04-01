## Git

- Fix Cache

    ```git
    git rm -r --cached .
    git add .
    ```

- Garbage Collection

    ```git
    git gc
    ```

- Force Overwrite Branch

    ```git
    git checkout <branch_to_be_overwritten>
    git reset --hard <branch_to_copy_from>
    ```

- Find a string from all commits

    ```git
    git log -G"<string>" --source --all
    ```

- Remove a file from all commits

    Install:
    ```bash
    pip install git-filter-repo
    ```

    Filter:
    ```git
    git reflog expire --expire=now --all
    git gc --prune=now
    git filter-repo --path <filepath> --invert-path [--refs branch] [--force]
    ```

    Force Push:
    ```bash
    git remote add origin git@github.com:<username>/<repository>.git
    git remote set-url origin https://github.com/<username>/<repository>.git
    git push --force --all
    ```

- Mixed Reset last commit

    ```git
    git reset HEAD~1
    ```

- Edit or delete commit after push

    ```git
    git rebase -i HEAD~n
    ```

    `Ctrl + X` to change the command of the commit to `edit` or `drop`

    ```git
    git push -f
    ```

- nul file cannot be removed

    Git Bash to directory:

    ```git
    rm nul
    ```

- Create an orphan branch

    ```git
    git checkout --orphan <branch_name>
    ```
