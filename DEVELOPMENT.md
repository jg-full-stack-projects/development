# Required tools
The tools required to run this are listed below

|Tool|OS|Notes|
|---|---|---|
|Docker Compose|Any|Extra steps required if you opt for Podman, Docker is recomemended if podman is not pre-installed|
|Docker|Any|You can choose either Docker or Podman as the backend. If you are not familiar Docker is highly recommended|
|Podman|Any|See the notes above|

## Running Docker Compose with podman as the backend
If you are not installing Docker and want to run Podman as the container backend an extra step is required to redirect to the podman socket instead of the standard docker socket.

First we need to activate the podman socket service and start it
```
systemctl enable --user --now podman.socket
```

And point the DOCKER\_SOCKET to the podman socket 
`export DOCKER_HOST=unix:///run/user/$UID/podman/podman.sock`. 

**It is recommended to make these changes persistent by puttng them in your shell rc file (.bashrc,.zshrc etc.).** 
For exapmle if you are using ZSH run 
```
echo "export DOCKER_HOST=unix:///run/user/$UID/podman/podman.sock" >> ~/.zshrc
```

For Bash (run this if you don't know which shell you are running) you need to run 
```
echo "export DOCKER_HOST=unix:///run/user/$UID/podman/podman.sock" >> ~/.bashrc
```

when that is done we need to get the docker-compose standalone binary, make sure `jq` is installed on your system.
```
# Systemwide install
DC_VERSION=$(curl https://api.github.com/repos/docker/compose/releases/latest | jq .name -r); sudo curl -SL https://github.com/docker/compose/releases/download/$DC_VERSION/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose; sudo chmod +x /usr/local/bin/docker-compose

# Install it on your local user
DC_VERSION=$(curl https://api.github.com/repos/docker/compose/releases/latest | jq .name -r); curl -SL https://github.com/docker/compose/releases/download/$DC_VERSION/docker-compose-linux-x86_64 -o ~/.local/bin/docker-compose; chmod +x $_
```

## Running the projects
Now that everything needed is installed we can proceed to running the projects in this Organisation

- Run the local dev environment
    ```
    # In case of the standalone binary 
    docker-compose -f docker-compose.yml -f docker-compose.dev.yml up --build
    # In case of the plugin
    docker compose -f docker-compose.yml -f docker-compose.dev.yml up --build
    ```
- Run the test suite
    ```
    # In case of the standalone binary 
    docker-compose -f docker-compose.yml -f docker-compose.test.yml up --build --abort-on-container-exit
    # In case of the plugin
    docker compose -f docker-compose.yml -f docker-compose.test.yml up --build --abort-on-container-exit
    ```
- Run the production code
    ```
    # In case of the standalone binary 
    docker-compose -f docker-compose.yml up -d
    # In case of the plugin
    docker compose -f docker-compose.yml up -d
    ```
