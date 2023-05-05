# MEMO
## local install

### Get docker-compose.yml
```sh
curl -O https://concourse-ci.org/docker-compose.yml
```

### Edit docker-compose.yml (for AppleSilicon)
```diff
       CONCOURSE_ADD_LOCAL_USER: test:test
       CONCOURSE_MAIN_TEAM_LOCAL_USER: test
       # instead of relying on the default "detect"
-      CONCOURSE_WORKER_BAGGAGECLAIM_DRIVER: overlay
       CONCOURSE_CLIENT_SECRET: Y29uY291cnNlLXdlYgo=
       CONCOURSE_TSA_CLIENT_SECRET: Y29uY291cnNlLXdvcmtlcgo=
       CONCOURSE_X_FRAME_OPTIONS: allow
       CONCOURSE_CONTENT_SECURITY_POLICY: "*"
       CONCOURSE_CLUSTER_NAME: sandbox
       CONCOURSE_WORKER_CONTAINERD_DNS_SERVER: "8.8.8.8"
-      # For ARM-based machine, change the Concourse runtime to "houdini"
-      CONCOURSE_WORKER_RUNTIME: "containerd"
+      CONCOURSE_WORKER_BAGGAGECLAIM_DRIVER: naive
+      CONCOURSE_WORKER_BAGGAGECLAIM_DISABLE_USER_NAMESPACES: true
+      CONCOURSE_WORKER_RUNTIME: "houdini"

```

ref: https://github.com/concourse/concourse/issues/8719#issuecomment-1491390779

### Login
```
fly -t sandbox login -c http://localhost:8080 -u test -p test
```

### Install fly command
```sh
curl 'http://localhost:8080/api/v1/cli?arch=amd64&platform=darwin' -o fly \
    && chmod +x ./fly && mv ./fly /usr/local/bin/
```
ref: https://concourse-ci.org/quick-start.html#install-fly

### Create example(Hello world) job
see [hello-world.yml](./hello-world.yml)

ref: https://concourse-ci.org/tutorial-hello-world.html



apply job. execute below command.
```sh
fly -t sandbox set-pipeline -p hello-world -c hello-world.yml

jobs:
  job hello-world-job has been added:
+ name: hello-world-job
+ plan:
+ - config:
+     image_resource:
+       name: ""
+       source:
+         repository: busybox
+       type: registry-image
+     platform: linux
+     run:
+       args:
+       - Hello world!
+       path: echo
+   task: hello-world-task
  
pipeline name: hello-world

apply configuration? [yN]: y
pipeline created!
you can view your pipeline here: http://localhost:8080/teams/main/pipelines/hello-world

the pipeline is currently paused. to unpause, either:
  - run the unpause-pipeline command:
    fly -t sandbox unpause-pipeline -p hello-world
  - click play next to the pipeline in the web ui
```

### Unpause pipeline
```sh
fly -t sandbox unpause-pipeline -p hello-world
```


### watch pipeline(Command line)
```sh
fly -t sandbox trigger-job --job hello-world/hello-world-job --watch
```