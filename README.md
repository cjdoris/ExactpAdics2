# ExactpAdicsCommon

Common code for the [ExactpAdics](https://github.com/cjdoris/ExactpAdics) and [ExactpAdics2](https://github.com/cjdoris/ExactpAdics2) packages. These need to manually merge from this repository when changes are made. Merge for the first time as follows:

```
$ git remote add common /path/to/ExactpAdicsCommon
$ git fetch common
$ git merge --allow-unrelated-histories common/master
```

and subsequent times as follows:

```
$ git fetch common
$ git merge common/master
```
