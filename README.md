# cvrg

A bash script for pushing coverage reports to [cvrg.report](https:/cvrg.report/) during local test execution or test runs in CI/CD environments.

The goal of this script is to not having to install language-specific coverage reporter plugins, but using one standardized helper for all languages and environments.

## Usage

### Bash script location

The download link [https://cvrg.report/bash](https://cvrg.report/bash) redirects to the the `master` branch of the [cvrg](https://raw.githubusercontent.com/cvrg-report/cvrg/master/cvrg) script on GitHub. 

### Dynamic download (CI/CD usage)

You can download the script for each run, for example when using CI/CD systems. You can include the following command before executing the test commands outputting the [lcov]() coverage reports to download the `cvrg.sh` script which uploads the coverage data to [cvrg.report](https:/cvrg.report/):

```bash
curl -s -o ./cvrg https://cvrg.report/bash && chmod +x ./cvrg && ./cvrg
```

Direct use of the dynamically downloaded script can be achieved like this: 

```bash
bash <(curl -s -o- -L https://cvrg.report/bash)
```

### Adding the uploader to your project

You can add the `cvrg` script to your development projects directly, e.g. 

```bash
$ mkdir -p .cvrg && wget https://cvrg.report/bash -o .cvrg/cvrg && chmod +x .cvrg/cvrg
```

Then, you can use the script at `cvrg/cvrg` to pipe the test coverage output to, or use the automatic discovery of coverage reporting files below the project path.  

### Runtime configuration

The `cvrg` script can be configured by specifying command line arguments:

#### General options

The general seeting can by influenced by the following:

```text
  -h          Show this help screen and exit
  -f          Fail with a exit code of 1 instead of 0
  -y path     Configuration YAML file path
  -u url      API endpoint base URL (default: https://api.cvrg.report)
  -t token    Project token (if not passed via YAML configuration file)
  -D feature  Disable features
  
              gcov        Disable gcov
              coveragepy  Disable coverage.py
```

#### curl options

For custom settings, like using proxies etc., the arguments for `curl` can be set accordingly:

```text
  -c path     Path to your custom cacert.pem file
  -a "args"   Additional curl arguments
```

#### gcov options

The creation of `gcov` reports can be customized by the following flags:

```text
  -i glob     Path to ignore while gathering reports
  -I glob     Path to include while gathering reports
  -e exe      Executable for gcov to use. Default is 'gcov'
  -g "args"   Additional gcov arguments
```

#### Project-related overrides

There are also flags which can be used to override the automatic discovery of project-related information:

```text
  -R path     Project root path
  -B name     Branch name
  -C sha      Commit hash
  -M "msg"    Commit message
  -T tag      Tag name
  
  -n "name"   Custom name (will be filled automatically for known CIs)
  -j id       Job identifier
  -b id       Build identifier
  -l "labels" Labels for this run (comma-separated)
  -p "info"   Pull request information
  -s slug     Owner/Repo information
```

#### Debugging

The following arguments can be used for debugging purposes:

```text
  -v        Verbose mode
  -d        Dump the gathered coverage report info (no upload)
```

## CI support

The `cvrg` scripts supports the following CI providers out of the box:

* [Travis CI](http://www.travis-ci.org)
* [Circle CI](http://www.circleci.com)
* [Codeship](http://www.codeship.com)
* [GitLab CI](https://about.gitlab.com/gitlab-ci/)
* [Shippable](http://www.shippable.com)
* [Drone CI](https://drone.io/)
* [Jenkins](https://jenkins.io/)
* [Teamcity](https://www.jetbrains.com/teamcity/)
* [Buddybuild](https://www.buddybuild.com/)
* [Bamboo CI](https://www.atlassian.com/software/bamboo)
* [Bitrise](https://www.bitrise.io/)
* [Buildkite](https://buildkite.com/)
* [Heroku CI](https://www.heroku.com/continuous-integration)
* [Codefresh](https://codefresh.io/)
* [Wercker](http://www.wercker.com/)
* [Magnum CI](https://magnum-ci.com/)
* [Greenhouse CI](https://nevercode.io/)
* [AppVeyor](https://www.appveyor.com/)
* [Semaphore CI](https://semaphoreci.com/)
