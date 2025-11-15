# Publishing AlgoLens C++ Tracers to GitHub

## ✅ Rebranding Complete!

All files have been rebranded from `algorithm-visualizer` to `algolens`:
- ✅ Header file: `algorithm-visualizer.h` → `algolens.h`
- ✅ Include directory: `include/algorithm-visualizer/` → `include/algolens/`
- ✅ All header guards: `ALGORITHM_VISUALIZER_*` → `ALGOLENS_*`
- ✅ CMakeLists.txt: Project name updated to `algolens`
- ✅ README.md: Fully rebranded with AlgoLens branding
- ✅ Test files: Updated to use `#include "algolens.h"`

## 📤 Publishing Steps

### 1. Push to GitHub

```bash
cd tracers.cpp

# Remove old git remote (if exists)
git remote remove origin

# Add new remote
git remote add origin https://github.com/suheerasameen/tracers.cpp.git

# Stage all changes
git add -A

# Commit
git commit -m "Rebrand to AlgoLens

- Renamed algorithm-visualizer.h to algolens.h
- Updated all include paths to algolens/
- Updated header guards to ALGOLENS_*
- Updated CMakeLists.txt project name
- Updated README with AlgoLens branding
- Updated test files to use new header"

# Push to GitHub
git push -u origin master
```

### 2. Create a Release on GitHub

1. Go to: https://github.com/suheerasameen/tracers.cpp
2. Click "Releases" → "Create a new release"
3. Fill in:
   - **Tag version:** `v1.0.0`
   - **Release title:** `AlgoLens C++ Tracers v1.0.0`
   - **Description:**
     ```
     # AlgoLens C++ Tracers v1.0.0
     
     First release of AlgoLens C++ visualization library.
     
     ## Features
     - Array1DTracer - 1D array visualization
     - Array2DTracer - 2D array/matrix visualization
     - ChartTracer - Chart visualization
     - GraphTracer - Graph/tree visualization
     - LogTracer - Console output
     
     ## Installation
     ```bash
     curl -L https://github.com/suheerasameen/tracers.cpp/archive/v1.0.0.tar.gz -o algolens.tar.gz
     tar xvzf algolens.tar.gz
     cd tracers.cpp-1.0.0
     mkdir build && cd build
     cmake ..
     make install
     ```
     
     ## Usage
     ```cpp
     #include "algolens.h"
     
     int main() {
         Array1DTracer tracer("Array");
         // Your code here
         return 0;
     }
     ```
     
     Based on algorithm-visualizer/tracers.cpp, rebranded for AlgoLens.
     ```
4. Click "Publish release"

### 3. Update Your AlgoLens Server

After publishing the release, update your server's Dockerfile:

**File:** `server-master/src/tracers/cpp/Dockerfile`

```dockerfile
FROM rikorose/gcc-cmake

ARG tag_name=v1.0.0

RUN curl --create-dirs -o /usr/local/include/nlohmann/json.hpp -L "https://github.com/nlohmann/json/releases/download/v3.6.1/json.hpp" \
 && curl --create-dirs -o /usr/tmp/algolens.tar.gz -L "https://github.com/suheerasameen/tracers.cpp/archive/${tag_name}.tar.gz" \
 && cd /usr/tmp \
 && mkdir algolens \
 && tar xvzf algolens.tar.gz -C algolens --strip-components=1 \
 && cd /usr/tmp/algolens \
 && mkdir build \
 && cd build \
 && cmake .. \
 && make install

CMD g++ Main.cpp -o Main -O2 -std=c++11 -lcurl \
 && ./Main
```

### 4. Update Algorithm Files

Update all C++ algorithm files to use the new header:

```cpp
// Old:
#include "algorithm-visualizer.h"

// New:
#include "algolens.h"
```

### 5. Update Skeleton Files

Update C++ skeleton template to use new header.

## 🧪 Testing

Before deploying, test the build locally:

```bash
cd tracers.cpp
mkdir build
cd build
cmake ..
make
sudo make install

# Test the installation
cd ../test
mkdir build
cd build
cmake ..
make
./test_main
```

## 📝 Next Steps

1. ✅ Push code to GitHub
2. ✅ Create v1.0.0 release
3. ✅ Update server Dockerfile
4. ✅ Update algorithm files
5. ✅ Test build
6. ✅ Deploy to production

## 🔗 Repository URL

https://github.com/suheerasameen/tracers.cpp

## 📚 Documentation

After publishing, users can install with:

```bash
# Download and install
curl -L https://github.com/suheerasameen/tracers.cpp/archive/v1.0.0.tar.gz -o algolens.tar.gz
tar xvzf algolens.tar.gz
cd tracers.cpp-1.0.0
mkdir build && cd build
cmake ..
make install
```

And use in their code:

```cpp
#include "algolens.h"

int main() {
    Array1DTracer tracer("My Array");
    LogTracer logger("Console");
    
    int arr[] = {5, 2, 8, 1, 9};
    tracer.set(arr);
    Layout::setRoot(VerticalLayout({tracer, logger}));
    
    logger.println("Algorithm starting...");
    Tracer::delay();
    
    return 0;
}
```
