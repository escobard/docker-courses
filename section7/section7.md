# Docker deployment with travic CI / AWS

## Travis CI

- Must ensure that the `parent folder of the repository` contains the .travis.yml file.
- Otherwise this causes a `ruby error` which causes the CI to crash.

## AWS

### Elastic beanstalk
- the top choice for running individual docker containers on a server