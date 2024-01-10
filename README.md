# Actions-OpenWrt

A template for making custom OpenWrt builds using GitHub Actions.

Based on "[P3TERX's Actions-OpenWrt](https://github.com/P3TERX/Actions-OpenWrt)".

## Default build info

- Using OpenWrt build source: [OpenWrt official build source](https://git.openwrt.org/openwrt/openwrt.git).
- OpenWrt version: openwrt-23.05 (SNAPSHOT).

## Usage

- To create a new repository using this template, click "[Use this template](https://github.com/jellybean13/Actions-OpenWrt/generate)" button.
- Change environment variables such as "`REPO_URL`" and "`REPO_BRANCH`" if you want.
- Create empty directories named "`overlay`" and "`patches`" if required.
- Add custom "`overlay`" and "`patches`" and push them to the GitHub repository.
- Go to "`Actions > Build OpenWrt`", select your branch, and click "`Run workflow`" button.
- Wait until the building process is complete.
- When the build is complete, go to "`Releases`" or "`Actions > Build OpenWrt`" to download your custom OpenWrt firmware.
- If neither relevant artifacts are in GitHub releases nor in "`Actions > Build OpenWrt`", which means the building process completed with errors, view logs in "`Actions > Build OpenWrt`".

## Environment variables list

> **Tip:** All environment variables can be found in [here](.github/workflows/build-openwrt.yml).

- Editable environment variables:

```yaml
  # Remote repository of OpenWrt.
  # Default: https://git.openwrt.org/openwrt/openwrt.git
  REPO_URL: https://git.openwrt.org/openwrt/openwrt.git
  # Branch/Tag of the remote repository.
  # Default: openwrt-23.05
  REPO_BRANCH: openwrt-23.05
  # The timezone of the building environment.
  # Default: Asia/Shanghai
  BUILDING_ENV_TIMEZONE: Asia/Shanghai
  # Upload OpenWrt firmware artifact.
  # Default: true
  UPLOAD_FIRMWARE_ARTIFACT: true
  # Upload OpenWrt packages (ipk) artifact.
  # Default: true
  UPLOAD_PACKAGES_ARTIFACT: true
  # Whether to upload custom firmware to CowTransfer.
  # Default: false
  UPLOAD_TO_COWTRANSFER: false
  # Whether to upload custom firmware to WeTransfer.
  # Default: false
  UPLOAD_TO_WETRANSFER: false
  # Whether to upload custom firmware to GitHub releases.
  # Default: true
  UPLOAD_TO_GITHUB_RELEASES: true
  # The number of maximum item that Workflow runs and GitHub releases preserve.
  # Default: 3
  MAXIMUM_NUMBER_OF_PRESERVED_ITEMS: 3
```

- Non-editable environment variables (if certain requirements not met):

```yaml
  # A file containing custom feeds.
  # DO NOT MODIFY unless the target file has been moved, renamed or removed.
  FEEDS_CONF_FILE: feeds.conf.default
  # A directory containing "apply custom overlay" feature.
  # DO NOT MODIFY unless the target directory has been moved, renamed or removed.
  OVERLAY_DIR: overlay
  # A directory containing "apply custom patches" feature.
  # DO NOT MODIFY unless the target directory has been moved, renamed or removed.
  PATCHES_DIR: patches
```

## Important notices

- You need to grant read and write permissions to workflow in "`Repository settings > Actions > General > Workflow permissions`".
- "`overlay/feeds.conf.default`" will override "`feeds.conf.default`" before updating feeds. And other files will override target files after feeds update. So, you can add modified feeds to "`overlay/feeds.conf.default`".
- Patches in "`patches`" directory will patch OpenWrt source code after feeds update. Note that the path that is in the header of the patch file is based on the root location of OpenWrt source code.
- Refreshing feeds may complete with errors if your patches alter packages in "`feeds`" directory, which is caused by merge conflict sometimes. If it happens, you need to reanalyze upstream codes, rebase revelant patches and try again.
- DO NOT using patches in "`patches`" directory to alter feeds, which takes no effect owing to the execution sequence of relevant scripts.
