# .NET Core Docker 生产示例

这个 .NET Core Docker 示例示范了一个用于构建生产上 .NET Core 应用 Docker 镜像的最佳实践模式。这个示例能够同时工作在 Linux 和 Windows 容器。

该 [示例 Dockerfile](Dockerfile) 创建了一个 .NET Core 应用程序 Docker 镜像，基于 [.NET Core 运行时 Docker 基础镜像](https://hub.docker.com/r/microsoft/dotnet/)。

它使用了 [Docker 多阶段构建特性](https://github.com/dotnet/announcements/issues/18) ，在一个基于更大的 [.NET Core SDK Docker 基础镜像](https://hub.docker.com/r/microsoft/dotnet/)的容器中构建该示例，然后拷贝最终构建结果到一个更小的 [.NET Core Docker 运行时基础镜像](https://hub.docker.com/r/microsoft/dotnet/)。构建时镜像包含了用于构建应用程序所必须的工具，而运行时镜像并没有。

这个示例需要 [Docker 17.03](https://docs.docker.com/release-notes/docker-ce) 或以上的 [Docker 客户端](https://www.docker.com/products/docker)。使用 [Windows 容器](http://aka.ms/windowscontainers)，你需要最新的 Windows 10 或者 Windows Server 2016。 以下指令假定你已有安装好的 [Git](https://git-scm.com/downloads) 客户端。

## 获取示例

最简单的方式来获得这个示例，是通过 Git 使用以下的指令来克隆这个仓库。 你也可以仅仅从 [.NET Core Docker samples](https://github.com/dotnet/dotnet-docker-samples/) 仓库下载它的 zip 压缩包（非常小）。

```console
git clone https://github.com/dotnet/dotnet-docker-samples/
```

## 使用 Docker 构建并运行示例

你可以通过以下命令来使用 Docker 构建并运行这个示例。这些指令假定你在该仓库的根目录。

```console
cd dotnetapp-prod
docker build -t dotnetapp-prod .
docker run --rm dotnetapp-prod Hello .NET Core from Docker
```

注意：这些指令能同时工作于 Linux 和 Windows 容器。.NET Core docker 镜像使用了 [多架构标签](https://github.com/dotnet/announcements/issues/14), 它对不同使用场景，抽象出了不同的操作系统。

## 在 Windows 或者 macOS 上构建，然后在 Linux 和 ARM32 (树莓派)上使用 docker 运行本示例。

本节的目标是，在一个运行 Linux 的树莓派上创建并运行一个 Docker .NET Core 运行时镜像。.NET Core SDK 不能运行于 Linux + ARM32 的配置。因此，X64 上使用的指令并不能工作。 有很多方式来绕过这个限制，主要是：

* 在 X64 构建应用，然后通过 scp (或者 pscp)  拷贝到 ARM32 设备。接着在 ARM32 设备上构建并且运行一个 Docker 运行时镜像，或者
* 在 Windows 上构建最终的 ARM32 镜像，推送这个镜像到一个 Docker 镜像仓库，然后拉取并且运行在 ARM32 设备上。

第二个选择仅支持 Windows。Linux 和 macOS 用户第一个方法。为简单起见，下面提供了 Windows 选项。

这些指令假定你在该仓库的根目录。

在 Windows 上 Docker “Linux 模式”下，输入以下的命令。这些指令假设你有一个个人的 Docker 用户帐号，名为 `mydockername`。你需要将它改为你真正的 docker 帐号名，比如这个示例的作者 [richlander](https://hub.docker.com/u/richlander/)。 你也需要创建一个名叫 `dotnetapp-prod-arm32` 的 Docker 仓库。你可以在 Docker web 界面创建一个新的仓库。

你需要登录 Docker 客户端来使用 `docker push` 推送镜像到 Docker Hub。

```console
cd dotnetapp-prod
docker build -t mydockername/dotnetapp-prod-arm32 -f Dockerfile.arm32 .
docker push mydockername/dotnetapp-prod-arm32
```

切换到你已经装好 Linux 和 Docker 的树莓派。输入以下命令。

```console
docker run --rm mydockername/dotnetapp-prod-arm32 Hello .NET Core from Docker
```

## 本地构建并运行示例

你可以通过以下命令使用 [.NET Core 2.0 SDK](https://www.microsoft.com/net/download/core) 在本地构建并运行这个示例。这些指令假定你在该仓库的根目录。

```console
cd dotnetapp-prod
dotnet run Hello .NET Core
```

你可以在本地，使用以下命令，制作一个准备好发布到生产的应用程序。

```console
dotnet publish -c release -o published
```

你可以通过以下命令在 **Windows** 上运行这个应用。

```console
dotnet published\dotnetapp.dll
```

你可以通过以下命令在 **Linux 或 macOS** 上运行这个应用。

```console
dotnet published/dotnetapp.dll
```

注意：`-c release` 参数会在 release 模式（默认是 debug 模式）构建这个应用程序。 查看 [dotnet run reference](https://docs.microsoft.com/dotnet/core/tools/dotnet-run) 来获得更多的命令行参数信息。

## 本例使用的 Docker 镜像

本例中使用了以下 Docker 镜像。
* [microsoft/dotnet:2.0-sdk](https://hub.docker.com/r/microsoft/dotnet)
* [microsoft/dotnet:2.0-runtime](https://hub.docker.com/r/microsoft/dotnet)

## 相关资源

* [ASP.NET Core Production Docker sample](../aspnetapp/README.md)
* [.NET Core Docker samples](../README.md)
* [.NET Framework Docker samples](https://github.com/Microsoft/dotnet-framework-docker-samples)
