# Nix

# Installation

  1. Remove the previous nix if needed 

      * `rm -rf /nix`

  2. Install[1]

      * `curl -L https://nixos.org/nix/install | sh`

  3. Configure the environment

      * `. /home/``whoami``/.nix-profile/etc/profile.d/nix.sh` 

## Isolated Enviornment 

  1. Create `shell.nix` with content

      ```
      { pkgs ? import <nixpkgs> {} }:
        pkgs.mkShell {
          # nativeBuildInputs is usually what you want -- tools you need to run
          nativeBuildInputs = [ pkgs.buildPackages.scala_2_10 ]; # <------- deps here
      }
      ```

  2. Set the environment (based on the shell.nix)[2]

      * `nix-shell shell.nix` or `nix-shell --pure shell.nix` 

          * Note: with `--pure` specified, the enviornment will be cleaned before nix shell is started.

# (Un)Install a package

  * `nix-env -iA nixpkgs.neovim`

  * `nix-env -qs`

  * `nix-env --uninstall neovim`

  * `nix-env -qs`

# Build a package from source

# References

  [1]. [Quick Install](https://nixos.org/download.html)

  [2]. [Development environment with nix-shell](https://nixos.wiki/wiki/Development_environment_with_nix-shell)

  [3]. [Isolating Development Environments Using Nix](https://dzone.com/articles/isolated-development-environment-using-nix)

  [4]. [Chapter 6. The Standard Environment](https://nixos.org/manual/nixpkgs/stable/#chap-stdenv)
