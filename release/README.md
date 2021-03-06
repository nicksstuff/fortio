## How to make a fortio release

- Make sure `version/version.go`'s `major`/`minor`/`patch` is newer than https://github.com/istio/fortio/releases

- Make a release there and document the changes since the previous release

- Make sure to use the same git tag format (e.g "v0.7.1" - note that there is `v` prefix in the tag, like many projects but unlike the rest of istio). Docker and internal version/tag is "0.7.1", the `v` is only for git tags.

- Make sure your git status is clean, and the tag is present before the next step or it will get marked dirty/pre

- Create the binary tgz: `make release` (from/in the toplevel directory)

- Upload the release/fortio-\*.tgz to GitHub

- The docker official builds are done automatically based on tag, check https://cloud.docker.com/app/istio/repository/docker/istio/fortio/builds

- Increment the `patch` and commit that right away so the first point is true next time and so master/latest docker images have the correct next-pre version.

## How to change the build image

Update [../Dockerfile.build](../Dockerfile.build)

Edit the `BUILD_IMAGE_TAG := v5` line in the Makefile, set it to `v6`
for instance (replace `v6` by whichever is the next one at the time)

run
```
make update-build-image
```

Make sure it gets successfully pushed to the istio/fortio registry

run
```
make update-build-image-tag
```

Check the diff and make lint, webtest, etc and PR
