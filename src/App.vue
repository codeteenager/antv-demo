<template>
  <button @click="save">保存</button>
  <div id="mountNode" class="mount-node"></div>
</template>

<script>
import G6 from '@antv/g6';

export default {
  name: 'App',
  data(){
    return {
      graph: null
    }
  },
  mounted() {
    const data = {
      // 点集
      nodes: [
        {
          id: 'node1', // String，该节点存在则必须，节点的唯一标识
          x: 100, // Number，可选，节点位置的 x 值
          y: 200, // Number，可选，节点位置的 y 值
        },
        {
          id: 'node2', // String，该节点存在则必须，节点的唯一标识
          x: 300, // Number，可选，节点位置的 x 值
          y: 200, // Number，可选，节点位置的 y 值
        },
      ],
      // 边集
      edges: [
        {
          source: 'node1', // String，必须，起始点 id
          target: 'node2', // String，必须，目标点 id
        },
      ],
    };
    this.graph = new G6.Graph({
      container: 'mountNode', // String | HTMLElement，必须，在 Step 1 中创建的容器 id 或容器本身
      width: 800, // Number，必须，图的宽度
      height: 500, // Number，必须，图的高度
      defaultNode: {
        type: 'rect',
        size: [100, 50]
      },
      defaultEdge: {
        type: 'polyline',
        color: 'red',
        label: '边边'
      },
      modes: {
        default: ['drag-canvas', 'zoom-canvas', 'drag-node'],
        edit: ['click-select']
      }
    });
    this.graph.data(data); // 读取 Step 2 中的数据源到图上
    this.graph.render(); // 渲染图
  },
  methods:{
    save(){
      console.log('========保存');
      console.log(this.graph);
      const data = this.graph.save();
      console.log('=============data');
      console.log(data);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.mount-node {
  background-color: darkcyan;
}
</style>
