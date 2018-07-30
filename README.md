# OBS-studio WebRTC - Fixed Mac CI Scripts

See the latest commit for CI script changes.

### Compilation, Installation and Packaging

 - [`install-dependencies-osx.sh`](./CI/install-dependencies-osx.sh) installs dependencies
 - [`before-script-osx.sh`](./CI/before-script-osx.sh) creates a build dir and runs cmake
 - [`before-deploy-osx.sh`](./CI/before-deploy-osx.sh)
   - calls [`build_app.py`](./CI/install/osx/build_app.py) which fixes all lib paths
   - packages app into a .pkg
   - signs the app with developer certificate if available

```bash
mkdir obs-and-dependencies
cd obs-and-dependencies
git clone --recursive https://github.com/ruddell/OBS-studio-webrtc.git
cd OBS-studio-webrtc
git checkout mac-build

# only run this the once to install dependencies
./CI/install-dependencies-osx.sh

# run this to rebuild the package, read the scripts to see what they do
./CI/before-script-osx.sh
cd build && make -j 8 && cd ..
./CI/before-deploy-osx.sh
open nightly
```