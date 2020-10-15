# kitchen-docker example

This if fork of https://github.com/someara/hello_dokken reverted to use 
rather [kitchen-docker](https://github.com/test-kitchen/kitchen-docker)
instead of [kitchen-dokken](https://github.com/test-kitchen/kitchen-dokken)

Why I Use `kitchen-docker` over `kitchen-dokken`
* I encountered various Ruby version mismatches - it seems that `dokken` version
  requires that Host ruby version is same as Docker image ruby version (???)

Why I don't use Vagrant+VirtualBox driver (which is recommended driver for Kitchen).

* VirtualBox unfortunately requires one of:
  - running host OS bare-metal
  - nested virtualization support
  to run VMs

I have none of these (only OS running inside VirtualBox on Windows) :-(

# Setup

Tested on `openSUSE LEAP 15.2`

Install ruby + build environment needed for native plugins:

```bash
sudo zypper in git-core ruby ruby-devel
# required by possible native plugins
sudo zypper in -t pattern devel_C_C++
```

Install enable and start Docker:

```bash
sudo zypper in docker
sudo systemctl enable docker
sudo systemctl start docker
```

Add yourself (unprivileged) user to `docker` group using:

```bash
sudo /usr/sbin/usermod -G docker -a $USER
```

Install kitchen GEMs:

```bash
sudo gem install kitchen
sudo gem install kitchen-docker
```

Clone this project to some directory:
```bash
mkdir ~/projects
cd ~/projects
git clone https://github.com/hpaluch-pil/hello_dokken.git
```

Run `kitchen list` - may NOT report errors.

## Running Tests

Finally run `kitchen test` - this should again run without errors. It will
- run our recipe from `recipes/default.rb`
- it will test our recipe using `test/integration/default/serverspec/default_spec.rb`

Done :-)



