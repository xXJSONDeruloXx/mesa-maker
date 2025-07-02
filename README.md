# Mesa Git Automated Builds

This repo hosts automated builds of the latest Mesa from `main` branch.

## 🔧 How it works

- Builds daily at 6 AM UTC or on manual trigger
- Targets `radeonsi`, `zink`, and `llvmpipe` Gallium drivers
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
glxinfo | grep OpenGL
```
