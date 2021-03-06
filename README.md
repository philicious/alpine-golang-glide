# alpine-golang-glide

Docker image that uses the latest and stable Golang and Glide as Package Dependency

NOTE: `latest` docker tag is now deprecated and will no longer be maintained. Kindly use the specific docker tag name.
`latest` tag is equivalent to tag `1.0.0`


OFFICIAL DOCKER TAGS WITH APPLICATION VERSIONS: 

Tags     | Golang | Glide   | GIT    | Make  | Alpine Base
---      | ---    | ---     | ---    | ---   | ---
1.2.0    | 1.8.0  | 0.12.3  | 2.11.1 | 4.2.1 | 3.5
1.1.1    | 1.7.5  | 0.12.3  | 2.11.1 | 4.2.1 | 3.5 
1.1.0    | 1.7.3  | 0.12.3  | 2.11.1 | 4.2.1 | 3.5
1.0.0    | 1.6.3  | 0.12.3  | 2.8.3  | 4.1.0 | 3.4
latest   | 1.6.3  | 0.12.3  | 2.8.3  | 4.1.0 | 3.4

* docker tagging is based on the golang upgrades.

Build-and-Run on the fly. This image also supports cMake for Makefile

Compiler and the `bin` file (go build) are compatible with Alpine.

To be able to support keyless authentication in pulling private repositories (e.g bitbucket), I've added `run-ssh` command so that users can mount their private keys (e.g ~/.ssh/id_rsa) and the identity will be added when `run-ssh` command is invoked.

## Example

`docker run --rm --privileged -v $HOME/.ssh:/tmp/ssh -v $PWD:/go/src/<package-name-in-your-glide> -w /go/src/<package-name-in-your-glide> billyteves/alpine-golang-glide:latest bash -c 'run-ssh && make'`

the `<package-name-in-your-glide>` shoule be the same path and value of your glide.yaml file. If not, errors will occur as your local vendor go library.

You can optionally remove the SSH if you are using a public repository as your go-library.

`docker run --rm -v $PWD:/go/src/<package-name-in-your-glide> -w /go/src/<package-name-in-your-glide> billyteves/alpine-golang-glide:latest bash -c 'make'`
