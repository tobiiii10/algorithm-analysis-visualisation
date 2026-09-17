# algorithm-analysis-visualisation
Classical sorting and graph algorithms implemented from scratch in Python, then benchmarked against input size to compare their measured runtime with their theoretical complexity.

Built as a second-year project at Loughborough University (May – Jun 2025).

What it covers

Sorting

Merge sort — O(n log n), stable, predictable
Quicksort — O(n log n) average, O(n²) worst case

Graph traversal and shortest paths

Breadth-first search — O(V + E)
Dijkstra's algorithm — shortest paths on a weighted graph

Every algorithm is implemented from first principles. Nothing is imported from a library.

Built with
Python — all implementations
Jupyter Notebook — benchmarking harness and plots
Running it

Open the notebook and run the cells in order:

bash
jupyter notebook

Benchmarks generate inputs across a range of sizes, time each algorithm over repeated runs, and plot the results.

What the benchmarks showed

The headline finding is the gap between asymptotic notation and observed behaviour at small input sizes.

Constant factors dominate until n gets large. Merge sort and quicksort are both O(n log n) on average, but their measured curves separate clearly at small n because of differing overhead — merge sort's allocation of temporary arrays costs real time that the notation discards. The asymptotic classes only converge once n is large enough for the log-linear term to swamp everything else.

This is the thing worth taking away: complexity analysis tells you how an algorithm scales, not which one is faster on your actual data. For small inputs, the constant factor is the whole story.

Quicksort's worst case is a real risk, not a theoretical one. On already-sorted input with naive pivot selection, the O(n²) behaviour appears immediately and unmistakably in the timings.

Findings are written up in a technical report comparing theoretical predictions against the empirical curves.

What I'd do differently

Timings are wall-clock over repeated runs, which picks up interpreter and garbage-collection noise. Instruction counting, or a profiler, would isolate algorithmic cost more cleanly.

The Dijkstra implementation uses a simple priority queue. Comparing a binary heap against a Fibonacci heap would show the difference between O((V + E) log V) and O(E + V log V) in practice — which, given the finding above, might well turn out to be nothing at these input sizes.
