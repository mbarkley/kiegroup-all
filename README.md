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

    git submodule foreach 'git remote add $USERNAME git@github.com:$USERNAME/$name.git && echo Added origin for $name || echo Ignoring $name'

Switching branches
---

For some branch, `$BRANCH`:

    git submodule foreach 'git checkout $BRANCH || echo Ignoring $name'

Rebase all repos
---

For some remote repository, `$REMOTE`, and branch, `$BRANCH`:

    git submodule foreach 'git fetch $REMOTE && git rebase $REMOTE/$BRANCH'


Choosing what to build
---

1. Building everything:

    ```
    mvn clean install -Pall
    ```

1. Build everything except Errai:

    ```
    mvn clean install -Pnot-errai
    ```

1. Build everything in the kiegroup org:

    ```
    mvn clean install -Pkiegroup
    ```

1. Build kie-wb-common:

    ```
    mvn clean install -Pkie-wb-common
    ```

1. Build kie-wb-common and uberfire:

    ```
    mvn clean install -Pkie-wb-common,uberfire
    ```

1. Build kie-drools-wb-webapp and all dependencies:

    ```
    mvn clean install -Pall -pl :kie-drools-wb-webapp -am
    ```

1. Build uberfire-commons, and all modules that depend on it:

    ```
    mvn clean install -Pall -pl :uberfire-commons -amd
    ```
