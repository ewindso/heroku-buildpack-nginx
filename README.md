## Nginx

### Compiling New Binaries

The folder `support/build` contains [Bob](http://github.com/kennethreitz/bob-builder) build scripts for nginx and dependencies.

To get started with it, create a Python app (*Bob* is a Python application) on Heroku inside a clone of this repository, and set your S3 config vars:

```term
$ heroku create --buildpack https://github.com/heroku/heroku-buildpack-python
$ heroku ps:scale web=0
$ heroku config:set WORKSPACE_DIR=/app/support/build
$ heroku config:set AWS_ACCESS_KEY_ID=<your_aws_key>
$ heroku config:set AWS_SECRET_ACCESS_KEY=<your_aws_secret>
$ heroku config:set S3_BUCKET=<your_s3_bucket_name>
$ heroku config:set S3_PREFIX=<optional_s3_subfolder_to_upload_to>
```

Then, shell into an instance and run a build by giving the name of the formula inside `support/build`:

```term
$ heroku run bash
Running `bash` attached to terminal... up, run.6880
~ $ bob build nginx

Building formula nginx:
    -----> Building Nginx 1.6.2...
    Checking for OS
    Compiling Nginx 1.6.2...
    -----> Done.
```

If this works, run `bob deploy` instead of `bob build` to have the result uploaded to S3 for you.
