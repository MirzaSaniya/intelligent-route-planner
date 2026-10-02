# Intelligent Route Planner

A classical AI search system that finds low-cost routes through a weighted graph using **Uniform Cost Search (UCS)** and **A\***.

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Tests](https://img.shields.io/badge/Tests-Pytest-green)
![Focus](https://img.shields.io/badge/AI-Search-orange)

## Why this project?

Navigation and logistics problems can be represented as a state-space search problem: the system starts at one location, chooses among available transitions, and tries to reach a goal while minimizing cost.

This project translates that idea into a compact, reusable route-planning engine. The cost can represent distance, travel time, tolls, energy, or a weighted combination of objectives.

The main question explored here is:

> **Can heuristic search find the same optimal route as uninformed search while examining fewer states?**

## What it demonstrates

- State-space formulation for route planning
- Weighted graph search
- Uniform Cost Search for optimal path finding
- A* search with a heuristic function
- Path reconstruction
- Search-efficiency benchmarking
- Unit testing for algorithmic correctness

## Architecture

```text
                 +-------------------+
                 |   Route Problem   |
                 | graph + start/end |
                 +---------+---------+
                           |
                +----------+----------+
                |                     |
                v                     v
       +----------------+     +----------------+
       | Uniform Cost   |     |      A*        |
       | Search         |     | Search         |
       +--------+-------+     +--------+-------+
                |                      |
                +----------+-----------+
                           v
                 +--------------------+
                 | Optimal Route +    |
                 | Search Statistics  |
                 +--------------------+
```

## Example use case

Consider a delivery network connecting a warehouse to a customer. Each road has a different cost. A route planner can search the network while optimizing for total route cost.

The included demo compares UCS and A* on the same network.

Run it with:

```bash
python examples/demo.py
```

Expected output format:

```text
Intelligent Route Planner
============================

Uniform Cost Search
Path: Warehouse -> ... -> Customer
Cost: ...
Expanded nodes: ...

A* Search
Path: Warehouse -> ... -> Customer
Cost: ...
Expanded nodes: ...
```

The exact numbers depend on the graph in `examples/demo.py`.

## Algorithms

### Uniform Cost Search

UCS expands the frontier node with the smallest accumulated path cost `g(n)`. With non-negative edge costs, it returns an optimal path.

### A*

A* prioritizes nodes using:

`f(n) = g(n) + h(n)`

where:

- `g(n)` is the cost accumulated so far
- `h(n)` estimates the remaining cost

For distance-based graphs, the included Euclidean heuristic is useful when the edge costs are consistent with geometric distance.

## Project structure

```text
intelligent-route-planner/
├── README.md
├── requirements.txt
├── src/
│   ├── __init__.py
│   └── route_planner.py
├── examples/
│   └── demo.py
└── tests/
    └── test_route_planner.py
```

## Running tests

Install the development dependency:

```bash
pip install -r requirements.txt
```

Run:

```bash
pytest
```

## Portfolio framing

This repository is intentionally presented as an independent AI engineering project inspired by concepts studied in Stanford CS221: Artificial Intelligence: Principles and Techniques.

The portfolio emphasis is on the **application, algorithm implementation, experimentation, testing, and documentation**, rather than reproducing course starter code or course solutions.

## Future extensions

- Add a real road-network dataset
- Support multi-objective costs such as distance + toll + time
- Add bidirectional search
- Add Greedy Best-First Search as a baseline
- Visualize frontier expansion step by step
- Add a small web UI for interactive route selection
- Benchmark runtime and node expansions across graph sizes

## License

MIT License. See `LICENSE`.
