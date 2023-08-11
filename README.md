# Libxmlsec1

Installs libxmlsec1 at version 1.2.37

Binary available for platforms:

- arm64   ventura
- x86_64  ventura
- x86_64  monterey

If no binary is available for your platform, this formula will try to compile it for souce.

You need to have a full Xcode install to compile from source.


# Install

`brew install espressive/libxmlsec1/libxmlsec1`


# Generating new bottles

If you try to install this and see something like:

```bash
==> ./configure --prefix=/usr/local/Cellar/libxmlsec1/1.2.37 --disable-crypto-dl --disable-apps-crypto-dl --with-nss=no --with-ns
==> make install
```

It means that Homebrew could not find a binary for your platform.

To generate one:

Uninstall libxmlsec1:

```bash
brew uninstall libxmlsec1

```

Create a temporary folder to store our build artifacts in.

```bash
mkdir ~/bottlelib
cd ~/bottlelib
```

Run this command to create the bottle and keep the necesary artifacts:

```bash
HOMEBREW_NO_INSTALL_CLEANUP=1 brew install --build-bottle espressive/libxmlsec1/libxmlsec1
```

Finally, package your new bottle:

```bash
brew bottle libxmlsec1
```

This will output something like:


```bash
./libxmlsec1--1.2.37.monterey.bottle.tar.gz
  bottle do
    sha256 cellar: :any, monterey: "529ec4cc50cbc20b280ef049964916da82c22e974713fa3ef958190121984d3b"
  end

```

You need to remove one of the extra dashes in the package name ```libxmlsec1-1.2.37.monterey.bottle.tar.gz```


Then, edit ```Formula/libxmlsec1.rb``` and add your new bottle DSL to the bottle do block.

BEFORE:

```ruby
  bottle do
    root_url "https://github.com/espressive/homebrew-libxmlsec1/releases/download/libxmlsec1-1.2.37"
    sha256 cellar: :any, arm64_ventura: "0c9824df95d548e0a4b7a4421b682763625ded41b1b750cea965859982fdde37"
    sha256 cellar: :any, ventura: "f4a666f94bc02fb7d47219418e91ee60903a4e0b0d4cf0817ba024e90d228a82"
  end
```

AFTER:

```ruby
  bottle do
    root_url "https://github.com/espressive/homebrew-libxmlsec1/releases/download/libxmlsec1-1.2.37"
    sha256 cellar: :any, arm64_ventura: "0c9824df95d548e0a4b7a4421b682763625ded41b1b750cea965859982fdde37"
    sha256 cellar: :any, ventura: "f4a666f94bc02fb7d47219418e91ee60903a4e0b0d4cf0817ba024e90d228a82"
    sha256 cellar: :any, monterey: "529ec4cc50cbc20b280ef049964916da82c22e974713fa3ef958190121984d3b"
  end
```

Commit your changes to the main branch.


Finally, go [here](https://github.com/espressive/homebrew-libxmlsec1/releases/tag/libxmlsec1-1.2.37), add your new bottle tarball and update the release.

Your new bottle is now available and should install from binary next time.

You can now delete the ```~/bottlelib``` directory.


# Build with workflows.

Do not try to use the ```brew pr-pull```/```brew test-bot``` workflows to automate this, MacOS workflows are billed at 10x time, take forever and don't compile arm/universal binaries.
