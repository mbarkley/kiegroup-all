After cloning...
---

`git submodule init;`

`git submodule update --remote;`

`git submodule foreach git checkout master;` #just to be sure

`git submodule foreach git pull origin master;` #just to be sure

`mvn clean install --fail-at-end;`

Useful Settings
---

* Setting `MAVEN_OPTS="-Xmx8192m"` may be necessary.

* Creating an alias for `git submodule foreach` can come in handy. (e.g. `alias gsf='git submodule foreach'`)

* Prevent from accidentaly pushing to origin `git submodule foreach git remote set-url --push origin no_push`.

Add your forks
---

To add all forks run the following command (replacing `$USERNAME` with your github handle):

    `git submodule foreach 'git remote add origin git@github.com:$USERNAME/$name.git && echo Added origin for $name || echo Ignoring $name'`

Switching branches
---

For some branch, `$BRANCH`:

    git submodule foreach 'git checkout $BRANCH || echo Ignoring $name'

Updating all repos to a branch
---

To update all repos to `$BRANCH`:

    git submodule foreach 


Choosing what to build
---

`mvn clean install -pl "uberfire"` will build only uberfire

`mvn clean install -pl "\!uberfire"` will build **everything except uberfire**

`mvn clean install -pl :kie-wb-webapp -am` will build the KIE workbench **and all it's dependencies**

`mvn clean install -pl :uberfire-api -amd` will build the uberfire-api **and everything depending on it**
