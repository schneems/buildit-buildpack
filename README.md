# Buildit Buildpack

Runs scripts, generates downloadable tar (and tgz) files.

## What

If you need to compile things or generate files on a Heroku machine, use this buildpack to do so.

## Write Your Build Script

First make the file you want to run

```
$ mkdir buildit-foo
$ cd buildit-foo
$ touch build
```

The buildit buildpack assumes you've got an executable file named `build`, make sure it's executable.

```
$ chmod 777 build
```

Write whatever you want in your build script, the first argument is the output directory (i.e. any files you want to be available after the build needs to go to that dir).

Here's an example of a [buildit file that builds gems](https://github.com/schneems/buildit-gems/blob/master/build).

To have it build bundler you could run

```
$ heroku config:set GEM=bundler
$ heroku config:set VERSION=1.9.6
$ git push heroku master
```



## Run your Build script

Create a Heroku app, set the buildpack url and deploy.

```
$ heroku create
$ heroku config:set BUILDPACK_URL=https://github.com/schneems/buildit-buildpack.git
$ git push heroku master
```

Protip: If you need to re-deploy without changing your script you can force a commit by running `$ git commit --allow-empty -mempty`.


## Download your files

Visit your Heroku app to view your files

```
$ heroku open
```

You'll see a directory containing your script, the output build directory and a builds.tar

![](https://www.dropbox.com/s/0aab5kvz4soxpq1/Screenshot%202015-05-06%2013.22.19.png?dl=1)

Warning: This is all publically available, don't put anything in your build output or your script that you wouldn't want visable to the world.

