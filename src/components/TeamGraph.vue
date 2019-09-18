<template>
  <div></div>
</template>

<script>
export default {};
</script>

<style>
</style>

<script>
import vis from "vis-network";

let network;

const nodes = new vis.DataSet([{ id: 1, label: "1", shape: "circle" }]);

// create an array with edges
const edges = new vis.DataSet([]);

const options = {
  nodes: {
    heightConstraint: {
      minimum: 100
    },
    widthConstraint: {
      minimum: 100
    },
    borderWidth: 0,
    color: {
      background: "#dddddd",
      highlight: "#70abeb"
    },
    physics: true,
    font: {
      size: 40,
      face: '"IBM Plex Serif", Helvetica, sans-serif',
      align: "center"
    },
    margin: 25
  },
  layout: {
    improvedLayout: true,
    randomSeed: 3
  },
  edges: {
    color: "#dddddd",
    width: 10,
    length: 220
  },
  interaction: {
    dragNodes: false,
    dragView: false,
    zoomView: false
  }
};

const data = {
  nodes: nodes,
  edges: edges
};

export default {
  components: {},
  props: {
    step: 0
  },
  data: function() {
    return {};
  },
  watch: {
    step: function(newStep, oldStep) {
      switch (newStep) {
        case 3:
          nodes.add([{ id: 3, label: "DS", shape: "circle" }]);
          edges.add([{ id: 2, from: 1, to: 3 }, { id: 3, from: 2, to: 3 }]);
          break;
        case 2:
          nodes.remove([{ id: 3 }]);
          edges.remove([{ id: 2 }, { id: 3 }]);
          nodes.add([{ id: 2, label: "2", shape: "circle" }]);
          edges.add([{ id: 1, from: 1, to: 2 }]);
          break;
        case 1:
          nodes.remove([{ id: 3 }, { id: 2 }]);
          edges.remove([{ id: 1 }, { id: 2 }, { id: 3 }]);
          break;
      }

      network.fit();
    }
  },
  destroyed: function() {
    network.destroy();
  },
  mounted: function() {
    this.$nextTick(() => {
      const el = this.$el;
      network = new vis.Network(el, data, options);
    });
  }
};
</script>

<style lang="scss">
@import "../variables.scss";
</style>
