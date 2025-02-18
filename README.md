# ScaleWeaver: A High-Fidelity Artificial Network of Networks (NoN) Generator

## Setup and Installation:

### Prerequisites

Ensure your system meets the following requirements:

1. Python >=2.7, 3.2 or above
2. NetworkX library (version >= 1.10)
3. NumPy library (version >= 1.5)

### Verification:

To verify your installation, run Python and execute the following commands:

```python
import sys, numpy, networkx
print(sys.version)
print(numpy.__version__)
print(networkx.__version__)
```

### Optional Dependency:

For visualization purposes, it is recommended to install Graphviz.

Citations:
[1] https://realpython.com/generative-adversarial-networks/
[2] https://www.vde.com/en/fnn/topics/european-network-codes/rfg
[3] https://www.v7labs.com/blog/neural-network-architectures-guide
[4] https://goemc.com/wp-content/uploads/2020/10/NEC-Requirements-for-Generators.pdf
[5] https://neptune.ai/blog/6-gan-architectures
[6] https://www.acer.europa.eu/electricity/connection-codes/requirements-for-generators
[7] https://openaccess.thecvf.com/content_CVPR_2019/papers/Karras_A_Style-Based_Generator_Architecture_for_Generative_Adversarial_Networks_CVPR_2019_paper.pdf
[8] https://www.entsoe.eu/network_codes/rfg/

## Usage Example:

```python
python musketeer.py -f data-samples/arenas_email.edges -t edgelist -p "{'node_growth_rate':[0.005, 0.001], 'edge_edit_rate':[0.05, 0.04, 0.03], 'node_edit_rate':[0.07, 0.06, 0.05]}" -o output/test.dot
```

1. Loads data
2. Increases nodes: 0.9% (level 1), 0.1% (level 0)
3. Edits: 3% edges, 5% nodes (level 2); 4% edges, 6% nodes (level 1); 5% edges, 7% nodes (level 0)
4. Outputs to test.dot

Direct Python call:
```python
import algorithms
new_G = algorithms.generate_graph(G, params)
```

## Key Parameters:

- `node_growth_rate`, `edge_growth_rate`: Values in (-1,infinity)
- `algorithm`: Alternative generators (e.g., `alternatives.expected_degree_replicate`)
- `accept_chance_edges`: Controls long-distance edge insertion (0.0-1.0)
- `deferential_detachment_factor`: Modifies edge deletion probability (default: 1)
- `locality_bias_correction`: Adjusts triangle generation (-1 to 1)
- `new_edge_horizon`: Depth of scanning for new edges (positive integer)
- `preserve_clustering_on_deletion`: Enhances clustering fidelity (boolean)

## Advanced Options:

- `algorithm:algorithms.musketeer_snapshots`: Sequential editing with snapshots
- `algorithm:algorithms.musketeer_iterated_cycles`: Alternating editing cycles
- `algorithm:algorithms.musketeer_on_subgraphs`: Apply to each component separately
- `post_processor`: Custom function for final processing

Troubleshooting:
---------------
Accelerating the computation
* remove the computation of the metrics with "-M False" argument (all metrics);  or in graphutils.py, make some complex metrics optional.
* convert the original graph into a simple format like edgelist
* reduce the new_edge_horizon (reduces fidelity)
* set deferential_detachment_factor close to 0 (reduces fidelity)
* give the authors funding to develop a version in the C language

Clustering is diminished in the replicas
* make sure that the pattern is consistent - there would be and need to be some variance
* reduce the edge editing rate at the finest level: it would improve preservation of all fine-level properties of the graph
* increase locality_bias_correction
* make fine_clustering True
* make preserve_clustering_on_deletion True

Path lengths and related global metrics are diminished in the replicas
* make accept_chance_edges closer to 0.  As a compensation to maintain fidelity, increase new_edge_horizon to 10, 20 or larger.

Support for weighted edges
* currently only used in coarsening
* I am planning to include it in future releases

Support for node and edge attributes
* use the parameters 'maintain_node_attributes':True, 'maintain_edge_attributes':True

Error writing DOT file or pygraphviz error:
* pygraphviz is not currently functional in the Windows platform
* specify an alternative output file such as "-o my_output.elist"
* or, try install/ing pydot package


## Conclusion:

Thank you for your interest in ScaleWeaver. I hope this tool proves valuable in your network analysis and generation tasks.

### Key Features:

- High-fidelity replication of complex network structures
- Multiscale approach for preserving properties across different granularities
- Customizable parameters for fine-tuning network generation
- Support for various input and output formats

### Future Development:

I am committed to continually improving ScaleWeaver. Planned enhancements include:

1. Full support for weighted edges
2. Improved performance optimizations
3. Extended documentation and use case examples
4. Integration with additional network analysis tools

### Community Contributions:

I welcome contributions from the community. If you encounter issues, have feature requests, or wish to contribute code, please visit our GitHub repository.


### Final Notes:

ScaleWeaver is provided as Open-Source, I strive for accuracy and reliability.

I appreciate your feedback and hope ScaleWeaver enhances your network analysis capabilities. Enjoy exploring the intricate world of complex networks with ScaleWeaver!
