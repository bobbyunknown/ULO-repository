# ULO Repository

Central data repository for ULO Firmware Builder.

## Structure

This repository uses **two branches**:

### `main` Branch
Contains GitHub Actions workflows for data synchronization.

### `data` Branch
Contains all firmware building data:

```
data/
├── kernels/           # Extracted kernel files
│   ├── 5.4.279/
│   ├── 6.1.66-DBAI/
│   └── ...
├── rootfs/
│   ├── base/         # Base rootfs from ULO-repository
│   └── custom/       # Custom rootfs from releases
├── firmware/         # Driver firmware files
├── devices/          # Device configurations
└── loader/           # Bootloader files
    ├── amlogic/
    ├── allwinner/
    └── rockchip/
```

## Auto-Sync

The `sync-data.yml` workflow automatically syncs data from:

- **Kernels**: `armarchindo/kernel` releases (tag: `kernel_dbai`)
- **Base Rootfs**: `armarchindo/ULO-repository/rootfs`
- **Custom Rootfs**: `armarchindo/rootfs-openwrt` releases
- **Firmware**: `armarchindo/ULO-repository/firmware`
- **Devices**: `armarchindo/ULO-Builder/device`
- **Loaders**: `armarchindo/ULO-Builder/core/loader`

## Triggers

- **Daily**: Runs at 00:00 UTC
- **Manual**: Via workflow dispatch
- **On Push**: When main branch is updated

## Usage

ULO-Builder fetches data from the `data` branch:

```yaml
repositories:
  ulo_data:
    type: github
    url: https://github.com/armarchindo/ULO-repository
    branch: data
```

## License

MIT License
