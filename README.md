# AlgoLens C++ Tracers [![GitHub release](https://img.shields.io/github/release/suheerasameen/tracers.cpp.svg?style=flat-square)](https://github.com/suheerasameen/tracers.cpp/releases/latest)

> Part of the [AlgoLens](https://algo.waqasishaque.me) project - Algorithm Visualization Platform

`tracers.cpp` is a visualization library for C++ that powers AlgoLens.
You can use it on [algo.waqasishaque.me](https://algo.waqasishaque.me) or locally on your machine.

## Prerequisites

- [libcurl](https://curl.haxx.se/libcurl/)

## Installation

1. Download and extract the source code in the [latest release](https://github.com/suheerasameen/tracers.cpp/releases/latest).

2. Change directory to it and run:

```bash
mkdir build
cd build
cmake ..
make install
```

## Usage

```cpp
// import visualization libraries {
#include "algolens.h"
// }

#include <vector>
#include <string>

// define tracer variables {
Array2DTracer array2dTracer = Array2DTracer("Grid");
LogTracer logTracer = LogTracer("Console");
// }

// define input variables
std::vector<std::string> messages{
        "Visualize",
        "your",
        "own",
        "code",
        "here!",
};

// highlight each line of messages recursively
void highlight(int line) {
    if (line >= messages.size()) return;
    std::string message = messages[line];
    // visualize {
    logTracer.println(message);
    array2dTracer.selectRow(line, 0, message.size() - 1);
    Tracer::delay();
    array2dTracer.deselectRow(line, 0, message.size() - 1);
    // }
    highlight(line + 1);
}

int main() {
    // visualize {
    Layout::setRoot(VerticalLayout({array2dTracer, logTracer}));
    array2dTracer.set(messages);
    Tracer::delay();
    // }
    highlight(0);
    return 0;
}
```

## Available Tracers

- **Array1DTracer** - Visualize 1D arrays
- **Array2DTracer** - Visualize 2D arrays and matrices
- **ChartTracer** - Visualize charts and plots
- **GraphTracer** - Visualize graphs and trees
- **LogTracer** - Console output for debugging

## Building from Source

```bash
git clone https://github.com/suheerasameen/tracers.cpp.git
cd tracers.cpp
mkdir build
cd build
cmake ..
make
sudo make install
```

## Links

- [AlgoLens Platform](https://algo.waqasishaque.me)
- [Documentation](https://algo.waqasishaque.me/docs)
- [Report Issues](https://github.com/suheerasameen/tracers.cpp/issues)
