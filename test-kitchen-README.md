# Module

TBD

## Testing

This framework use test kitchen. All you have to run here for this project is

    kitchen command_1  # command says hello world
    ..
    kitchen command_x #command says changeme

if you want to know more about test kitchen then visit https://goo.gl/TeGCEZ

### Override the tests

If you don't want to run all the tests, don't hack the main _.kitchen.yml_!
Instead create a simpler *.kitchen.local.yml* to override it.
To see and example of an override it just rename the file _.kitchen.local.yml.example_ to _.kitchen.local.yml_.

### Advices

To run all the test I would advice a machine with a lot of bandwidth and memory.

### Prerequisites

To make the testing work you need to have installed locally:

- docker
- a ruby env (possibly 2.4.0-dev)

Install all the test-kitchen dependencies run:

    $ bundle install

To check which ruby version you are using (only works with rbenv):

    $ rbenv global
    2.4.0-dev

### Check status

You can see the status of test-kitchen with:

    $ kitchen list
    Instance        Driver  Provisioner  Verifier  Transport  Last Action
    default-ubuntu  Docker  PuppetApply  Shell     Ssh        Verified

### Login into the docker container

It's a little starnge to login via test-kitchen in a docker container.
The usual _kitchen login_ command doesn't work. There is a script to do just
that already in the repo:

    ./utilities/kl.sh ubuntu

Should login automatically. Instead of _ubuntu_ just put the name of the machine
you want to login.
Use it from the root dir of this module.

### Validate puppet

Run:

    puppet-lint --no-autoloader_layout-check --FIX manifests/* && \
    puppet-lint --no-autoloader_layout-check --FIX test/\*.pp && \
    rake validate

### To test with with test-kitchen

Run:

    kitchen converge -c 999 && kitchen verify -c 999
