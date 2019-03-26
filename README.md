# Snapcraft remote part for go
[![Snap Status](https://build.snapcraft.io/badge/anonymouse64/go-snapcraft-part.svg)](https://build.snapcraft.io/user/anonymouse64/go-snapcraft-part)

A remote snapcraft part to build the go tools

Add "after: [go]" to your part written in go. This will use the latest go from the master branch to compile your program.

If you want to specify a specific version of go, also add a go part with the version as the `source-tag` spec. For example, to use go version `1.11.6`, use:

```yaml
    parts:
    my-go-program:
        ...
        after: [go]
    go:
        source-tag: go1.11.6
```

Note that for a number of use cases, this remote part has been superceded by the introduction of base snaps and support for `build-snap` in snapcraft 3.X. In snapcraft 3.X, for a part that uses go to build something, you can use:

```yaml
    parts:
    my-go-program:
        ...
        build-snaps: [go]
```

and the latest release of go will be used to build your snap. This is faster and more efficient than building the entire go toolchain from scratch as the remote part in this repo does. However, `build-snap` will not work if you need to run snapcraft inside a docker container or otherwise cannot run/use snaps while building a snap with snapcraft (such as running on GitLab CI, etc). In such situations, you can use this remote part to build with different versions of go in your snap. 

Also note that if you define a base snap in your snap such as with `base: core18` keyword, then you can no longer use remote parts, and will need to either use `build-snap` as shown above, or copy the go part definition here into your snapcraft.yaml as a part directly. 
