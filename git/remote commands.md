- **`git checkout -b <new branch> <origin/branch>`**  
	
	1. Create a new local branch `<new branch>`.
	2. Set up tracking to follow the remote branch `<origin/branch>`.
	3. Switch to the newly created branch.
	
	So, the new branch is linked to the remote branch, and any future `git pull` or `git push` will default to tracking that remote branch unless changed.

- **`git branch -u <o/branch> <existing branch>`**  
  Sets up tracking between your local branch and a remote branch (e.g., `origin/branch`), so changes are tracked between the two.

- **`git fetch`**  
  Downloads objects and refs from a remote repository without merging them into your current branch. Useful for getting updates.

    - **`git fetch origin <place>`**  
      Fetches updates for the specific remote branch `<place>` from `origin`.

    - **`git fetch origin <source>:<destination>`**  
      Fetches `<source>` from `origin` and stores it as `<destination>` locally, allowing you to name it differently.

    - **`git fetch origin :<destination>`**  
      Creates a new branch `<destination>`  locally

- **`git pull`**  
  Fetches updates from the remote branch and merges them into your current branch.

    - **`git pull --rebase`**  
      Fetches the remote changes and rebases your local commits on top of them, keeping a cleaner history without merge commits.

    - **`git pull origin <place>`**  
      Fetches and merges updates from the `<place>` branch in the remote repository `origin`.

    - **`git pull origin <source>:<destination>`**  
      Fetches updates from `<source>` and merges them into your local `<destination>` branch.

- **`git push`**  
  Pushes your local changes to the remote repository.

    - **`git push origin <place>`**  
      Pushes your local `<place>` branch to the corresponding branch on `origin`.

    - **`git push origin <source>:<destination>`**  
      Pushes your local `<source>` branch to the `<destination>` branch on `origin`.

    - **`git push origin :<destination>`**  
      Deletes the `<destination>` branch on `origin` by specifying no local source.