# protobuf 3 docker

[on docker hub](https://hub.docker.com/r/decebal2dac/protoc-php/)

Docker image with protoc 3, gogo plugin and php 7.0.  Based on the work of
nanoservice and tigera.

The initial image was enriched based on this tutorial: https://grpc.io/docs/quickstart/php.html#run

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

    composer require lvht/grpc

    docker run -it --rm -v $PWD:/src:rw \
      decebal2dac/protoc-php  \
      --php_out=out \
      --grpc-php_out=composer_name=Providers/Grpc:out \
      --plugin=protoc-gen-grpc-php=./vendor/bin/protoc-gen-grpc-php \
      *.proto

### requirements 
- at the moment it needs composer installed locally, composer also is installed in the `decebal2dac/protoc-php` container, but haven't got to the part where the package is installed in it as well
- as an alternative one can just install composer locally using this one liner:

        curl -s https://getcomposer.org/installer | php && \
            mv composer.phar /usr/local/bin/composer 


## Contributors

* [Tigera](https://github.com/tigera) (added gogo)
* Based on the work by [waterlink](https://github.com/waterlink) Oleksii Fedorov, creator, maintainer
* [Decebal](https://github.com/decebal) (added php 7.0)
