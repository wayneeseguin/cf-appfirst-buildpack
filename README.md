# AppFirst Cloud Foundry Buildpack

This buildpack is intended to allow for use of the AppFirst collector for 
monitoring applications on Cloud Foundry.

From within your application's project root, create a .buildpacks file which has
a first line containing the AppFirst CF buildpack followed by the buildpack 
for our application. We then push our to CF using multiple buildpacks.

# Example: cf-env

In our example we will deploy the Ruby version of the cf-env application.

```sh
$ git clone https://github.com/cloudfoundry-community/cf-env.git
$ cd cf-env
```

We now create a `.buildpacks` file whose first line is the URL for the AppFirst 
CF buildpack and the second line is the Ruby buildpack, so it should look like:

```sh
$ cat .buildpacks
https://github.com/wayneeseguin/cf-appfirst-buildpack
https://github.com/cloudfoundry/ruby-buildpack
```

Next we set our AppFirst tenant id in an `.appfirst` file in the project root
path, the contents should look like the following. Note you must replace '0000' 
with your tenantId which you can find under the 'admin > account' section of 
AppFirst's website when you are logged in:

```sh
$ cat .appfirst
tenantId=0000
```

Now, still within the project root path, we push our application to our Cloud 
Foundry enabling multiple buildpacks:

```sh
$ cf push appfirst -b https://github.com/ddollar/heroku-buildpack-multi
```

Within a minute, if the above configuration steps were followed the application's
metrics should begin showing within AppFirst's UI.

## Custom Buildpack Documentation

Cloud Foundry [Custom Buildpack documentation](http://docs.cloudfoundry.org/buildpacks/custom.html) contains more details about how this buildpack is put together.
