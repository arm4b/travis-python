# Vagrant with Travis Python env
Vagrantfile to build Travis environment with Python, RabbitMQ and MongoDB.

Since [Travis-CI](https://travis-ci.org/) doesn't have remote SSH debug option, Vagrant image is useful for debugging and testing Travis builds.

### Get started
Clone with `recursive` flag to fetch dependency repo with [Travis cookbooks](https://github.com/travis-ci/travis-cookbooks/):
```sh
git clone --recursive https://github.com/armab/travis-python.git

vagrant up
vagrant ssh

# activate Travis Python 2.7 virtualenv
source ~/virtualenv/python2.7/bin/activate
```

### Why?
> Used to troubleshoot [StackStorm](https://github.com/StackStorm/st2/blob/master/.travis.yml) Travis-CI builds with complex configurations, [travis.yml](https://github.com/StackStorm/st2/blob/master/.travis.yml)
