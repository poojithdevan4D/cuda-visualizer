# CUDA Visualizer

An interactive, beginner-friendly tool for understanding how a GPU runs code under CUDA. It visualizes the execution hierarchy (grid, block, warp, thread), shows why memory access patterns matter, and lets you explore SM occupancy. Built as a single HTML file, no build step, no backend.

**Live demo:**https://poojithdevan4d.github.io/cuda-visualizer

## What it covers

- **Structure** — a 3D explorer for the CUDA hierarchy. Set grid and block dimensions, then drill from the grid into a block, into a warp, down to individual lanes. Includes an animated "play execution" view that shows SIMT lockstep and warp divergence.
- **Memory** — visualizes how a warp's 32 threads touch global memory, and how coalesced vs strided vs misaligned access changes the number of memory transactions.
- **Occupancy** — an SM occupancy calculator across several GPU architectures (Ampere, Ada, Turing, Hopper). Shows which resource (warps, registers, shared memory, or the block cap) is limiting how many blocks fit per SM.
- **Practice** — a quiz mode that tests the concepts: warps per block, total threads, wasted lanes, which warp a thread belongs to, and more, with scoring and streaks.
- **Guided tour** — a step-by-step walkthrough for complete beginners, using a plain-language army analogy.

## Features

- Guided tour for newcomers
- Animated camera transitions and SIMT execution playback
- Shareable URLs (the current configuration is encoded in the link)
- One-click preset scenarios
- PNG export of the 3D view
- Works on any modern browser, fully client-side

## Running it

Just open `index.html` in a browser. The only external dependency is Three.js, loaded from a CDN.

To host it (all free):

- **GitHub Pages:** push this repo, enable Pages in repo settings, point it at the root. Done.
- **Vercel / Netlify:** drag the folder in, or connect the repo. No build command needed.

## Accuracy notes

This is a teaching tool, so some details are simplified for clarity:

- The memory view uses a 128-byte cache-line model. Real hardware also has 32-byte sectors and L2 cache effects. The coalescing intuition the tool teaches is correct, but exact transaction counts on real hardware can differ.
- The occupancy presets use approximate architectural limits and simplify register allocation granularity. For real kernel tuning, use NVIDIA's official Occupancy Calculator and Nsight Compute.

## How this was built

The first working version of this tool was generated with the help of an AI assistant, then reviewed and iterated on. If you fork or extend it, that's the spirit, build on it and make it your own. Contributions and corrections welcome.

## License

MIT. See [LICENSE](LICENSE).
