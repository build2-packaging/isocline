# build2 Package for `isocline`

[`isocline`](https://github.com/daanx/isocline) is a pure C library that can be used as an alternative to the GNU readline library.

[![Official](https://img.shields.io/website/https/github.com/daanx/isocline.svg?down_message=offline&label=Official&style=for-the-badge&up_color=blue&up_message=online)](https://github.com/daanx/isocline)
[![build2](https://img.shields.io/website/https/github.com/build2-packaging/isocline.svg?down_message=offline&label=build2&style=for-the-badge&up_color=blue&up_message=online)](https://github.com/build2-packaging/isocline)
[![cppget.org](https://img.shields.io/website/https/cppget.org/libisocline.svg?down_message=offline&label=cppget.org&style=for-the-badge&up_color=blue&up_message=online)](https://cppget.org/libisocline)
[![queue.cppget.org](https://img.shields.io/website/https/queue.cppget.org/libisocline.svg?down_message=empty&down_color=blue&label=queue.cppget.org&style=for-the-badge&up_color=orange&up_message=running)](https://queue.cppget.org/libisocline)

## Usage

First, add the stable section of the `cppget.org` repository to your project's `repositories.manifest` to be able to fetch this package.

```
:
role: prerequisite
location: https://pkg.cppget.org/1/stable
# trust: ...
```

If the stable section of `cppget.org` is not an option then add this Git repository itself instead as a prerequisite.

```
:
role: prerequisite
location: https://github.com/build2-packaging/isocline.git
```

Add the respective dependency in your project's `manifest` file to make the package available for import.

```
depends: libisocline ^1.0.9
```

The static library can then be imported by the following declaration in a `buildfile`. Please note that the `libisocline` package only exports the static library as the shared build is not supported by the upstream repository.

```
import isocline = libisocline%liba{isocline}
```

## Configuration

There are no configuration options available.

## Issues and Notes

- Warnings are generated due to unused private functions in the library.
- Shared library builds are not supported by the upstream repository. Even the use of automatic DLL symbol export does not seem to solve that issue.

## Contributing

Thanks in advance for your help and contribution to keep this package up-to-date.
For now, please, file an issue on [GitHub](https://github.com/build2-packaging/isocline/issues) for everything that is not described below.

### Recommend Updating Version

Please, file an issue on [GitHub](https://github.com/build2-packaging/isocline/issues) with the new recommended version.

### Update Version by Pull Request

1. Fork the repository on [GitHub](https://github.com/build2-packaging/isocline) and clone it to your local machine.
2. Run `git submodule init` and `git submodule update` to get the current upstream directory.
3. Inside the `upstream` directory, checkout the new library version `X.Y.Z` by calling `git checkout vX.Y.Z` that you want to be packaged.
4. If needed, change source files, `buildfiles`, and symbolic links accordingly to create a working build2 package. Make sure not to directly depend on the upstream directory inside the build system but use symbolic links instead.
5. Update library version in `manifest` file if it has changed or add package update by using `+n` for the `n`-th update.
6. Make an appropriate commit message by using imperative mood and a capital letter at the start and push the new commit to the `master` branch.
7. Run `bdep ci` and test for errors.
8. If everything works fine, make a pull request on GitHub and write down the `bdep ci` link to your CI tests.
9. After a successful pull request, we will run the appropriate commands to publish a new package version.

### Update Version Directly if You Have Permissions

1. Inside the `upstream` directory, checkout the new library version `X.Y.Z` by calling `git checkout vX.Y.Z` that you want to be packaged.
2. If needed, change source files, `buildfiles`, and symbolic links accordingly to create a working build2 package. Make sure not to directly depend on the upstream directory inside the build system but use symbolic links instead.
3. Update library version in `manifest` file if it has changed or add package update by using `+n` for the `n`-th update.
4. Make an appropriate commit message by using imperative mood and a capital letter at the start and push the new commit to the `master` branch.
5. Run `bdep ci` and test for errors and warnings.
6. When successful, run `bdep release --tag --push` to push new tag version to repository.
7. Run `bdep publish` to publish the package to [cppget.org](https://cppget.org).
