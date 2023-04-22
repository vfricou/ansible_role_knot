# Ansible Role: knot

# Disclaimer

I couldn't be responsible with any production issues if you use this role without any prior tests.  
This role is designed for my proper environment and possibly not correspond to your.

The master branch is development branch. Use only release/* branches for production.

# Introduction

This role is designed to perform postinstallation on GNU/Linux servers and to performs systems updates.  
It's structured and do tasks according to my own postinstallation and production needs.  
Feel free to fork and update this according to your requirements.

# Supported OS

**Debian** :
- bullseye (11)

**Ubuntu** :
- Jammy Jellyfish (22.04)

**Rocky** :
- 8
- 9

**AlmaLinux** :
- 8
- 9

**RHEL** :
- 8
- 9

# Requirements

## On target OS

You need to have python3 package installed on remote OS to use this role.

# Changelog

To clearest and updated changelog, I encourage you to see pull requests with flags "feature".

# Roadmap

- Manage replication
- DNSSec

# Documentation

You could read [usage documentation](./docs/usage.md) for more informations
