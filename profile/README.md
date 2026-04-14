![wolfi logo](https://github.com/wolfi-dev/.github/raw/main/profile/wolfi-logo-dark-mode.svg#gh-dark-mode-only)
![wolfi logo](https://github.com/wolfi-dev/.github/raw/main/profile/wolfi-logo-light-mode.svg#gh-light-mode-only)

# Wolfi OS
Wolfi is the first community Linux (un)distribution declaratively built for creating a secure base layer for your containers! 

Wolfi is a Linux OS designed for the container and cloud-native era. Chainguard started the Wolfi project to enable building [Chainguard Containers](https://www.chainguard.dev/containers), our collection of curated [distroless](https://blog.chainguard.dev/minimal-container-images-towards-a-more-secure-future/) images that meet the requirements of a secure software supply chain. This required a Linux distribution with components at the appropriate granularity and with support for [glibc](https://www.gnu.org/software/libc/).

Wolfi is a stripped-down distro designed for the cloud-native era. It doesn't have a kernel of its own, instead relying on the environment (such as the container runtime) to provide one. This separation of concerns in Wolfi means it is adaptable to a range of environments.

## Wolfi Features

Wolfi, whose name was inspired by the [world's smallest octopus](https://en.wikipedia.org/wiki/Octopus_wolfi), has some key features that differentiates it from other distributions that focus on container/cloud-native environments:

- Provides a high-quality, build-time SBOM as standard for all packages
- Packages are designed to be granular and independent, to support minimal images
- Focuses on the latest release of all packages
- Uses the proven and reliable apk package format
- Fully declarative and reproducible build system
- Designed to support glibc

## Where's the Source?

The [os repository](https://github.com/wolfi-dev/os) contains the core Wolfi OS as a sync from internal Chainguard repositories. Any proposed improvements are applied internally, and then synced back out to the public repository.

## Wolfi Community

| Resource    | Details |
| ----------- | ----------- |
| Forum       | See [GitHub Discussions](https://github.com/orgs/wolfi-dev/discussions) |
| Slack       | Some community members can be found in the`#apko` channel on [Kubernetes Slack](https://slack.kubernetes.io), but there is no active monitoring of this channel.|
| Slack       | Some community members can be found on [Chainguard Community Slack](https://join.slack.com/t/chainguardcommunity/shared_invite/zt-3nxzg5zz7-_7r3CdZ01M17ICCuNMhwtA)|

The [community repo](https://github.com/wolfi-dev/community) contains full details of past community calls and resources.

## Get Started

To get you up and running with Wolfi, let's go over a quick demo where you can create an image from a Dockerfile.

We'll use a "Hello, World" style Python program to demonstrate:

```python
def main():
    print("Hello, Wolfi!")

if __name__ == "__main__":
    main()
```

Within the same directory, you can create the Dockerfile. This Dockerfile will set up the `WORKDIR`, and copy relevant files. It will also define the entry point that will be executed when we run this image with `docker run`. We are using the [wolfi-base image](https://github.com/chainguard-images/images/tree/main/images/wolfi-base) to build a Python image from scratch, using Wolfi apks. The final image runs using the unprivileged `nonroot` user.

```docker
FROM cgr.dev/chainguard/wolfi-base

ARG version=3.11
WORKDIR /app

RUN apk add python-${version} && chown -R nonroot:nonroot /app/

USER nonroot

COPY  hello_wolfi.py /app/
ENTRYPOINT [ "python", "hello_wolfi.py" ]
```

This Dockerfile uses a variable called `version` to define which Python version is going to be installed on the resulting image. You can change this to one of the available Python versions on the [wolfi-dev/os](https://github.com/wolfi-dev/os) repository.

From here, you can build and run your image. If you run into issues with the `build` step, try using `sudo`.

```sh
docker build . -t hellowolfi
docker run --rm hellowolfi
```

You should receive the following output: 

```
Hello, Wolfi!
```

For more guidance, you can check out a full tutorial on [Creating Wolfi Images with Dockerfiles](https://edu.chainguard.dev/open-source/wolfi/wolfi-with-dockerfiles/), or alternately use apko to build a distroless image with only the packages you need, by reviewing a [Getting Started with apko](https://edu.chainguard.dev/open-source/apko/getting-started-with-apko/) tutorial.

## FAQ

### What is Wolfi and how does it compare to Alpine?

Wolfi is a Linux _undistro_  designed from the ground up to support newer computing paradigms such as containers. Although Wolfi has a few similar design principles as Alpine (such as using apk), it is a different distribution that is  focused on supply chain security. Unlike Alpine, Wolfi does not currently build its own Linux kernel, instead relying on the host environment (e.g. a container runtime) to provide one.

### Is Wolfi free to use?

Yes, Wolfi is freely [available under the Apache License V2](https://github.com/wolfi-dev/os/blob/main/LICENSE) and will always be.

### Where are packages in Wolfi published?

Packages in Wolfi are published to [public Wolfi APK Repositories](https://edu.chainguard.dev/chainguard/chainguard-images/network-requirements/).

### What packages are included in Wolfi?

Wolfi focusses on latest package versions and provides a base minimum of packages for variety of containers. Specifically all packages used in free Chainguard Containers are available as packages.

Non-latest versions of packages in these repositories are retained for 12 months until June 8th, 2026, and then for 6 months by default.

For more information, see the [Wolfi Archive Policy announcement](https://github.com/orgs/wolfi-dev/discussions/63023), the [updated policy announcement](](https://github.com/orgs/wolfi-dev/discussions/78666)), and our [discussions forum in general](https://github.com/orgs/wolfi-dev/discussions).

Chainguard also regularly removes packages from Wolfi for reasons outside the scope of the Wolfi retention policy. Typically, this involves removing the package definition from the Wolfi GitHub repository only. 

Existing packages that have already been built remain in the Wolfi binary package repository such as `apk.cgr.dev/chainguard/x86_64` until they are removed according to the retention policy.

The most common trigger for removal is when a new version of a version streamed package is released. In this situation, package definitions for prior versions streams are removed from Wolfi. For example, when MariaDB 13 is released and added to Wolfi, MariaDB 12 is removed from Wolfi. New versions of MariaDB 12 packages are available from Chainguard only as the focus of Wolfi is on latest releases only. 

### Can I mix packages from Alpine repositories into a Wolfi-based image?

No, it’s not possible to mix Alpine apks with Wolfi apks. If your image requires dependencies that are currently only available for Alpine. You might consider using [melange](https://github.com/chainguard-dev/melange) to build a custom apk for your image.

### Can I use Wolfi on the Desktop?

No. Desktop distributions require additional software that is out of scope for Wolfi.

### Who maintains Wolfi?

Wolfi was created and is currently maintained by [Chainguard](https://chainguard.dev) as the base of Chainguard OS.

### What are the plans for long-term Wolfi governance?

We intend for Wolfi to be the core foundation of Chainguard OS and available as open source project for use with minimal packages as used in our free Chainguard Containers.

### Where can I get security feeds for Wolfi?

See [SECURITY.md](/SECURITY.md) for information about reporting security incidents concerning and consuming security data about Wolfi.

### Where can I ask questions or learn more about using Wolfi?

Find details in our [repositories](https://github.com/orgs/wolfi-dev/repositories), use our [community channels](#wolfi-community) and read our [documentation](https://edu.chainguard.dev/open-source/wolfi/overview/).
