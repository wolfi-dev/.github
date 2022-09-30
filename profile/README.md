![wolfi logo](https://github.com/wolfi-dev/.github/raw/main/profile/wolfi-logo-dark-mode.svg#gh-dark-mode-only)
![wolfi logo](https://github.com/wolfi-dev/.github/raw/main/profile/wolfi-logo-light-mode.svg#gh-light-mode-only)

# Wolfi OS

Wolfi is a community Linux OS designed for the container and cloud-native era. Chainguard started the Wolfi project to enable building  [Chainguard Images](/chainguard/chainguard-images/overview), our collection of curated [distroless]( https://blog.chainguard.dev/minimal-container-images-towards-a-more-secure-future/) images that meet the requirements of a secure software supply chain. This required a Linux distribution with components at the appropriate granularity and with support for both [glibc](https://www.gnu.org/software/libc/) and [musl](https://www.musl-libc.org/), something that was not yet available in the cloud-native Linux ecosystem.

Wolfi is a stripped-down distro designed for the cloud-native era. It doesn't have a kernel of its own, instead relying on the environment (such as the container runtime) to provide one. This separation of concerns in Wolfi means it is adaptable to a range of environments.

# Wolfi Features

Wolfi, whose name was inspired by the [world's smallest octopus](https://en.wikipedia.org/wiki/Octopus_wolfi), has some key features that differentiates it from other distributions that focus on container/cloud-native environments:

- Provides a high-quality, build-time SBOM as standard for all packages
- Packages are designed to be granular and independent, to support minimal images
- Uses the proven and reliable apk package format
- Fully declarative and reproducible build system
- Designed to support glibc and musl 

# Where's the Source?

* [bootstrap-stage1](https://github.com/wolfi-dev/bootstrap-stage1) contains the stage1 bootstrap repository which is used with Alpine.
* [bootstrap-stage2](https://github.com/wolfi-dev/bootstrap-stage2) contains the stage2 bootstrap repository which is used with Alpine and the stage1 toolchain to bootstrap stage3.
* [bootstrap-stage3](https://github.com/wolfi-dev/bootstrap-stage3) contains the stage3 bootstrap repository which is a micro GNU/Linux distribution built with stage2 and used to bootstrap Wolfi.
* [os](https://github.com/wolfi-dev/os) contains the core Wolfi OS repository.

# FAQ

## What is Wolfi and how does it compare to Alpine?
Wolfi is a Linux _undistro_  designed from the ground up to support newer computing paradigms such as containers. Although Wolfi has a few similar design principles as Alpine (such as using apk), it is a different distribution that is  focused on supply chain security. Unlike Alpine, Wolfi does not currently build its own Linux kernel, instead relying on the host environment (e.g. a container runtime) to provide one.

## Is Wolfi free to use?
Yes, Wolfi is free and will always be.

## Can I use Wolfi on the Desktop?
No. Wolfi is an un-distro, or distroless base to be used within the container / OCI ecosystem. Desktop distributions require additional software that is out of scope for Wolfi's roadmap.

## Who maintains Wolfi?
Wolfi was created and is currently maintained by [Chainguard](https://chainguard.dev).

## What are the plans for long-term Wolfi governance?
We intend for Wolfi to be a community-driven project, which means over time it will have multi-vendor governance and maintainers. For now we're focused on building the project and community, and will revisit this in several months when a community has formed.

## Where can I get security feeds for Wolfi?
See [SECURITY.md](/SECURITY.md) for information about reporting security incidents concerning and consuming security data about Wolfi.
