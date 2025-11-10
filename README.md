# Starlet Noise Sandbox

A C++ playground for experimenting with noise algorithms.

## Features
- Simple **2D Perlin Noise** implementation
- **ASCII Console** visualization of noise output
- Adjustable resolution and scale

## Building the Project
This project uses **CMake**. Follow these steps to build:

### 1. Clone the Repository
```bash
git clone https://github.com/masonlet/starlet-noise-sandbox.git
cd starlet-noise-sandbox
```

### 2. Create a Build Directory and Generate Build Files
```bash
mkdir build
cd build
cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=ON ..
```
`-DCMAKE_EXPORT_COMPILE_COMMANDS=ON` flag generates a `compile_commands.json` file
Can be safely omitted on Windows if you're using Visual Studio

### 3. Build the Project
- **Linux**:
  ```bash
  make
  ```

- **Windows**:
  ```bash
  cmake --build .
  ```
  Or open the generated `.sln` file in Visual Studio and build the solution.
