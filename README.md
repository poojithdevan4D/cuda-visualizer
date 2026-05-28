# CUDA Visualizer

An interactive, beginner-friendly tool for understanding how a GPU runs code under CUDA. It visualizes the execution hierarchy (grid, block, warp, thread, lane), shows why memory access patterns matter, and lets you explore SM occupancy. Single HTML file, no build step, no backend.

**Live demo:** https://poojithdevan4d.github.io/cuda-visualizer/

## What it covers

**Structure** — a 3D explorer for the CUDA hierarchy. Set grid and block dimensions, then drill from the grid into a block, into a warp, down to individual lanes. Each warp-view cube is labelled with both its lane number (the slot, 0 to 31) and its tid (the unique thread occupying that slot). Includes an animated "play execution" view that shows SIMT lockstep and warp divergence. Hover any thread to see its full index calculation worked out (`blockIdx.x * blockDim.x + threadIdx.x = ...`) with real numbers plugged in.

**Memory** — visualizes how a warp's 32 threads touch global memory, and how the access pattern changes the number of memory transactions. Includes an animation that fires each thread into memory sequentially with a live transaction counter.

**Occupancy** — an SM occupancy calculator across several GPU architectures (Ampere, Ada, Turing, Hopper). Shows which resource (warps, registers, shared memory, or the block cap) is limiting how many blocks fit per SM.

**Practice** — a quiz mode that tests the concepts: warps per block, total threads, idle lanes, which warp a thread belongs to, total warps across the grid. Tracks score and streaks.

**Guided tour** — a step-by-step walkthrough for complete beginners using a plain-language army analogy (thread = soldier, warp = squad of 32 in lockstep, block = platoon, grid = whole army).

## Features

- Guided tour for newcomers
- Smooth animated camera transitions between grid, block, and warp views
- SIMT execution playback with divergence animation
- Sequential memory access animation with live transaction tally
- Thread index decoder (hover any thread to see its global index math)
- Glossary with plain-language definitions of every term
- Shareable URLs (the current configuration is encoded in the link)
- One-click preset scenarios (1D vector add, 2D image processing, wasted-lane example, etc.)
- PNG export of the 3D view
- Keyboard shortcuts (press `?` for the list)
- Works on any modern browser, fully client-side

## Running it

Just open `index.html` in a browser. The only external dependency is Three.js, loaded from a CDN.

To host it (all free):

- **GitHub Pages:** push to a repo, enable Pages in repo settings, point at the root. Done.
- **Vercel / Netlify:** drag the folder in, or connect the repo. No build command needed.

## Keyboard shortcuts

- `1` / `2` / `3` / `4` — switch between Structure / Memory / Occupancy / Practice
- `G` — open glossary
- `T` — start the guided tour
- `S` — copy a shareable link to the current view
- `P` — play execution (in warp view)
- `Esc` — go back to the previous view
- `?` — show this list in the app

## Accuracy notes

This is a teaching tool, so some details are simplified for clarity:

- The memory view uses a 128-byte cache-line model. Real hardware also has 32-byte sectors and L2 cache effects. The coalescing intuition is correct, but exact transaction counts on real hardware can differ.
- The occupancy presets use approximate architectural limits and simplify register allocation granularity. For real kernel tuning, use NVIDIA's official Occupancy Calculator and Nsight Compute.
- The tool will let you set block dimensions exceeding the real CUDA limit of 1024 threads per block (a real GPU would refuse to launch these), but it will warn you. This is deliberate, so you can still visualise the larger structures.

## How this was built

The first working version was generated with AI assistance, then reviewed, fixed, and iterated on. The code is MIT licensed, so if you want to extend or fork it, the spirit is: build on it and make it your own. Corrections, bug reports, and contributions all welcome.

## Contributing

If you find a bug, open an issue. If you want to add a feature (memory bank conflicts, shared memory layout, a new GPU preset, additional quiz question types), feel free to open a PR. Keep it focused, this is a teaching tool and clarity beats feature count.

## License

MIT. See [LICENSE](LICENSE).
