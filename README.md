# Nix Workshop Part 2: NixOS
Notes for part 2-of-2 of my introductory Nix workshop

Link to the recording: https://youtu.be/T58ml5SmkNM

# Overview

## What you'll learn today:
- What is NixOS?
- How is NixOS different from using the Nix package manager on MacOS or other Linux distros?
- How do you install and configure NixOS?

# What is NixOS?

- Start with the Nix package manager / build tool, and build an entire Linux distro from the ground up using Nix.
- 

# Installing NixOS

- Download ISO image from https://nixos.org
- Write to USB drive, boot from USB drive
- Follow graphical installer, choose Desktop Environment (DE)

# Configuring NixOS

## Enable flakes
- Navigate to `/etc/nix` and notice two files:
```bash
/etc/nixos
❯ ls -1
configuration.nix
hardware-configuration.nix
```
- Edit the file `/etc/nixos/configuration.nix`
- Add the following line to enable flakes:
```
{ config, pkgs, ... }:

{
  imports =
    [ 
      ./hardware-configuration.nix
    ];

  # Enable Flakes and the new command-line tool
  nix.settings.experimental-features = [ "nix-command" "flakes" ];

  environment.systemPackages = with pkgs; [
    # Flakes use Git to pull dependencies from data sources 
    git
    vim
    wget
    curl
  ];
  # Set default editor to vim
  environment.variables.EDITOR = "vim";

}
```



## Add desired packages

# Resources
- https://nixos-and-flakes.thiscute.world
- Watch this to learn how to configure Nix (with Home-Manager) and/or NixOS: https://youtu.be/a67Sv4Mbxmc
- https://nixos.wiki
Recording of this Nix workshop (Part 1): https://www.youtube.com/watch?v=glQoiK5DOZY
