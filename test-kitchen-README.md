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
that already in the repo. If you have this machine:

    $ kitchen list
    Instance                            Driver  Provisioner  Verifier  Transport  Last Action
    solrcloud5-standalone-ubuntu-1404   Docker  PuppetApply  Shell     Ssh        Verified

Do the following:

    $ ./utilities/kl.sh solrcloud5-standalone-ubuntu-1404
    spawn kitchen login solrcloud5-standalone-ubuntu-1404
    Last login: Wed Sep 21 11:38:36 2016 from 172.17.0.1
    kitchen@ece63fe9bcba:~$

It should login automatically.
Use it from the root dir of this module.

### Validate puppet

Run:

    puppet-lint --no-autoloader_layout-check --FIX manifests/* && \
    puppet-lint --no-autoloader_layout-check --FIX test/\*.pp && \
    rake validate

### To test with with test-kitchen

Run:

    kitchen converge -c 999 && kitchen verify -c 999
