# Graph ordering algorithm

Basic graph ordering implementation of Tarjan algorithm.

```typescript

import { GraphOrderingAlgorithm } from "./index.js"

type NodeData = {
   name: string
   edges?: string[]
}

const graph: { [key: string]: NodeData } = {
   "n1": {
      name: "node 1",
      edges: []
   },
   "n2": {
      name: "node 2",
      edges: ["n5"]
   },
   "n3": {
      name: "node 3",
      edges: ["n2"]
   },
   "n4": {
      name: "node 4",
      edges: ["n5"]
   },
   "n5": {
      name: "node 5",
      edges: ["n3"]
   },
}

const algo = new GraphOrderingAlgorithm<NodeData>((node, visitor) => {
   if (node.edges) {
      for (const key of node.edges) {
         visitor(graph[key])
      }
   }
})
for (const key in graph) {
   algo.addNode(graph[key])
}
algo.process()

for (const comp of algo.components) {
   console.log(`group: ${comp.groupId}`);
   for (let node = comp.connecteds; node; node = node.connected) {
      console.log(`     + ${node.data.name}`);
   }
}

```