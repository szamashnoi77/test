#!/usr/bin/make
#
# Update the repository every time when a new package arrives

all: repo

repo: dists/xenial/InRelease dists/xenial/Release.gpg

dists/xenial/InRelease: dists/xenial/Release
        gpg --clearsign --digest-algo SHA512 -o dists/xenial/InRelease.new dists/xenial/Release
        mv dists/xenial/InRelease.new dists/xenial/InRelease

dists/xenial/Release.gpg: dists/xenial/Release
        gpg -abs -o dists/xenial/Release.gpg-new dists/xenial/Release
        mv dists/xenial/Release.gpg-new dists/xenial/Release.gpg

dists/xenial/Release: conf/distributions contrib/binary-amd64/Packages.gz
        cat conf/distributions > dists/xenial/Release
        apt-ftparchive release . >> dists/xenial/Release

contrib/binary-amd64/Packages.gz: contrib/binary-amd64/Packages
        gzip --keep --force -9 ../../contrib/binary-amd64/Packages

contrib/binary-amd64/Packages: contrib/binary-amd64/*.deb
        dpkg-scanpackages contrib/binary-amd64 > contrib/binary-amd64/Packages.new
        mv contrib/binary-amd64/Packages.new contrib/binary-amd64/Packages
