# SAWTOOTH-UTILS
Set of utility scripts to help with development of hyperledger sawtooth.  These
scripts are targeted at allowing users to run the Sawtooth-core development
directly on a Ubuntu 16.04 machine using docker as an execution environment
for sawtooth.

## INSTALL
clone this repo in a sawtooth working directory as a peer to sawtooth-core
Required dependences: docker-ce, docker-compose, python3, python3-pip, virtualenv

## SETTING UP FOR USE

From the sawtooth directory
run `source sawtooth-utils\bin\st-env'

This will need to be done in every shell you intend to do development from.

## GENERAL USAGE

- `build_all_prebuild` can be used inplace of `build_all`. This script will
download the lasts version of prebuild docker images from dockerhub and
name them appropriately to be used by the all of the `run_tests`,
`run_docker_tests`, etc. This if the docker images from docker_hub are out of
date or not compatible with your current branch, `build_all` can be run to
generate the needed docker images locally.

- `st-run`, `st-run-cxx|java|js` will run the command given as inside a docker
image with the requiured. These commands runs as the host user inside the
docker image. So file permisions do not get modified. Also these commands map
a directory from the sawtooth working directory to the user home directory in
the docker container. This allows npm and maven caching to work correctly and
speeds up the build performance of Java and Javascript sdks significantly. The
user done here will not work on OSX or Windows.

- `st-sudo` is similar to `st-run` but runs the command as root in the docker
container. This is often necessary to cleanup after a `run_tests` as
`run_docker_test` still executes all the tests as root and leaves artifacts
littered around the dev directory owned by root. `st-sudo git clean -fxd` will
clean these up.

- `run_tests` can be called directly for the host shell and

- `st-ut` will run the validator unit tests in a docker container.
- `st-lint` will run the validator unit tests in a docker container using
'upstream/master' as the basis.
- `st-bandit` will run bandit in a docker container.
- `st-build-doc` will run a doc build in a docker container.

- `st-pr <pr number>` will fetch and checkout a given pr.
- `st-validate <branch_name>` will run fetch upstream and origin, checkout
the given branch name and run lint, tests, docs, and bandit on that branch and
provide a summary of the results.

- `st-vagrant` will run the vagrant commands regardless what directory you are
in. Also `st-vagrant window` will open a new gnome-terminal with a vagrant
ssh session in it.



