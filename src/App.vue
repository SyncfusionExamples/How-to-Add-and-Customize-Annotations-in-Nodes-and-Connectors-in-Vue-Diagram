<template>
  <ejs-diagram ref="diagramObject" :width="width" :height="height" 
  :nodes="nodes" :connectors="connectors"
  :getNodeDefaults="getNodeDefaults"></ejs-diagram>
</template>
<script>

let diagramInstance;

let nodes = [
  {
    id: "startNode",
    offsetX: 440,
    offsetY: 60,
    shape: { type: "Flow", shape: "Terminator" },
    annotations: [{ content: 'Start'}]
  },
  {
    id: "inputNode",
    offsetX: 440,
    offsetY: 180,
    shape: { type: "Flow", shape: "Data" },
    annotations: [{ content: 'Enter a number',
    //offset: { x:0, y:0 },
    //verticalAlignment: 'Top',
    //horizontalAlignment: 'Left',
    style: { textWrapping: 'Wrap', fontFamily: 'TimesNewRoman', fontSize: 14 },
    //width: 45,
    constraints: AnnotationConstraints.ReadOnly,
    hyperlink:{
      content: 'My Hyperlink',
      link: 'https://syncfusion.com',
      hyperlinkOpenState: 'CurrentTab'
    }
  }]
  },
  {
    id: "decisionNode",
    offsetX: 440,
    offsetY: 300,
    shape: { type: "Flow", shape: "Decision" },
    annotations: [{ content: 'N divisible by 2 ?' }]
  },
  {
    id: "processEvenNode",
    offsetX: 700,
    offsetY: 300,
    shape: { type: "Flow", shape: "Process" },
    //annotations: [{ content: 'N is Even' }]
  },
  {
    id: "processOddNode",
    offsetX: 440,
    offsetY: 420,
    shape: { type: "Flow", shape: "Process" },
    annotations: [{ content: 'N is Odd' }]
  },
  {
    id: "endNode",
    offsetX: 440,
    offsetY: 540,
    shape: { type: "Flow", shape: "Terminator" },
    annotations: [{ content: 'End' }]
  }
];

let connectors = [
  {
    id: 'startToInputConnector',
    sourceID: 'startNode',
    targetID: 'inputNode'
  },
  {
    id: 'inputToDecisionConnector',
    sourceID: 'inputNode',
    targetID: 'decisionNode'
  },
  {
    id: 'decisionToProcessEvenConnector',
    sourceID: 'decisionNode',
    targetID: 'processEvenNode',
    annotations: [{ content: 'true', style: {fill: 'white'},
    //offset:0,
    alignment: 'Before',
    displacement: {x:5, y:5}}]
  },
  {
    id: 'decisionToProcessOddConnector',
    sourceID: 'decisionNode',
    targetID: 'processOddNode',
    annotations: [{ content: 'false', style: {fill: 'white'},
    alignment: 'After',
    displacement: {x:5, y:5}}]
  },
  {
    id: 'processOddToEndConnector',
    sourceID: 'processOddNode',
    targetID: 'endNode'
  },
  {
    id: 'processEvenToEndConnector',
    sourceID: 'processEvenNode',
    targetID: 'endNode',
    type: "Orthogonal",
    segments: [ { type: "Orthogonal", direction: "Bottom", length: 200 } ]
  }
];

import {
  DiagramComponent, AnnotationConstraints
} from '@syncfusion/ej2-vue-diagrams';

export default {
  components: {
    'ejs-diagram': DiagramComponent
  },
  data: function () {
    return {
      width: '1102px',
      height: '602px',
      nodes: nodes,
      connectors: connectors,
      getNodeDefaults: (node) => {
        node.height = 60;
        node.width = 150;
      }
    };
  },
  mounted: function(){
    diagramInstance = this.$refs.diagramObject.ej2Instances;
    diagramInstance.addLabels(diagramInstance.nodes[3], [{ content: 'N is Even'}]);
    //diagramInstance.addLabels(diagramInstance.connectors[3], [{ content: 'false', style: { fill: 'white'}}]);

    //diagramInstance.nodes[3].annotations[0].content = 'Updated Node Annotation';
    //diagramInstance.connectors[3].annotations[0].content = 'Updated Connector Annotation';
  }
};
</script>
<style>
@import "../node_modules/@syncfusion/ej2-vue-diagrams/styles/material.css";
</style>