# Globalize your .gitignore

When I was new to git, I would always jam the same old stuff in each project's `.gitignore`, like:

#### `.gitignore`
```
.DS_Store
# other os x-y stuff
node_modules
bower_components
```

`node_modules` and `bower_components` make sense to be included in a project's `.gitignore`. Whatever developer may check out and contribute to your project will end up with those directories created, and you [may or may not](http://addyosmani.com/blog/checking-in-front-end-dependencies/) want them hidden from your repository.

Other stuff, however, may be unique to your development environment. Things such as hidden OS files, IDE project files, etc. Is every contributor to your project meant to update `.gitignore` to consider their environment? This problem is neverending.

Then, I remembered something very important. git's smarter than I am. They've totally figured this out.

Introducing...

#### `~/.gitignore_global`
```
# Compiled source #
###################
*.com
*.class
*.dll
*.exe
*.o
*.so

# Packages #
############
# it's better to unpack these files and commit the raw source
# git has its own built in compression methods
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip

# Logs and databases #
######################
*.log
*.sql
*.sqlite

# OS generated files #
######################
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
```

Create that file, then run:

```bash
$ git config --global core.excludesfile ~/.gitignore_global
```

Every git project, system-wide, will now respect this list of ignored file patterns, saving you the trouble!

The technique above is detailed in [GitHub's Help Pages](https://help.github.com/articles/ignoring-files).
