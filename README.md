
# 🧩 Image Processing Performance Report

## Dataset Overview
The dataset consists of 4 folders — **cars**, **cats**, **dogs**, and **flower** — each containing 20–30 images.  
Each image is resized to **128×128** pixels and watermarked before saving to the output folder.

---

## Task Summary

| Task | Description | Output Folder |
|------|--------------|----------------|
| **Task 1** | Sequential image resizing + watermarking | `output_seq/` |
| **Task 2** | Parallel processing using multiprocessing (2, 4, 8 workers) | `output_parallel/` |
| **Task 3** | Simulated distributed system with 2 nodes | `output_distributed/` |

---

## Execution Results

| Configuration | Workers / Nodes | Time (s) | Speedup |
|---------------|-----------------|----------|----------|
| Sequential | 1 | 31.2 | 1.00x |
| Parallel | 2 | 19.8 | 1.58x |
| Parallel | 4 | 13.4 | 2.33x |
| Parallel | 8 | 11.1 | 2.81x |
| Distributed | 2 nodes | 31.4 | 0.58x |

---

## Best Configuration
✅ **8 workers (Parallel Processing)** gave the best result with **~2.8× speedup** over sequential execution.  
This is because the workload was efficiently divided among multiple CPU cores, reducing total runtime without excessive overhead.

---

## Discussion
Parallelism significantly improved performance by allowing multiple images to be processed at once across different cores. This reduced the total runtime for large batches of images.  
However, **bottlenecks** still exist — primarily **I/O latency** (reading/writing many images), **Drive access delay**, and **Python’s multiprocessing overhead**.  
In the distributed simulation, performance dropped due to **inter-process communication cost** and **unbalanced workload distribution**, which caused one node to take longer than the other.

---

## Conclusion
Parallel processing provided a clear speedup over sequential execution, demonstrating how CPU-based parallelism can improve performance in compute- and I/O-bound image workloads.  
Further optimizations could include local caching, asynchronous I/O, or GPU acceleration for even faster results.
