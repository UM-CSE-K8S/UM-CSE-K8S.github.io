# UM-CSE-K8S.github.io
Showing progresses on the k8s priority

## Flowchart Diagram

This repository includes a Graphviz flowchart diagram that demonstrates a process flow with the following components:

- **5 sequential steps**: Initialize Process → Collect Data → Process Data → Generate Output → Save Results
- **Decision block**: "Is Data Valid?" with Yes/No branches
- **Loop mechanism**: If data is invalid, the flow loops back to the data collection step

### Files

- `flowchart.dot` - Graphviz source file
- `flowchart.png` - PNG rendering of the flowchart
- `flowchart.svg` - SVG rendering of the flowchart

### Viewing the Diagram

![Flowchart](flowchart.png)

### Rendering the Diagram

To regenerate the diagram images from the source file:

```bash
dot -Tpng flowchart.dot -o flowchart.png
dot -Tsvg flowchart.dot -o flowchart.svg
```
