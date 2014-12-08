# dockerImages


A series of docker images' build files that might be useful to someone or not

Each of the folders in this repo contains the Dockerfile and other files used by
it (scripts, config files, response files, etc). However, some files like binaries,
tarballs and other files which their redistribution is not allowed or it doesn't
make sense to be included in this repo might not be included.

Please check the README.md file within each folder for specific instructions on
how to build each image.

## General notes

If you wich to modify an image used by one the other ones, please check "FROM"
instruction on the corresponding "Dockerfile" files accordingly.