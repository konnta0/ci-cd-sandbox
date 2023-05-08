# Download


## Create a folder
```shell
mkdir actions-runner && cd actions-runner
```

## Download the latest runner package
```shell
curl -o actions-runner-osx-arm64-2.304.0.tar.gz -L https://github.com/actions/runner/releases/download/v2.304.0/actions-runner-osx-arm64-2.304.0.tar.gz
```

## Optional: Validate the hash
```shell
echo "789fc57af2f0819d470fcc447e2970f201cfc8aa1d803d4e5b748ec4c5d10db8  actions-runner-osx-arm64-2.304.0.tar.gz" | shasum -a 256 -c
```

## Extract the installer
```shell
tar xzf ./actions-runner-osx-arm64-2.304.0.tar.gz
```

# Configure
## Create the runner and start the configuration experience
```shell
./config.sh --url https://github.com/konnta0/ci-cd-sandbox --token AQJY7SDZQ6Q3XILVIBKHQCLEK7JAK
```

## Last step, run it!
```
./run.sh
```

```
runs-on: self-hosted
```

ref:
https://zenn.dev/tellernovel_inc/articles/57c19694dfdf44



# Debug with act
## Install act
```shell
brew install act
```

ref:
https://github.com/nektos/act