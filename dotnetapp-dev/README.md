# .NET Core 开发示例

本 .NET Core docker 示例示范了如何在你的 .NET Core 开发过程中使用 Docker。该示例同时适用于 Windows 和 Linux 容器。

该 [示例 Dockerfile](Dockerfile) 创建了一个 .NET Core 应用程序镜像，基于 [.NET Core SDK Docker 基础镜像](https://hub.docker.com/r/microsoft/dotnet/)。它构建并且运行应用程序在同一个镜像中，这是一个对于交互式开发非常有用，但不是生产上最佳的策略。对于面向生产的示例请看 [.NET Core Production Sample](../dotnetapp-prod/README.md) 或者 [ASP.NET Core Production Sample](../aspnetapp/README.md)。

这个示例需要 [Docker 17.03](https://docs.docker.com/release-notes/docker-ce) 或以上的 [Docker 客户端](https://www.docker.com/products/docker)。使用 [Windows 容器](http://aka.ms/windowscontainers)，你需要最新的 Windows 10 或者 Windows Server 2016。 以下指令假定你已有安装好的 [Git](https://git-scm.com/downloads) 客户端。

## 获取示例

最简单的方式来获得这个示例，是通过 Git 使用以下的指令来克隆这个仓库。 你也可以仅仅从 [.NET Core Docker samples](https://github.com/dotnet/dotnet-docker-samples/) 仓库下载它的 zip 压缩包（非常小）。

```console
git clone https://github.com/dotnet/dotnet-docker-samples/
```

## 使用 Docker 构建并运行示例

你可以通过以下命令来使用 Docker 构建并运行这个示例。这些指令假定你在该仓库的根目录。

```console
cd dotnetapp-dev
docker build -t dotnetapp-dev .
docker run --rm dotnetapp-dev Hello .NET Core from Docker
```

注意：这些指令能同时工作于 Linux 和 Windows 容器。.NET Core docker 镜像使用了 [多架构标签](https://github.com/dotnet/announcements/issues/14), 它对不同使用场景，抽象出了不同的操作系统。

## 本地构建并运行示例

你可以通过以下命令使用 [.NET Core 2.0 SDK](https://www.microsoft.com/net/download/core) 在本地构建并运行这个示例。这些指令假定你在该仓库的根目录。

```console
cd dotnetapp-dev
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

本例中使用了以下 Docker 镜像

* [microsoft/dotnet:2.0-sdk](https://hub.docker.com/r/microsoft/dotnet)

## 相关资源

* [.NET Core Docker samples](../README.md)
* [.NET Framework Docker samples](https://github.com/Microsoft/dotnet-framework-docker-samples)
