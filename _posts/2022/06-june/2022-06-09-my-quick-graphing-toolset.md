---
title: "My Quick Graphing Toolset"
categories: ["graphing", "management", "software_engineering"]
---

To quickly create graphs and charts, I use a tool called Mermaid on website: <https://mermaid.live/>

It can be directly used in markdown files like:

```mermaid!
  graph TD;
      A-->B;
      A-->C;
      B-->D;
      C-->D;
```

```mermaid!
pie title Pets adopted by volunteers
  "Dogs" : 386
  "Cats" : 85
  "Rats" : 35
```

Sources: 
 * <https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/>