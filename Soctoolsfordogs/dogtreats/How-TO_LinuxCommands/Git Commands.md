#### Some Basic git ![[1.2_Bibliography#Git]]
#### initialise a git repo locally.
```
git init
```

Clone a remote repo locally.
```
git clone "repo"
```

Add all changes to repo
```
git add . 
```

Take a branch
```
git branch crazy-experiment
```

List all branches
```
git branch
```

Delete a branch
```
git branch -d -D(be careful) crazy-experiment
```

Check remote server.
```
git remote -v
```

Change remote https to ssh,, works both ways
```
git remote set-url origin git@github.com:OWNER/REPOSITORY.git
```

### Standard procedure to push
```
git status //check branch status
git add . //add all changes
git commit -m "message" //commit changes locally
git push origin main/branch //push changes remote.
```


#howto_linux_commands

