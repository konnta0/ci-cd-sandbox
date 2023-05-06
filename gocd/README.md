### Minimal example of a GoCD pipeline
```sh
curl -fsSL 'https://www.gocd.org/test-drive-gocd/try.sh' | bash -s 'https://download.gocd.org/test-drive/installers/23.1.0/16079/gocd-23.1.0-16079-2164-osx-aarch64.zip'
```

```sh
cd  gocd-23.1.0-16079-2164
./run-gocd
```





### Use Docker to run the application
```sh
docker run -d -p8153:8153 gocd/gocd-server:v23.1.0
```


ref: https://github.com/gocd/docker-gocd-server