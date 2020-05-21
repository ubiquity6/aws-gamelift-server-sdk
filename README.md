# aws-gamelift-server-sdk
AWS Gamelift Server SDK 

This repo was created so we could build the AWS Gamelift Server SDK with Bazel.

## Changes
We are currently using a forked version of protobuffers in our monorepo. We need to use the same version of the library to avoid multiple definition errors. 
The .proto definition was found online, someone reverse engineered the bindings thankfully. See https://github.com/dplusic/GameLift-Server-Protobuf
The protobuf headers/impl were regenerated via these steps
```bash
cd $REPO_ROOT
bazel build @com_google_protobuf//:protoc
bazel-bin/external/com_google_protobuf/protoc -I=. --cpp_out=. sdk.proto
```
Move the generated .h and .cc files to the following paths:
1. `aws-gamelift-server-sdk/include/aws/gamelift/server/protocols`
2. `/Users/nealmanaktola/github/aws-gamelift-server-sdk/source/aws/gamelift/server/protocols`

We also modified any reference from `<sioclient/sio_client.h>` to `<sio_client.h>`. AWS cmake script created this folder. We don't need this.

