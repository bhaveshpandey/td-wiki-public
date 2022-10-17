# Nix


* [Derivations](derivation.md)
* [Flakes](flake.md)


## Nix Repl

* nix repl

```sh

pkgs = import <nixpkgs> {}
"${pkgs.redis}"
"${pkgs.openimageio}"
```


## Nix build

Nix can also be used as a software build system. It uses a `.nix` file to describe the build process.
Following is an example build file.
```nix

let
    pkgs = import <nixpkgs> {};
in pkgs.runCommand "build-name" {buildInputs=[];}
    ''
    echo "Copying file:  ${./README.md}"
    cat ${./README.md}
    cp ${./README.md} $out
    ''
```

We can then build the package using the `nix-build` command as follows.
```sh

nix-build /path/to/example.nix
```

We can also trace the derivations used for builds as follows.

```sh

nix-store -q --deriver /nix/store/8rccg4ywzlbcbrwm24ahj9riya8xdr16-aces-1.2
# Output of above command is the absolute path of the derivation used for the build as shown below:
# /nix/store/ifvbaha1nwjnx1wh0amy6942s3c4iv0b-aces-1.2.drv

# We can further trace the dependencies of the derivation shown above by using the `--requisites / -R` flag
nix-store -qR /nix/store/ifvbaha1nwjnx1wh0amy6942s3c4iv0b-aces-1.2.drv
nix-store -q --requisites /nix/store/ifvbaha1nwjnx1wh0amy6942s3c4iv0b-aces-1.2.drv
```

We can also show the contents/definition of the derivations as follows:

```sh
nix show-derivation /nix/store/ifvbaha1nwjnx1wh0amy6942s3c4iv0b-aces-1.2.drv
```


## Queries

```sh

nix-env --query
nix-env --query --available --attr-path
nix-env --query --available --attr-path --attr <ATTRIBUTE>
# Query output paths of installed packages
nix-env -q --out-path

# Query derivations for installed packages
nix-env -q --out-path | awk '{print $2}' | xargs nix-store -q
```

## Install/Remove

```sh

nix-env --install --attr <ATTRIBUTE>
nix-env --uninstall <NAME>
# Following command can be used to install a custom build package
nix-env -i /path/to/the/derivation/file.drv
```

## Upgrade

nix-env --upgrade
nix-channel --update


## Rollback

nix-env --rollback
nix-channel --rollback


## Nix Shell Environments

Open a shell with packages made temporarily available (similar to pipenv/virtualenv)

```sh

nix-shell -p kafkacat

# Following command will initialize a shell with python310, gcc and cmake installed
nix-shell -p python310 gcc cmake

# To completely isolate the shell from any external dependencies use `--pure` flag
nix-shell -p --pure python310 gcc cmake
```


## Nix store

Following command lets us query all the dead/unused derivations

```sh

nix-store --gc --print-dead
```

nix-store --query --graph /nix/store/z5c1adn3a9kla7a7axdsgnina24dbbi9-redpanda-21.11.15
nix-store --query --referrers /nix/store/1c1mm4kw1rz5jjdx1vw1k19xrfnvcd40-bison-3.7.6.drv
nix-store --query --references /nix/store/1c1mm4kw1rz5jjdx1vw1k19xrfnvcd40-bison-3.7.6.drv
nix-store --query --derivers /nix/store/1c1mm4kw1rz5jjdx1vw1k19xrfnvcd40-bison-3.7.6.drv
nix-store --query --tree /nix/store/1c1mm4kw1rz5jjdx1vw1k19xrfnvcd40-bison-3.7.6.drv
nix-store --query --requisites /nix/store/1c1mm4kw1rz5jjdx1vw1k19xrfnvcd40-bison-3.7.6.drv
nix-store --dump-db /nix/store/1c1mm4kw1rz5jjdx1vw1k19xrfnvcd40-bison-3.7.6.drv

nix why-depends /nix/store/1c1mm4kw1rz5jjdx1vw1k19xrfnvcd40-bison-3.7.6.drv /nix/store/ngsrqrziiw0hzwyi52m42mpabclnad8g-redpanda-21.11.15.drv --extra-experimental-features nix-command


## Using Nix repl for testing builds

We can use the `nix repl` command to quickly and interactively build packages or build experimental packages.

```sh

nix repl
Welcome to Nix 2.11.1. Type :? for help.

nix-repl> nixpkgs = import <nixpkgs> {}

nix-repl> nixpkgs.stdenv.mkDerivation {
            name = "env";
            unpackPhase = "true";
            installPhase = "env > $out";
          }
```


## References

* [Installing from local repo](https://nixos.wiki/wiki/Nixpkgs/Create_and_debug_packages#How_to_install_from_the_local_repository)
* [Intro to Pkgs-make](https://github.com/shajra/example-nix/blob/master/tutorials/1-pkgs-make/README.md)
* [Nix Derivation Basics](https://scrive.github.io/nix-workshop/04-derivations/01-derivation-basics.html)
* [Nix Based C++ Workflow From Scratch](https://www.breakds.org/post/nix-based-c++-workflow/)
