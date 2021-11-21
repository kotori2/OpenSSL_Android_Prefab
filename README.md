# ndkports

A fork of [Google's ndkPorts](https://android.googlesource.com/platform/tools/ndkports/) 
building **static** builds of Android common ndk tools.
Currently only OpenSSL is supported.

## Ports

Each third-party project is called a "port". Ports consist of a description of
where to fetch the source, apply any patches needed, build, install, and package
the library into an AAR.

A port is a subclass of the abstract Kotlin class `com.android.ndkports.Port`.
Projects define the name and version of the port, the URL to fetch source from,
a list of modules (libraries) to build, and the build steps.

See the [Port class] for documentation on the port API.

Individual port files are kept in `ports/$name/port.kts`. For example, the cURL
port is [ports/curl/port.kts](ports/curl/port.kts).

[Port class]: src/main/kotlin/com/android/ndkports/Port.kt

## Building a Port

ndkports requires an NDK to be used for building to be specified on the command
line as well as a list of packages to build. For example, to build cURL:

```bash
$ ./gradlew :openssl publish -PndkPath=/path/to/ndk
```

Note that dependencies currently need to be already built or ordered explicitly.

To build all ports using Docker, use `scripts/build.sh`.
