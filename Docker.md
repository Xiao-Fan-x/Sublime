构建Dockerfile

docker build -f  + dockerfile文件路径 -t  + 镜像名:[ tag ] (版本号)



docker 

sudo groupadd docker

sudo gpasswd -a $USER docker

newgrp docker



| shot  |                                                                                         |     chinese  |
| ---------------------------- | -------------------------------------------------------------------------------------- | ----- |
| --add-host                   | -- Add a custom host-to-IP mapping                                                     |  -- 添加自定义主机到 IP 映射                              |
| --attach                 -a  | -- Attach to stdin, stdout or stderr                                                   |   -- 附加到标准输入、标准输出或标准错误    |
| --blkio-weight               | -- Block IO (relative weight), between 10 and 1000                                     |   -- 块 IO（相对权重），在 10 到 1000 之间    |
| --blkio-weight-device        | -- Block IO (relative device weight)                                                   |   -- Block IO（相对设备权重）    |
| --cap-add                    | -- Add Linux capabilities                                                              |   -- 添加Linux功能    |
| --cap-drop                   | -- Drop Linux capabilities                                                             |   -- 放弃 Linux 功能    |
| --cgroupns                   | -- Cgroup namespace mode to use                                                        |   -- 使用的 Cgroup 命名空间模式    |
| --cgroup-parent              | -- Parent cgroup for the container                                                     |   -- 容器的父 cgroup    |
| --cidfile                    | -- Write the container ID to the file                                                  |   -- 将容器ID写入文件    |
| --cpu-period                 | -- Limit the CPU CFS (Completely Fair Scheduler) period                                |   -- 限制 CPU CFS (Completely Fair Scheduler) 周期    |
| --cpu-quota                  | -- Limit the CPU CFS (Completely Fair Scheduler) quota                                 |   -- 限制 CPU CFS (Completely Fair Scheduler) 配额    |
| --cpu-rt-period              | -- Limit the CPU real-time period                                                      |   -- 限制CPU实时周期    |
| --cpu-rt-runtime             | -- Limit the CPU real-time runtime                                                     |   -- 限制CPU实时运行时间    |
| --cpus                       | -- Number of CPUs (default 0.000)                                                      |   -- CPU 数量（默认 0.000）    |
| --cpuset-cpus                | -- CPUs in which to allow execution                                                    |   -- 允许执行的 CPU    |
| --cpuset-mems                | -- MEMs in which to allow execution                                                    |   -- 允许执行的 MEM    |
| --cpu-shares             -c  | -- CPU shares (relative weight)                                                        |   -- CPU 份额（相对权重）    |
| --detach                 -d  | -- Detached mode: leave the container running in the background                        |   -- 分离模式：让容器在后台运行    |
| --detach-keys                | -- Escape key sequence used to detach a container                                      |   -- 用于分离容器的转义键序列    |
| --device                     | -- Add a host device to the container                                                  |   -- 将主机设备添加到容器中    |
| --device-cgroup-rule         | -- Add a rule to the cgroup allowed devices list                                       |   -- 将规则添加到 cgroup 允许的设备列表    |
| --device-read-bps            | -- Limit the read rate (bytes per second) from a device                                |   -- 限制设备的读取速率（每秒字节数）    |
| --device-read-iops           | -- Limit the read rate (IO per second) from a device                                   |   -- 限制设备的读取速率（每秒 IO）    |
| --device-write-bps           | -- Limit the write rate (bytes per second) to a device                                 |   -- 限制设备的写入速率（每秒字节数）    |
| --device-write-iops          | -- Limit the write rate (IO per second) to a device                                    |   -- 限制设备的写入速率（每秒 IO）    |
| --disable-content-trust      | -- Skip image verification                                                             |   -- 跳过图像验证    |
| --dns                        | -- Custom DNS servers                                                                  |   -- 自定义 DNS 服务器    |
| --dns-option                 | -- Custom DNS options                                                                  |   -- 自定义 DNS 选项    |
| --dns-search                 | -- Custom DNS search domains                                                           |   -- 自定义 DNS 搜索域    |
| --domainname                 | -- Container NIS domain name                                                           |   -- 容器 NIS 域名    |
| --entrypoint                 | -- Overwrite the default entrypoint of the image                                       |   -- 覆盖镜像的默认入口点    |
| --env                    -e  | -- Environment variables                                                               |    -  环境变量    |
| --env-file                   | -- Read environment variables from a file                                              |   -- 从文件中读取环境变量    |
| --expose                     | -- Expose a port from the container without publishing it                              |   -- 从容器中公开一个端口而不发布它    |
| --gpus                       | -- GPU devices to add to the container ('all' to pass all GPUs)                        |   -- 要添加到容器中的 GPU 设备（'all' 表示通过所有 GPU）  |  
| --group-add                  | -- Set one or more supplementary user groups for the container                         |   -- 为容器设置一个或多个补充用户组    |
| --health-cmd                 | -- Command to run to check health                                                      |   -- 运行检查健康状况的命令    |
| --health-interval            | -- Time between running the check                                                      |   -- 运行检查之间的时间    |
| --health-retries             | -- Consecutive failures needed to report unhealthy                                     |   -- 需要报告不健康的连续失败    |
| --health-timeout             | -- Maximum time to allow one check to run                                              |   -- 允许运行一项检查的最长时间    |
| --help                       | -- Print usage                                                                         |   -- 打印使用    |
| --hostname               -h  | -- Container host name                                                                 |   -- 容器主机名    |
| --init                       | -- Run an init inside the container that forwards signals and reaps processes          |   -- 在容器内运行一个 init 来转发信号并获取进程    |
| --interactive            -i  | -- Keep stdin open even if not attached                                                |   -- 即使没有附加，也保持标准输入打开    |
| --ip                         | -- IPv4 address                                                                        |   -- IPv4 地址    |
| --ip6                        | -- IPv6 address                                                                        |   -- IPv6 地址    |
| --ipc                        | -- IPC namespace to use                                                                |   -- 要使用的 IPC 命名空间    |
| --isolation                  | -- Container isolation technology                                                      |   -- 容器隔离技术    |
| --kernel-memory              | -- Kernel memory limit in bytes                                                        |   -- 以字节为单位的内核内存限制    |
| --label                  -l  | -- Container metadata                                                                  |   -- 容器元数据    |
| --link                       | -- Add link to another container                                                       |   -- 添加到另一个容器的链接    |
| --link-local-ip              | -- Container IPv4/IPv6 link-local addresses                                            |   -- 容器 IPv4/IPv6 链路本地地址    |
| --log-driver                 | -- Default driver for container logs                                                   |   -- 容器日志的默认驱动    |
| --log-opt                    | -- Log driver specific options                                                         |   -- 记录驱动程序特定选项  |
| --mac-address                | -- Container MAC address                                                               |    -- 容器 MAC 地址   |
| --memory                 -m  | -- Memory limit                                                                        |    -- 内存限制   |
| --memory-reservation         | -- Memory soft limit                                                                   |    -- 内存软限制   |
| --memory-swap                | -- Total memory limit with swap                                                        |    -- 带交换的总内存限制   |
| --mount                      | -- Attach a filesystem mount to the container                                          |    -- 将文件系统挂载附加到容器   |
| --name                       | -- Container name                                                                      |    -- 容器名称   |
| --network                    | -- Connect a container to a network                                                    |    -- 将容器连接到网络   |
| --network-alias              | -- Add network-scoped alias for the container                                          |    -- 为容器添加网络范围的别名   |
| --no-healthcheck             | -- Disable any container-specified HEALTHCHECK                                         |    -- 禁用任何容器指定的 HEALTHCHECK   |
| --oom-kill-disable           | -- Disable OOM Killer                                                                  |    -- 禁用 OOM Killer   |
| --oom-score-adj              | -- Tune the host's OOM preferences for containers (accepts -1000 to 1000)              |    -- 调整主机对容器的OOM首选项（接受-1000到1000）   |
| --pid                        | -- PID namespace to use                                                                |    -- 要使用的 PID 命名空间   |
| --pids-limit                 | -- Tune container pids limit (set -1 for unlimited)                                    |    -- 调整容器 pids 限制（设置 -1 为无限制）   |
| --privileged                 | -- Give extended privileges to this container                                          |    -- 给这个容器扩展权限   |
| --publish                -p  | -- Expose a container's port to the host                                               |    -- 将容器的端口暴露给主机   |
| --publish-all            -P  | -- Publish all exposed ports                                                           |    -- 发布所有暴露的端口   |
| --read-only                  | -- Mount the container's root filesystem as read only                                  |    -- 将容器的根文件系统挂载为只读   |
| --restart                    | -- Restart policy                                                                      |    --重启策略   |
| --rm                         | -- Remove intermediate containers when it exits                                        |    -- 退出时移除中间容器   |
| --runtime                    | -- Name of the runtime to be used for that container                                   |    -- 用于该容器的运行时名称   |
| --security-opt               | -- Security options                                                                    |     -  安全选项   |
| --shm-size                   | -- Size of '/dev/shm' (format is '<number><unit>')                                     |    -- '/dev/shm' 的大小（格式为 '<number><unit>'）   |
| --sig-proxy                  | -- Proxy all received signals to the process (non-TTY mode only)                       |    -- 将所有接收到的信号代理到进程（仅限非 TTY 模式）   |
| --stop-signal                | -- Signal to kill a container                                                          |    -- 杀死一个容器的信号   |
| --stop-timeout               | -- Timeout (in seconds) to stop a container                                            |    -- 停止容器的超时（以秒为单位）   |
| --storage-opt                | -- Storage driver options for the container                                            |    -- 容器的存储驱动选项   |
| --sysctl                     | -- sysctl options                                                                      |    -- sysctl 选项   |
| --tmpfs                      | -- mount tmpfs                                                                         |    -- 挂载 tmpfs   |
| --tty                    -t  | -- Allocate a pseudo-tty                                                               |    -- 分配一个伪tty   |
| --ulimit                     | -- ulimit options                                                                      |    -- ulimit 选项   |
| --user                   -u  | -- Username or UID                                                                     |    -- 用户名或 UID   |
| --userns                     | -- Container user namespace                                                            |    -- 容器用户命名空间   |
| -v                           | -- Bind mount a volume                                                                 |    -- 绑定挂载卷   |
| --volume-driver              | -- Optional volume driver for the container                                            |    -- 容器的可选卷驱动程序   |
| --volumes-from               | -- Mount volumes from the specified container                                          |    -- 从指定容器挂载卷   |
| --workdir                -w  | -- Working directory inside the container  | -- 容器内的工作目录 |