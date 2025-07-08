# Mesa Git Automated Builds

This repo hosts automated builds of the latest Mesa from `main` branch with bundled LLVM libraries for maximum portability.

## Features

- **Daily builds** at 6 AM UTC or on manual trigger
- **Complete driver support**: `radeonsi`, `zink`, `softpipe`, and `llvmpipe` Gallium drivers
- **Vulkan support**: AMD drivers with bundled LLVM 20.1
- **Vulkan Translation Layers ready**: Includes all necessary LLVM libraries
- **Portable**: No system LLVM installation required
- Builds are uploaded as `.zip` files to the [Releases](../../releases)

## Usage

### Simple Usage (Recommended)

1. Download the latest `mesa-git.zip` from [Releases](../../releases)
2. Extract it:
   ```bash
   unzip mesa-git.zip
   cd mesa-git
   ```
3. **Use the wrapper script for any application**:
   ```bash
   ./mesa-git your-application
   ```
   The `mesa-git` script automatically handles all environment setup, including bundled LLVM libraries.

### Manual Setup (Advanced)

If you prefer to set environment variables manually:

```bash
export LD_LIBRARY_PATH=$PWD/lib64/bundled:$PWD/lib64:$LD_LIBRARY_PATH
export LIBGL_DRIVERS_PATH=$PWD/lib64/dri
export VK_ICD_FILENAMES=$PWD/share/vulkan/icd.d/radeon_icd.x86_64.json
```

## Release Zip Structure

After extracting `mesa-git.zip`, you'll find the following structure:

```
mesa-git/
├── build-info.txt      # Commit hash and build date
├── mesa-git            # All-in-one wrapper script with LLVM support
├── include/            # Mesa headers (EGL, GBM, GL)
├── lib64/              # Libraries and drivers
│   ├── bundled/        # Bundled LLVM 20.1 libraries
│   ├── dri/            # Gallium drivers (radeonsi, zink, etc.)
│   ├── gbm/            # GBM driver
│   ├── pkgconfig/      # .pc files for development
│   └── vdpau/          # VDPAU libraries for video acceleration
└── share/
    ├── drirc.d/        # Default driver configs
    ├── glvnd/          # GLVND vendor config
    └── vulkan/
        └── icd.d/      # Vulkan ICD JSON

```

### Key Files

- **`mesa-git` script**: All-in-one wrapper that automatically configures environment and loads bundled LLVM libraries
- **`lib64/bundled/`**: Contains LLVM 20.1 libraries required for Vulkan Translation Layers and advanced features
- **`build-info.txt`**: Shows the Mesa commit and build date for reference

### Example: Using with Steam

**Set the Steam game launch option to:**
```
/path/to/mesa-git/mesa-git %command%
```

For example, if you extracted to your home directory:
```
~/mesa-git/mesa-git %command%
```

### Example: Vulkan Translation Layers

The bundled LLVM libraries make this build perfect for Vulkan Translation Layers:

```bash
cd mesa-git
# Run any application with full LLVM support
./mesa-git your-vulkan-application
# Works with VKD3D-Proton, DXVK, or other translation layers
```

The `mesa-git` wrapper automatically handles all library paths and LLVM dependencies.

## Troubleshooting

### LLVM Library Issues

If you encounter errors like `libLLVM.so.20.1: cannot open shared object file`, this build includes bundled LLVM libraries and the `mesa-git` wrapper automatically handles them:

1. **Always use the wrapper**: `./mesa-git your-application`
2. **Check library loading**: `./mesa-git ldd lib64/libvulkan_radeon.so` should show LLVM libraries resolved
3. **Manual verification**: The wrapper sets `LD_LIBRARY_PATH` to include `lib64/bundled` first

### Why Bundle LLVM?

- **Portability**: Works on systems without LLVM 20.1 installed
- **Vulkan Translation Layers**: Required for VKD3D-Proton, DXVK, and similar tools
- **Consistency**: Ensures the exact LLVM version Mesa was built against

## System Requirements

- **Architecture**: x86_64 Linux
- **No specific LLVM version required** (bundled)
- **Kernel**: Recent Linux kernel with DRM support
- **Hardware**: AMD GPUs for Vulkan support (Intel/NVIDIA for OpenGL only)
