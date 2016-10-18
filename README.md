# Puppet module generator scripts

Example of usage:

    cd /tmp
    wget -O generate-puppet-module-with-test-kitchen.sh https://gist.githubusercontent.com/jecnua/57024265332c03e9edd70647473a793e/raw/puppet-module-with-test-kitchen-generate
    chmod 700 generate-puppet-module-with-test-kitchen.sh
    ./generate-puppet-module-with-test-kitchen.sh aaa bbb

## TODO

- Fix test BEFORE rubocop
- Next step curl-bash it
- Clean kitchen.yml from all comments and put a new file for that
- Add vagrant file with test
