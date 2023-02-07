## Synopsys GitHub Action - Polaris　
## v.1.0.0   https://github.com/synopsys-sig/synopsys-action#synopsys-github-action---polaris

Before you can run a pipeline using the Synopsys Action and Polaris, you must make sure the appropriate
applications, projects and entitlements are set in your Polaris environment.

At this time, Polaris does not support the analysis of pull requests. We recommend running the Synopsys Action on
pushes to main branches.

We recommend configuring sensitive data like access tokens and even URLs, using GitHub secrets.

```yaml
name: Synopsys Security Testing

on:
  push:
    # At this time, it is recommended to run Polaris only on pushes to main branches
    # Pull request analysis will be supported by Polaris in the future
    branches: [ master, main ]

  pull_request:
    branches: [ master, main ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v2
      - name: Synopsys Action
        uses: synopsys-sig/synopsys-action@<version>
        with:
          polaris_serverUrl: ${{ secrets.POLARIS_SERVER_URL }}
          polaris_accessToken: ${{ secrets.POLARIS_ACCESS_TOKEN }}
          polaris_application_name: "testapp1"
          polaris_project_name: "testproj1"
          polaris_assessment_types: "[\"SCA\", \"SAST\"]"

          # Optional parameter to specify path to synopsys bridge.
          # This can be used if you want to pre-configure your GitHub Runner with the
          # Synopsys Bridge software
          # The default is either /{user_home}/synopsys-bridge or in linux /usr/synopsys-bridge
          #synopsys_bridge_path: "/path_to_bridge_executable"

          # Optional parameter, but usually specified - the location of the Synopsys Bridge software
          # The Synopsys Bridge software distribution is platform specific - this must match the host OS
          # of your runner. For example in this case, we are using the latest version for Linux.
          bridge_download_url: ${{ env.LINUX_BRIDGE_URL }}
        env:
          LINUX_BRIDGE_URL: "https://sig-repo.synopsys.com/artifactory/bds-integrations-release/com/synopsys/integration/synopsys-action/0.1.72/ci-package-0.1.72-linux64.zip"
```


# Apache Roller

[Apache Roller](http://roller.apache.org) is a Java-based, full-featured, multi-user and group-blog server suitable for blog sites large and small.
Roller is typically run with Apache Tomcat and MySQL.
Roller is made up of the following Maven projects:

* _roller-project_:         Top level project
* _app_:                    Roller Weblogger webapp, JSP pages, Velocity templates
* _assembly-release_:       Used to create official distributions of Roller
* _docs_:                   Roller documentation in ODT format
* _it-selenium_:            Integrated browser tests for Roller using Selenium

## Documentation

The Roller Install, User and Template Guides are available in ODT format (for OpenOffice or LibraOffice):

* <https://github.com/apache/roller/tree/master/docs>

## For more information

Hit the Roller Confluence wiki:

* How to build and run Roller: <https://cwiki.apache.org/confluence/x/EM4>
* How to contribute to Roller: <https://cwiki.apache.org/confluence/x/2hsB>
* How to make a release of Roller: <https://cwiki.apache.org/confluence/x/gycB>
* Other developer resources: <https://cwiki.apache.org/confluence/x/D84>


## Installing Roller 

If you want to run Roller in production, then you should down load the latest official release and install it by following the Installation Guide, which you can find at the documentation link: <https://github.com/apache/roller/tree/master/docs>.


## Quick start: Running via Maven

You probably should not run Roller in production using this technique, but it's a relatively easy way to try Roller for yourself. 
Assuming you've got a UNIX shell, Java, Maven and Git:

Get the code:

    $ git clone https://github.com/apache/roller.git

Compile and build Roller:

    $ cd roller
    $ mvn -DskipTests=true install

Run Roller in Jetty with an embedded Derby database (for testing only):

    $ mvn jetty:run

Once Jetty is up and running browse to <http://localhost:8080/roller> to try to Roller.


## Quick start: running via Docker

Another way to try Roller is to use Docker. 
This is actually easier than running via Maven because you do not need Maven or Java. 
If you've got Docker, here's how you can run Roller for demo purposes.

Get the code:

    $ git clone https://github.com/apache/roller.git

Run Docker Compose to build and launch Roller along with a PostgreSQL database:

    $ cd roller
    $ docker-compose up
    
It will take a while to build and start the Docker image. 
Once it's done browse to <http://localhost:8080/roller> to try Roller.
