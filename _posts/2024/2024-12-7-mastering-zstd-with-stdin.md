---
title: "Mastering zstd: Stdin Compression Tricks"
categories: ["devops", "linux"]
---

Zstandard (zstd) offers powerful compression directly from stdin, making file handling a breeze. Whether you're archiving logs or transferring data, piping content is simple. For compression, just pipe your data: `cat file.txt | zstd > compressed.zst`. Decompression is equally straightforward: `zstd -d < compressed.zst > restored.txt`. Pro tip: Use compression levels with `-#` to balance speed and size. Command-line enthusiasts will love how zstd seamlessly integrates with shell pipelines, providing efficient, flexible compression on the fly. Experiment with different levels to find your sweet spot!
