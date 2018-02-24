# cvrg

A bash script for pushing coverage reports to [cvrg.report](https:/cvrg.report/) during local test execution or test runs in CI/CD environments.

The goal of this script is to not having to install language-specific coverage reporter plugins, but using one standardized helper for all languages and environments.

## Usage

### Adding it to your project

You can add the `cvrg` script to your development projects directly, e.g. 

```bash
$ mkdir -p .cvrg && wget https://raw.github.com/cvrg-report/cvrg/cvrg -o .cvrg/cvrg && chmod +x .cvrg/cvrg
```

Then, you can use the script at `cvrg/cvrg` to pipe the test coverage output to, or use the `cvrg/cvrg <filepath>` input paramter to specify a lcov report file path to be sent to [cvrg.report](https:/cvrg.report/).  


### Dynamic download (CI/CD usage)

You can download the script for each run, for example when using CI/CD systems. You can include the following command before executing the test commands outputting the [lcov]() coverage reports to download the `cvrg.sh` script which uploads the coverage data to [cvrg.report](https:/cvrg.report/):

```bash
curl -s -o ./cvrg https://raw.github.com/cvrg-report/cvrg/cvrg && chmod +x ./cvrg && ./cvrg
```

Direct use of the dynamically downloaded script can be achieved like this: 

```bash
bash <(curl -s -o- -L https://raw.github.com/cvrg-report/cvrg/cvrg)
```
