# Mesa Git Automated Builds

This repo hosts automated builds of the latest Mesa from `main` branch.

## 🔧 How it works

- Builds daily at 6 AM UTC or on manual trigger
- Targets `radeonsi`, `zink`, `softpipe`, and `llvmpipe` Gallium drivers
- Vulkan support: `amd`
- Builds are uploaded as `.zip` files to the [Releases](../../releases)

## 📥 Usage

1. Download the latest `mesa-<commit>.zip` from [Releases](../../releases)
2. Extract it:
   ```bash
   unzip mesa-*.zip -d mesa-git
   cd mesa-git
   ```
3. Use it:

```bash
export LD_LIBRARY_PATH=$PWD/lib64:$LD_LIBRARY_PATH
export LIBGL_DRIVERS_PATH=$PWD/lib64/dri
export VK_ICD_FILENAMES=$PWD/share/vulkan/icd.d/radeon_icd.x86_64.json
```

### Example Commands

```bash
# Test OpenGL:
LD_LIBRARY_PATH=$PWD/lib64:$LD_LIBRARY_PATH LIBGL_DRIVERS_PATH=$PWD/lib64/dri glxinfo | grep 'OpenGL version'

# Test Vulkan:
LD_LIBRARY_PATH=$PWD/lib64:$LD_LIBRARY_PATH VK_ICD_FILENAMES=$PWD/share/vulkan/icd.d/radeon_icd.x86_64.json vulkaninfo | head -20

# Run an application with custom Mesa:
LD_LIBRARY_PATH=$PWD/lib64:$LD_LIBRARY_PATH LIBGL_DRIVERS_PATH=$PWD/lib64/dri VK_ICD_FILENAMES=$PWD/share/vulkan/icd.d/radeon_icd.x86_64.json your-application

# For Steam games (add this to game's launch options):
LD_LIBRARY_PATH=$PWD/lib64:$LD_LIBRARY_PATH LIBGL_DRIVERS_PATH=$PWD/lib64/dri VK_ICD_FILENAMES=$PWD/share/vulkan/icd.d/radeon_icd.x86_64.json %command%
```
