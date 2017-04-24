## Heroku buildpack: Zotonic 1.x

This is a Heroku buildpack for a Zotonic 1.x site.
Use it for easy deployment of a single Zotonic site.
The buildpack will automatically provision a dev database and configure your Zotonic site to use it.

NOTICE: The git repo to push should only contain a Zotonic site, not the whole Zotonic source.

### Configure your site
    $ cd YOUR_SITE_DIR 
then
    
    $ heroku config:add BUILDPACK_URL="https://github.com/wiregh/heroku-buildpack-zotonic-v1.x" -a YOUR_APP

or
    
    $ heroku create --buildpack "https://github.com/wiregh/heroku-buildpack-zotonic-v1.x"

### Configure your Zotonic site

Set the following environment variables :

* ADMIN_PASSWORD (That's the admin password, obviously)
* OTP_VERSION (Erlang version to be used, defaults to ```OTP-19.1.1```)
* ZOTONIC_VERSION (Defaults to ```master```)

### Select an Erlang version

The Erlang/OTP release version that will be used to build and run your application is now sourced from the environment variable ```OTP_VERSION```. It needs to be the branch or tag name from the http://github.com/erlang/otp repository, and further, needs to be one of the versions that precompiled binaries are available for.

Currently supported OTP versions:

* OTP-18.0
* OTP-18.0.3
* OTP-18.1
* OTP_18.2
* OTP-18.1.3
* OTP-18.1.5
* OTP-18.2
* OTP-18.2.2
* OTP-18.2.3
* OTP-18.2.4.1
* OTP-18.2.4
* OTP-18.3
* OTP-18.3.1
* OTP-18.3.2
* OTP-18.3.3
* OTP-18.3.4
* OTP-19.0
* OTP-19.0.2
* OTP-19.0.3
* OTP-19.1
* OTP-19.1.1

To select the version for your app set environment variable ```OTP_VERSION``` to define Erlang version.

    $ heroku config:set OTP_VERSION=OTP-19.1.1

### Zotonic version
This buildpack is targeted at Zotonic 1.x which is still in development by the zotonic team with no release yet so the ```master``` branch of Zotonic source is used by default.

### Extra Dependencies
To make Zotonic fetch and compile extra dependencies needed by your site or modules, create a file called ```compile_deps```  
at the root of your site's directory which lists the needed dependencies.

Example
```
$ cd YOUR_SITE_DIR  
```

    $ cat compile_deps

```
%%% List with extra dependencies which get fetched and compiled by rebar
   [
       {jsx, "1.4", {git, "git://github.com/talentdeficit/jsx", {tag, "v1.4"}}},
       {jwt, ".*", {git, "git://github.com/marianoguerra/jwt-erl", {branch, "master"}}}   
       
       ].
       
 ```

### Deploy your site

    $ git push heroku master

You may need to write a new commit and push if your code was already up to date.

### TODO

~~Fetches deps and rebuilds all Zotonic on each deploys, should use the build cache to only recompile the necessary bits.~~

~~IMPORTANT: All file uploads go to the transient file system, meaning that everything is destroyed on each deploys. These assets should go to S3 or similar.~~

Pull requests are very welcome.

### THANKS

Geoff Cant for writing the base heroku-buildpack-erlang, the starting point of this buildpack. 

Eric Cestari for writing heroku-buildpack-zotonic for earlier versions of Zotonic found at 
https://github.com/vmaatta/heroku-buildpack-zotonic

The Zotonic and Heroku guys.

### ABOUT ZOTONIC

Zotonic is a blazingly fast CMS. Read more about it here: http://www.zotonic.com

### AUTHOR

Enoch Jr. Nii Nortey Wilson

enoch@planet-winnerghana.com


