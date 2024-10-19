1. `git rebase <base> <about to come>`
2. `git branch -d <branch name>`
3. `git reflog`
4. `git branch -f <branch name> <where to move>`
5. `git checkout -b <branch name> <location>`
6. `git rebase --abort`
7. Relative refs
	1. **`^^^^`**: Moves `HEAD` back by 4 commits.
	2. **`~<number>`**: Moves `HEAD` back by `<number>` commits. 
8. `git checkout <branch>`
	1. `git checkout <commit hash>` detaching head
	2. `git checkout <branch>^2` moves `HEAD` to second parent
9. `git cherry-pick <commit-hash> <commit-hash> ..`
	1. Cherry-pick only works with commit hashes
	2. Puts those commit hashes under the HEAD
10. `git rebase -i <where to>`
	1. `reword`
	2. `pick`
	3. `drop`
	4. `squash`
11. `git stash`
	1. First `git add .` to track the files, then `stash` them
	2. Stashes are stored in a stack data structure
	3. `git stash pop` to get the files back
	4. `git stash list` to show all stashes
	5. `git stash -m "some message"` to stash away with a message
	6. `git stash pop --index <X>` here X is the index number, you can check the number from `git stash list`
	7. `git stash branch <branch name> <X>` Stashed content can be retrieved back on to a branch and X is the index
	8. `git stash drop <X>` to drop the specific stash of index number X
	9. `git stash clear` to clear the entire stash stack
	10. `git stash apply <stash@{X}>` to apply any stash onto any branch, X is the stash index
12. After resolving a **merge conflict** do a `git add .` then continue ahead with
	1. If rebasing then use `git rebase --continue`
	2. If merging then use `git commit`
13. `git restore <file path>` used to restore a file to its previous commit, lets say I am working on a file that is not committed, I can reset the state of the repo to the previous commit using restore command, (**This action cannot be undone**) 

# Squashing vs Dropping
Squashing and dropping commits in Git are different operations with distinct purposes:
### Squashing

- **Purpose**: To combine multiple commits into a single commit.
- **Use Case**: When you want to consolidate a series of related changes into one commit for a cleaner commit history.
- **Result**: The changes from the squashed commits are preserved, but they are combined into a single commit with a new commit message.

### Dropping

- **Purpose**: To remove a commit from the commit history entirely.
- **Use Case**: When you want to discard changes introduced by a specific commit.
- **Result**: The changes from the dropped commit are removed from the commit history.

### Example

Let's say you have the following commit history:

```
a <-- b <-- c <-- d <-- e <-- f
```

#### Squashing Commits `c`, `d`, and `e` into a Single Commit

1. **Start Interactive Rebase**:
   ```sh
   git rebase -i HEAD~4
   ```

2. **Edit the Rebase Todo List**:
   Change `pick` to `squash` for commits `d` and `e`:
   ```
   pick <commit-hash-c> Commit message for c
   squash <commit-hash-d> Commit message for d
   squash <commit-hash-e> Commit message for e
   pick <commit-hash-f> Commit message for f
   ```

3. **Save and Close the Editor**:
   Save the changes and close the editor. Edit the combined commit message as needed.

4. **Complete the Rebase**:
   ```sh
   git rebase --continue
   ```

5. **Force Push (if necessary)**:
   ```sh
   git push --force
   ```

Resulting commit history:
```
a <-- b <-- e' <-- f
```
Where `e'` is the new commit that combines the changes from `c`, `d`, and `e`.

#### Dropping Commit `d`

1. **Start Interactive Rebase**:
   ```sh
   git rebase -i HEAD~4
   ```

2. **Edit the Rebase Todo List**:
   Change `pick` to `drop` for commit `d`:
   ```
   pick <commit-hash-c> Commit message for c
   drop <commit-hash-d> Commit message for d
   pick <commit-hash-e> Commit message for e
   pick <commit-hash-f> Commit message for f
   ```

3. **Save and Close the Editor**:
   Save the changes and close the editor.

4. **Complete the Rebase**:
   ```sh
   git rebase --continue
   ```

5. **Force Push (if necessary)**:
   ```sh
   git push --force
   ```

Resulting commit history:
```
a <-- b <-- c <-- e <-- f
```
Where commit `d` has been removed from the history.

### Summary

- **Squashing**: Combines multiple commits into one, preserving the changes but consolidating the commit history.
- **Dropping**: Removes a commit and its changes from the commit history entirely.

Both operations can be performed using interactive rebase, but they serve different purposes and result in different outcomes.

# Rebasing and merging are same
- Either rebasing or merging, we have to resolve the merge conflict and commit, thus both will result in the same final result, but in case of rebasing the previous version will be not saved
