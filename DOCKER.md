# Install with Docker

Follow these steps to get started using Docker.

1. [Install Docker](https://docs.docker.com/get-docker/)
2. Clone the repository in your projects folder
```
git clone git@github.com:Profileo/security.profileo.com.git ~/projects/security.profileo.com
```
3. Add host entry
    - on Linux, add to `/etc/hosts`
    - on Windows, add to `%SystemRoot%\system32\drivers\etc\hosts`
    - append this line: 
        ```
        127.0.0.1 security.profileo.test
        ```
4. Build and run the docker container
```
docker-compose -f ~/projects/security.profileo.com/docker-compose.yml up -d --build 
```
5. [Open the website](http://security.profileo.test)
