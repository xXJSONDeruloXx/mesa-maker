# Mesa Git Automated Builds

This repo hosts automated builds of the latest Mesa from `main` branch.

## How it works

- Builds daily at 6 AM UTC or on manual trigger
- Targets `radeonsi`, `zink`, `softpipe`, and `llvmpipe` Gallium drivers
- Vulkan support: `amd`
- Builds are uploaded as `.zip` files to the [Releases](../../releases)

## Usage

1. Download the latest `mesa-git.zip` from [Releases](../../releases)
2. Extract it:
   ```bash
   unzip mesa-git.zip
   ```
3. Use it:

```bash
export LD_LIBRARY_PATH=$PWD/lib64:$LD_LIBRARY_PATH
export LIBGL_DRIVERS_PATH=$PWD/lib64/dri
export VK_ICD_FILENAMES=$PWD/share/vulkan/icd.d/radeon_icd.x86_64.json
```

## Release Zip Structure

After extracting `mesa-git.zip`, you'll find the following structure:

```
mesa-git/
├── build-info.txt      # Commit hash and build date
├── include/            # Mesa headers (EGL, GBM, GL)
├── lib64/              # Libraries and drivers
│   ├── dri/            # Gallium drivers (radeonsi, zink, etc.)
│   ├── gbm/            # GBM driver
│   ├── pkgconfig/      # .pc files for development
│   └── vdpau/          # VDPAU libraries for video acceleration
├── mesa-git            # Helper script to run commands with this Mesa build
└── share/
    ├── drirc.d/        # Default driver configs
    ├── glvnd/          # GLVND vendor config
    └── vulkan/
        └── icd.d/      # Vulkan ICD JSON

```

- **`mesa-git` script**: A helper to run any command or game with the custom Mesa environment. It sets up all necessary environment variables automatically.
- **`build-info.txt`**: Shows the Mesa commit and build date for reference.

### Example: Using with Steam

If you extract to your home directory, you can force a Steam game to use this Mesa build by setting the launch option:

```
~/mesa-git/mesa-git %command%
```

This ensures the game runs with the libraries and drivers from the extracted Mesa build, overriding the system defaults.
