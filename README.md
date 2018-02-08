# protobuf 3 docker

[on docker hub](https://registry.hub.docker.com/u/calico/protoc/)

Docker image with protoc 3, gogo plugin and php 7.0.  Based on the work of
nanoservice and tigera.

## Usage

    # Just print protobuf help message
    docker run -it --rm \
      decebal2dac/protoc-php --help

    # Use current folder for input and output
    docker run -it --rm -v $PWD:/src:rw \
      decebal2dac/protoc-php --cpp_out=. *.proto

    # If you ran into problems with user uid and gid (consider scripting it)
    docker run -it --rm -v $PWD:/user-src:rw -u $(id -u):$(id -g) -w /user-src \
      decebal2dac/protoc-php --cpp_out=. *.proto

Php is installed in the docker file, as it is meant to be used with: https://github.com/lvht/protoc-gen-grpc-php. For example:

    docker run -it --rm -v $PWD:/src:rw \
      decebal2dac/protoc-php  \
      --php_out=out \
      --grpc-php_out=composer_name=Memoria/Application/Providers/Grpc:out \
      --plugin=protoc-gen-grpc-php=./vendor/bin/protoc-gen-grpc-php \
      *.proto


## Contributors

* Tigera (added gogo)
* Based on the work by [waterlink](https://github.com/waterlink) Oleksii Fedorov, creator, maintainer
* Decebal (added php 7.0)
