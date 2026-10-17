# Sofle Firmware Workspace

## Repository Roles

- This repository (`zmk-sofle`) owns the Sofle shield, keymap, and firmware build configuration.
- `config/west.yml` is the source of truth for the integration workspace. It pins `zmk` to `https://github.com/MicheleYin/zmk.git` at `feature/nice-view` and `zmk-module-nice-view-svg` to `https://github.com/MicheleYin/zmk-module-nice-view-svg` at `feature/nice-view`.
- The `zmk` dependency is a custom fork. Do not replace it with `zmkfirmware/zmk`, `main`, or another upstream revision unless explicitly requested. Features and APIs used by this firmware may exist only in the custom fork.
- `zmk-module-nice-view-svg` supplies the Nice!view Plus module. Its Zephyr module name is `zmk-nice-view-plus`.
- `zmk-studio` is a separate application repository; it is not the ZMK firmware or module dependency.

## Workspace Setup and Builds

For a fresh firmware workspace, initialize West from this repository's local manifest and update its pinned projects:

```sh
west init -l config
west update
west zephyr-export
```

Use `build.yaml` as the source of truth for the Sofle firmware targets, shields, artifacts, and CMake options. For changes to the Nice!view Plus module or its ZMK integration, build/test with this Sofle manifest so the custom ZMK fork and the intended module revision are used. The module's standalone tests may use different dependencies.

When changing a dependency revision, update `config/west.yml` deliberately and verify the resulting `west list`; do not silently switch the firmware to upstream ZMK.
