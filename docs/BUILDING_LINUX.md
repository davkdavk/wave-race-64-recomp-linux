# Building on Linux (Debian 13 / Ubuntu)

```bash
sudo apt install clang cmake ninja-build binutils-mips-linux-gnu \
  python3-venv python3-dev build-essential libsdl2-dev libgtk-3-dev \
  libvulkan-dev mesa-vulkan-drivers
git clone --recurse-submodules https://github.com/davkdavk/wave-race-64-recomp.git
cd wave-race-64-recomp
git clone https://github.com/LLONSIT/Wave-Race-64.git reference/wr64-decomp
# checkout the validated revision from docs/BUILDING.md

python3 -m venv ~/wr64venv
~/wr64venv/bin/pip install PyYAML==6.0.3 pylibyaml==0.1.0 tqdm==4.67.1 \
  intervaltree==3.1.0 colorama==0.4.6 spimdisasm==1.42.4 rabbitizer==1.16.2 \
  pygfxd==1.0.5 n64img==0.3.3 crunch64==0.6.2

~/wr64venv/bin/python tools/patch_n64recomp.py
~/wr64venv/bin/python tools/patch_rsprecomp.py
~/wr64venv/bin/python tools/patch_rt64.py
~/wr64venv/bin/python tools/patch_librecomp.py
~/wr64venv/bin/python tools/patch_water.py
~/wr64venv/bin/python tools/patch_runtime_shutdown.py
cmake -S lib/N64ModernRuntime/N64Recomp -B build-tools -G Ninja \
  -DCMAKE_BUILD_TYPE=Release -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++
cmake --build build-tools --target N64RecompCLI RSPRecomp -j$(nproc)
~/wr64venv/bin/python tools/generate_game.py "Wave Race 64 (USA) (Rev A).z64"

cmake -S . -B build -G Ninja -DCMAKE_C_COMPILER=clang -DCMAKE_CXX_COMPILER=clang++ \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo -DWR64_WITH_RUNTIME=ON -DWR64_WITH_RECOMPILED=ON \
  -DWR64_WITH_FRONTEND=ON -DRT64_SDL_WINDOW_VULKAN=ON \
  -DCMAKE_CXX_FLAGS="-DPLUME_SDL_VULKAN_ENABLED -DRT64_SDL_WINDOW_VULKAN -I/usr/include/SDL2" \
  -DCMAKE_C_FLAGS="-DPLUME_SDL_VULKAN_ENABLED -DRT64_SDL_WINDOW_VULKAN -I/usr/include/SDL2"
cmake --build build -j$(nproc)
./build/WaveRace64Recomp --identify "Wave Race 64 (USA) (Rev A).z64"
./build/WaveRace64Recomp "Wave Race 64 (USA) (Rev A).z64"
```

The `SDL_WINDOW_VULKAN` flag in `src/callbacks.cpp` is required on Linux,
otherwise `SDL_Vulkan_CreateSurface` fails and the game segfaults.
