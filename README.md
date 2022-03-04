# Docker

Contains Docker images for all Covas projects.
All images are hosted on [GitHub Container Registry](https://github.com/orgs/sios-technology-inc/packages).

## How it works

This repository automatically publishes Docker Image to GitHub Container Registry,
and enable developers or CI/CD pipelines to pull the images with the following format:

    ghcr.io/sios-technology-inc/covas-docker-{NAME}:{VERSION}

    # Example: `deploy` image with version `1.2.3`
    docker pull ghcr.io/sios-technology-inc/covas-docker-deploy:1.2.3

    # Example: `nodejs` image with version `alpine-123`
    docker pull ghcr.io/sios-technology-inc/covas-docker-nodejs:alpine-123

## Important Security Notices

GitHub Container Registry enables package owners to choose [visibility of images](https://docs.github.com/en/packages/learn-github-packages/configuring-a-packages-access-control-and-visibility), either `public` or `private`.

- `public`: image will be **PUBLICLY AVAILABLE** via `docker pull`
- `private`: priviledged organization members only, requires `docker login` before calling `docker pull`

In any case, always follow the [best practices](https://sysdig.com/blog/dockerfile-best-practices/) found on the web,
and NEVER include credentials!

## Image types

There are 2 types of images in this repository.

### Generic images

When the image is to be used with multiple services, it is considered as generic image.
The generic image should contain minimal dependencies that are used across services.

Examples:

- [go](./go)
- [node](./node)
- [mysql](./mysql)

### Service specific images

When the image is used by specific service, it is considered as service specific image.
It is recommended to include all OS-level dependencies, so that developers does not need to build it locally.

Examples:

- [deploy](./deploy)
- [schema](./schema)

## Creating new image

Follow these steps to create a new image.

### 1. Prepare directory and GitHub Actions

You must name the image with the following conventions:

- Lowercase letters
- Dash (hyphen)

Take `foo` as an example, create directory to contain Dockerfile and its dependencies.

    mkdir foo
    touch foo/CHANGELOG.md
    touch foo/Dockerfile

Also create a GitHub Actions file.

    touch .github/workflows/publish.foo.yml

### 2. Create Pull Request

After the `foo` image is ready, make a Pull Request for review.

When you merge the Pull Request to `develop` branch, it will trigger GitHub Actions to push to GitHub Container Registry with the following hostname and paths.

    ghcr.io/sios-technology-inc/covas-docker-foo:latest

### 3. Release

Release process is very simple, just update CHANGELOG.md of the target image directory with the appropriate version.

> Your CHANGELOG.md must follow [keepachangelog 1.0.0](https://keepachangelog.com/en/1.0.0/) format.

Let's say you have the following CHANGELOG.md:

    # CHANGELOG

    ## [Unreleased]

    ### Added

    - Something cool

    ## [0.1.0] - 2020-10-01

    ...

When making a release, add a new h2 heading with newly created version.

You can choose to adopt [Semantic Versioning](https://semver.org) (e.g. `## [1.2.3]`),
or any lowercase string (e.g. `## [alpine-1.2.3]`).

    # CHANGELOG

    ## [Unreleased]

    ## [0.2.0] - 2020-10-12

    ...

    ### Added

    - Something cool

    ## [0.1.0] - 2020-10-07

    ...

Then push the change to `develop` branch. That's all!

Wait few minutes for [Actions](https://github.com/sios-technology-inc/covas-docker-image/actions) to push to container registry.

### 4. Make the image publicly available (Optional)

The image is in private mode by default, and only administrator could change the configuration to make it public.

> See [Configuring visibility of container images for an organization](https://docs.github.com/en/packages/learn-github-packages/configuring-a-packages-access-control-and-visibility#configuring-visibility-of-container-images-for-an-organization) to control image visibility.

Finally, you can pull your image.

    docker pull ghcr.io/sios-technology-inc/covas-docker-foo:0.1.0
