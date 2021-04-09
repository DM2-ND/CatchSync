# CatchSync

This repository contains the code package for the KDD'14 Best Paper Finalist / TKDD'16 paper:

**[CatchSync: Catching Synchronized Behavior in Large Directed Graphs](http://www.meng-jiang.com/pubs/catchsync-kdd14/catchsync-kdd14-paper.pdf).** 

**[Catching Synchronized Behaviors in Large Networks: A Graph Mining Approach](http://www.meng-jiang.com/pubs/catchsync-tkdd16/catchsync-tkdd16-paper.pdf).** 

[Meng Jiang](http://meng-jiang.com/), Peng Cui, Alex Beutel, Christos Faloutsos, Shiqiang Yang.

## Usage

Given a directed graph with millions of nodes, how can we automatically spot anomalies? Suspicious graph patterns show up in many applications, from Twitter users who buy fake followers, manipulating the social network, to botnet members performing distributed denial of service attacks, disturbing the network traffic graph.
 
**Input:** node pairs (edge list) of a directed graph;

**Output:**
1. Feature space plots: in-degree vs. authority for target nodes (out-degree vs. hubness for source nodes);
2. Synchronicity (coherence) vs. normality: for source nodes.

**Installation:** Python >= 2.6; R >= 3.0.1

**Data:** see ./data/socialgraph: A directed graph (sample data). Two columns {node1,node2}: node1 follows (connects to) node2. Injected users: 'badXXXX'; normal users: 'userXXXX'.

**Result:** see ./plot/*.png:
- followee_feature_space.png: A feature space created by followees' features (in-degree and authority).
- follower_synchronicity_normality.png: Synchronicity vs. Normality for followers. Followers with too high synchronicity are suspicious.

**compile:**
	Complile java code CatchSync.java => CatchSync.class

**edgelist:** [graph_to_edgelist]
- Mapping a directed graph into a edge list with nodes starting from 0,1...; and a nodemap from old id to new id
- Input: "data" (directory name), socialgraph
- Output: edgelist, nodemap

**distribution:** [edgelist_to_dc]
- Calculating data distributions: node's degrees, out-degree and in-degree distributions
- Input: "data" (directory name), edgelist, nodemap
- Output: xindoutd, outd2c, ind2c

**adjacencylist:** [edgelist_to_adjacencylist]
- Changing edge list into two adjacency lists (source node to a list of targets, target node to a list of sources)
- Input: "data" (directory name), edgelist
- Output: adjacencylist_u2vs, adjacencylist_v2us

**hitsscore:** [hits_degree_adjacency]
- Computing HITS score (U1 value = hubness, V1 value = authority) in 10 iterations
- Input: "data" (directory name), adjacencylist_u2vs, adjacencylist_v2us, nodemap, xindoutd, 10
- Output: xu1outd, xv1ind

**cellfeature:** [scatter_to_cell] or [scatter_to_cell_N]
- Mapping scatter plots into cell plots: 1. by log(a), a=2; 2. N*N, 100*100
- Input: "data" (directory name), xu1outd/xv1ind/..., "log 100"/"2"
- Output: xcu1coutdN100, cellu1outdN100

**coherence:** [normalcy_coherence]
- Computing synchronicity (coherence) and normality (normalcy).
- Input: "data" (directory name), adjacencylist_u2vs, xcv1cindP2, cellv1indP2
- Output: unorcohoutdP2

**cellcoherence:**
- Mapping scatter plots into cell plots: linear 100*100 deg>=20
- Input: "data" (directory name), unorcohoutdP2, lin 100 20
- Output: xcunorcucohD20, cellunorcohD20
	
**jetplot:**
- Plot the feature space and synchronicity-normality.
- Input: cellv1indN100/cellunorcohD20
- Output: followee_feature_space.png/follower_synchronicity_normality.png

## Citation
If you find this repository useful in your research, please cite our paper:

```bibtex
@inproceedings{jiang2014catchsync,
  title={CatchSync: catching synchronized behavior in large directed graphs},
  author={Jiang, Meng and Cui, Peng and Beutel, Alex and Faloutsos, Christos and Yang, Shiqiang},
  booktitle={Proceedings of the 20th ACM SIGKDD international conference on Knowledge discovery and data mining},
  pages={941--950},
  year={2014},
  organization={ACM}
}

@article{jiang2016catching,
  title={Catching synchronized behaviors in large networks: A graph mining approach},
  author={Jiang, Meng and Cui, Peng and Beutel, Alex and Faloutsos, Christos and Yang, Shiqiang},
  journal={ACM Transactions on Knowledge Discovery from Data (TKDD)},
  volume={10},
  number={4},
  pages={1--27},
  year={2016},
  publisher={ACM New York, NY, USA}
}
