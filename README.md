# C++ STL Professional Reference

A structured and practical repository for learning and revising the C++ Standard Template Library (STL).

## Repository Structure

- `docs/STL_GUIDE.md` — Comprehensive STL guide with explanations and examples.
- `CONTRIBUTING.md` — Contribution workflow and quality expectations.
- `.gitignore` — Standard ignore rules for C++ and common editor/tool artifacts.
- `LICENSE` — MIT license.

## Quick Start

1. Clone the repository.
2. Open `docs/STL_GUIDE.md` and navigate to the container/topic you want.
3. Copy any code snippet into a `.cpp` file and compile with a modern compiler:

```bash
g++ -std=c++17 -O2 -Wall -Wextra -pedantic example.cpp -o example
./example
```

## Coverage

The guide includes:

- Sequence containers (`array`, `vector`, `deque`, `list`, `forward_list`)
- Associative containers (`set`, `multiset`, `map`, `multimap`)
- Unordered associative containers (`unordered_set`, `unordered_map`, etc.)
- Container adapters (`stack`, `queue`, `priority_queue`)
- Utility types (`pair`)

## Why this structure?

This layout separates:

- **Repository metadata** (`README`, `LICENSE`, contribution rules)
- **Learning content** (`docs/`)

That makes the project easier to maintain, browse, and extend with future examples/tests.

## Contributing

Please read [CONTRIBUTING.md](CONTRIBUTING.md) before submitting changes.
