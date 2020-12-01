#### docker在window10的powershell中启动失败
```
    解决问题的issue:
        https://github.com/docker/for-win/issues/1825
    场景：
        安装完docker重启后，在powershell中输入启动命令报错，
        error during connect: Get http://%2F%2F.%2Fpipe%2Fdocker_engine/v1.35/info: open //./pipe/docker_engine: The system cannot find the file specified. In the default daemon configuration on Windows, the docker client must be run elevated to connect. This error may also indicate that the docker daemon is not running.

    解决办法：
        在powershell中输入命令
        提升权限：
            cd "C:\Program Files\Docker\Docker"
            ./DockerCli.exe -SwitchDaemon
        启动docker:
            docker run -d -p 80:80 docker/getting-started
            
```