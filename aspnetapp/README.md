# ASP.NET Core Docker 生产示例

这个 ASP.NET Core Docker 示例示范了一个用于构建生产上 ASP.NET 应用 Docker 镜像的最佳实践模式。这个示例能够同时工作在 Linux 和 Windows 容器。

[示例 Dockerfile](Dockerfile) 创建了一个 ASP.NET Core 应用 Docker 镜像，基于 [ASP.NET Core Runtime 基础镜像](https://hub.docker.com/r/microsoft/aspnetcore/).

它使用了 [Docker 多阶段构建](https://github.com/dotnet/announcements/issues/18) ，先在一个基于更大的 [ASP.NET Core 构建时基础镜像](https://hub.docker.com/r/microsoft/aspnetcore-build/) 的容器中构建示例程序，然后拷贝最终构建结果到一个更小的 [ASP.NET Core Docker 运行时基础镜像](https://hub.docker.com/r/microsoft/aspnetcore/)。 构建时镜像包含了用于构建应用程序所必须的工具，而运行时镜像并没有。 

这个示例需要 [Docker 17.03](https://docs.docker.com/release-notes/docker-ce) 或以上的 [Docker 客户端](https://www.docker.com/products/docker)。使用 [Windows 容器](http://aka.ms/windowscontainers)，你需要最新的 Windows 10 或者 Windows Server 2016。 以下指令假定你已有安装好的 [Git](https://git-scm.com/downloads) 客户端。

## 获取示例

最简单的方式来获得这个示例，是通过 Git 使用以下的指令来克隆这个仓库。 你也可以仅仅从 [.NET Core Docker samples](https://github.com/dotnet/dotnet-docker-samples/) 仓库下载它的 zip 压缩包（非常小）。

```console
git clone https://github.com/dotnet/dotnet-docker-samples/
```

## 构建并运行 Windows 容器下的这个示例

你可以使用以下命令来构建并运行 Windows 容器下的这个示例。该指令假定你在该仓库的根目录。

```console
cd aspnetapp
docker build -t aspnetapp .
docker run -it --rm --name aspnetcore_sample aspnetapp
```

当你使用 Windows 容器时，你必须在浏览器里，直接通过容器 IP（相对于 http://localhost ）来访问。
你可以通过以下步骤来获得你容器的 IP 地址：

1. 打开一个新的 CMD 窗口。
1. 运行 `docker ps` 来查看所有运行的容器。应该能看到 “aspnetcore_sample” 容器。
1. 运行 `docker exec aspnetcore_sample ipconfig`。
1. 拷贝容器 IP 地址，然后复制到你的浏览器（例如 `172.29.245.43`）。

注意： `docker exec` 支持通过名字或者哈希号来区分容器。 上面使用的是容器名。

以下样例展示了如何从一个运行中的 Windows 容器中获得 IP 地址。

```console
C:\git\dotnet-docker-samples\aspnetapp>docker exec aspnetcore_sample ipconfig

Windows IP Configuration


Ethernet adapter Ethernet:

   Connection-specific DNS Suffix  . : contoso.com
   Link-local IPv6 Address . . . . . : fe80::1967:6598:124:cfa3%4
   IPv4 Address. . . . . . . . . . . : 172.29.245.43
   Subnet Mask . . . . . . . . . . . : 255.255.240.0
   Default Gateway . . . . . . . . . : 172.29.240.1
```

注意：`Docker exec` 运行了一个新的命令。 查看 [Docker exec reference](https://docs.docker.com/engine/reference/commandline/exec/) 来获得更多的命令行参数。

## 构建并运行 Linux 容器下的这个示例

你可以使用以下命令来构建并运行 Linux 容器下的这个示例。该指令假定你在该仓库的根目录。

```console
cd aspnetapp
docker build -t aspnetapp .
docker run -it --rm -p 8000:80 --name aspnetcore_sample aspnetapp
```

在应用程序启动后，通过浏览器来访问 `http://localhost:8000`。

注意：`-p` 参数把你本地机器的 8000 端口映射到容器的 80 端口（端口映射的形式是 `host:container`）。查看 [Docker run reference](https://docs.docker.com/engine/reference/commandline/run/) 来获得更多的命令行参数信息。

## 本地构建并运行示例

你可以通过 [.NET Core 2.0 SDK](https://www.microsoft.com/net/download/core)，结合以下命令，在本地构建并运行这个示例。这些指令假定你在该仓库的根目录。

```console
cd aspnetapp
dotnet run
```


在应用程序启动后，通过浏览器来访问 `http://localhost:8000`。

你可以在本地，使用以下命令，制作一个准备好发布到生产的应用程序。

```console
dotnet publish -c release -o published
```

你可以通过以下命令在 **Windows** 上运行这个应用。

```console
dotnet published\aspnetapp.dll
```


你可以通过以下命令在 **Linux 或 macOS** 上运行这个应用。

```console
dotnet published/aspnetapp.dll
```

注意：`-c release` 参数会在 release 模式（默认是 debug 模式）构建这个应用程序。 查看 [dotnet run reference](https://docs.microsoft.com/dotnet/core/tools/dotnet-run) 来获得更多的命令行参数信息。

## 本例使用的 Docker 镜像

本例中使用了以下 Docker 镜像

* [microsoft/aspnetcore-build:2.0](https://hub.docker.com/r/microsoft/aspnetcore-build)
* [microsoft/aspnetcore:2.0](https://hub.docker.com/r/microsoft/aspnetcore/)

## 相关资源

* [ASP.NET Core Getting Started Tutorials](https://www.asp.net/get-started)
* [.NET Core Production Docker sample](../dotnetapp-prod/README.md)
* [.NET Core Docker samples](../README.md)
* [.NET Framework Docker samples](https://github.com/Microsoft/dotnet-framework-docker-samples)
