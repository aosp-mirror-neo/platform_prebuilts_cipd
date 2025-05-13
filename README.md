This directory contains prebuilt binaries of [CIPD](https://chromium.googlesource.com/infra/luci/luci-go/+/main/cipd/README.md) which are used by Soong.

Process for updating the prebuilts:

1. Choose a `git_revision` to update to. You can either take the revision from the [latest build](https://chrome-infra-packages.appspot.com/p/infra/tools/cipd/linux-amd64/+/latest) of CIPD or choose one from https://source.chromium.org/chromium/infra/infra_superproject . Note that changes to the `luci-go` repository are rolled into `infra` by the Skia Autoroller, and the CIPD package tags will correspond to the revision in the `infra` repo.

1. Update the `cipd_client.ensure` file in this directory with the new tag value. All of the platforms should be updated to the same `git_revision` for consistency.

1. Update `cipd_client.versions` by running
   ```
   $ cipd ensure-file-resolve -ensure-file - < cipd_client.ensure
   ```

1. Update the binaries by running
   ```
   $ cipd export -root . -ensure-file cipd_client.ensure
   ```

1. Commit the change to git. If new platforms were added, make sure to `git add` the new files.
