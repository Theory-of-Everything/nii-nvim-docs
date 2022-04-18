This is a guide that will help you migrate from nii-nvim v0.1.1-alpha to v0.2.0-beta

## Merging custom configs with branch changes
If you have custom configurations for you nii-nvim install, there are a few steps you will need to take before you pull the latest changes from the master branch.
- To fetch all changes on the remote without overwriting your local changes:
```bash
git fetch origin master:master
```

1. If you have uncommited local changes in your config (assuming you cloned it), this command will save changes so that they are not overwritten
```bash
git stash
```

2. If you have **committed** changes in the current branch, you can diff and merge/rebase changes as so
```bash
git rebase master # If you want to rebase changes

git merge master  # if you want to merge directly to master
```

3. **ONLY AFTER** you have completely done all of the neccissary steps above, you can pull from origin
```bash
git pull origin
```

 If you stashed local uncommited changes (per point 1) you can pop changes into your working directory now. At this point you can diff/merge/rebase all of your changes.
 ```bash
 git stash pop
 ```

 If you have any other questions or need help, feel free to reach out on the [discord server](https://discord.gg/H6WY7cUkfw) or [matrix room](https://matrix.to/#/#nii-nvim:halogen.city)
