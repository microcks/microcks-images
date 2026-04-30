# microcks-images

Base container images used by Microcks

[![License](https://img.shields.io/github/license/microcks/microcks?style=for-the-badge&logo=apache)](https://www.apache.org/licenses/LICENSE-2.0)
[![Project Chat](https://img.shields.io/badge/discord-microcks-pink.svg?color=7289da&style=for-the-badge&logo=discord)](https://microcks.io/discord-invite/)


## Build locally

### On MacOS

Donwload pre-requisites:

```sh
curl -Lo ./jam https://github.com/paketo-buildpacks/jam/releases/download/v2.17.3/jam-darwin-arm64 \
            && mv ./jam ./cloud-native-buildpacks/jam \
            && chmod u+x ./cloud-native-buildpacks/jam

curl -L -O https://github.com/buildpacks/pack/releases/download/v0.38.2/pack-v0.38.2-macos.tgz \
            && tar xvf pack-v0.38.2-macos.tgz \
            && mv ./pack ./cloud-native-buildpacks/pack \
            && chmod u+x ./cloud-native-buildpacks/pack
```

Build stack and buildpack:

```sh
cd ./cloud-native-buildpacks
mkdir build
./jam create-stack --config noble-tiny.stack.toml --build-output build/build.oci --run-output build/run.oci
./jam publish-stack --build-ref lbroudoux/build-noble-tiny:latest \
    --run-ref lbroudoux/run-noble-tiny:latest \
    --build-archive build/build.oci \
    --run-archive build/run.oci
./pack builder create lbroudoux/builder-noble-java-tiny:latest --config noble-java-tiny.builder.toml --publish
```

