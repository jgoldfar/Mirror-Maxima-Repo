# Maxima Mirror Auto-Updater

[![Build Status](https://travis-ci.org/jgoldfar/Mirror-Maxima-Repo.svg?branch=master)](https://travis-ci.org/jgoldfar/Mirror-Maxima-Repo)

I created this repository to see how difficult it would be to set up an automated git mirror; turns out, this isn't too tricky at all!
This repository mirrors the upstream [Maxima Sourceforge Repository](http://maxima.sourceforge.net/) to a [github clone](https://github.com/jgoldfar/maxima-clone); to avoid having to deal with hosting, I simply use Travis to execute those instructions.
To do that, we'll need push access to my clone to be granted to Travis.

1) Generate a new key (easier to revoke if compromised)

```shell
ssh-keygen -t rsa -b 4096 -C "jgoldfar+docker@gmail.com" -f id_rsa -P ""
cat id_rsa.pub
```

2) Copy the public key to a [deploy key on GitHub](https://developer.github.com/v3/guides/managing-deploy-keys/#deploy-keys).

3) Encrypt the private key and store the encrypted version on the server:

```shell
travis encrypt-file id_rsa --add
rm id_rsa id_rsa.pub
git add id_rsa .travis.yml
```

## Contact

Feel free to open an issue or PR to contribute, or contact me at jgoldfar@my.fit.edu.

## Changelog

* An issue arose on the regular cron run on 3/1/2019 due to a change in configuration on the Sourceforge servers (most likely.) This was fixed by upgrading the image used to run the build on Travis to Ubuntu Xenial. At the same time, I reduced the image to the `minimal` version should eliminate some cruft from the build environment.
