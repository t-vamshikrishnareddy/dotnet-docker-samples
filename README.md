# .NET Core Docker 示例
本仓库维护着多种 .NET 核心的 Docker 配置示例，你可以用于自己的 Docker 镜像。
它们也是广泛有用的 .NET 示例，提供了一些指令来针对使用 Docker 和不使用 Docker 两种场景。

这些示例依赖于 [.NET Core Docker 镜像](https://hub.docker.com/r/microsoft/dotnet/)。

我们使用 [dotnetbot](https://github.com/dotnet-bot) 来演示，它是 .NET 开源项目的吉祥物。 示例项目 [dotnetapp-dev](dotnetapp-dev)，[dotnetapp-prod](dotnetapp-prod) 和 [dotnetapp-selfcontained](dotnetapp-selfcontained) 都是简单地在控制台打印一个 “Welcome!” 消息。[aspnetapp](aspnetapp) 则是启动了一个运行在容器中的基础的 ASP.NET 网站，你可以通过浏览器来访问。

你可以选择一个最适合你场景的示例程序。各个示例的指令描述了如何在 Windows，Linux 或者 macOS 上最终生成一个 [Windows](http://aka.ms/windowscontainers) 或者 Linux Docker 镜像。

这些示例使用了 .NET Core 2.0。 根据情况，它们使用了 Docker [多阶段构建](https://github.com/dotnet/announcements/issues/18) 和 [多架构标签](https://github.com/dotnet/announcements/issues/14)。

你需要安装好 [.NET Core SDK](https://www.microsoft.com/net/download/core#/sdk) 和 [Git](https://git-scm.com/downloads) 和 [Docker client 17.06 or newer](https://www.docker.com/products/docker) 客户端来使用这些示例程序。

## 马上开始

你可以直接运行一个已经构建好并发布到 Docker Hub 的 [示例程序](https://hub.docker.com/r/microsoft/dotnet-samples/)。 这个示例程序的源代码在 [dotnetapp-prod](dotnetapp-prod)。

运行 **Linux** 镜像：

```console
docker run microsoft/dotnet-samples
```

运行 **Windows** 镜像：

```console
docker run microsoft/dotnet-samples:dotnetapp-nanoserver
```

我们推荐运行这个示例两次。第二次运行将不包括下载这个镜像，这也是更典型更常见的 Docker 使用方式。

## 示例

接下来的示例展示了 .NET Core 镜像的不同使用方式。

### 开发

* [.NET Core Development Sample](dotnetapp-dev) - 这个示例适于开发和构建，因为它依赖于 .NET Core SDK 镜像。它会帮你执行 `dotnet` 命令，减少了它需要用于构建 Docker 镜像的时间（假定你在容器内交互式地改动和测试它们）。

### 生产

* [.NET Core Docker Production Sample](dotnetapp-prod) - 这个示例适于生产，因为它依赖于 .NET Core Runtime 镜像, 而不是更庞大的 .NET Core SDK 镜像。大多数应用只需要运行时，这可以减小你应用镜像的大小。 
* [.NET Core self-contained application Docker Production Sample](dotnetapp-selfcontained) - 这个示例适于生产场景，因为它依赖于一个操作系统镜像（没有 .NET Core 的。 [Self-contained .NET Core apps](https://docs.microsoft.com/dotnet/articles/core/deploying/) 包括作为应用一部分的 .NET Core 和基础镜像中已安装的非中心组件。
* [ASP.NET Core Docker Production Sample](aspnetapp) - 这个示例示范了一个 docker 化的 ASP.NET Core Web 应用。

### ARM32 / Raspberry Pi

* [.NET Core Docker Production Sample](dotnetapp-prod) - 这个示例包括了在树莓派 Linux 上运行一个运行时镜像的指令。
* [.NET Core self-contained application Docker Production Sample](dotnetapp-selfcontained) - 这个示例包括了在树莓派 Linux 上运行一个自包含（self-contained）镜像的指令。
* 相关的: 请访问 [.NET Core on Raspberry Pi](https://github.com/dotnet/core/blob/master/samples/RaspberryPiInstructions.md)

## 相关仓库

相关的 Docker Hub 仓库:

* [microsoft/dotnet](https://hub.docker.com/r/microsoft/dotnet/) for .NET Core images.
* [microsoft/dotnet-samples](https://hub.docker.com/r/microsoft/dotnet-samples/) for .NET Core sample images.
* [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) for ASP.NET Core images.
* [microsoft/aspnet](https://hub.docker.com/r/microsoft/aspnet/) for ASP.NET Web Forms and MVC images.
* [microsoft/dotnet-framework](https://hub.docker.com/r/microsoft/dotnet-framework/) for .NET Framework images (for web applications, see microsoft/aspnet).

相关的 GitHub 仓库:

* [dotnet/announcements](https://github.com/dotnet/announcements/issues?q=is%3Aissue+is%3Aopen+label%3ADocker) for Docker-related announcements.
* [microsoft/dotnet-framework-docker-samples](https://github.com/microsoft/dotnet-framework-docker-samples/) for .NET Framework samples.
