<template>
  <table>
    <tbody>
      <tr>
        <td
          :colspan="datasource.children && datasource.children.length ? datasource.children.length*2 : null"
        >
          <div
            class="node"
            :id="datasource.id"
            @click.stop="handleClick({$event, nodeData: datasource})"
          >
            <slot :node-data="datasource">
              <div class="title">{{ datasource[nodeTitle] }}</div>
              <div v-if="nodeContent" class="content">{{ datasource[nodeContent] }}</div>
            </slot>
          </div>
        </td>
      </tr>
      <template v-if="datasource.children && datasource.children.length">
        <tr class="lines">
          <td :colspan="datasource.children.length*2">
            <div class="downLine"></div>
          </td>
        </tr>
        <tr class="lines">
          <td class="rightLine"></td>
          <template v-for="n in (datasource.children.length-1)">
            <td class="leftLine topLine"></td>
            <td class="rightLine topLine"></td>
          </template>
          <td class="leftLine"></td>
        </tr>
        <tr class="nodes">
          <td colspan="2" v-for="child in datasource.children" :key="child.id">
            <node :datasource="child" :handle-click="handleClick" :nodeContent="nodeContent">
              <template v-for="slot in Object.keys($scopedSlots)" :slot="slot" slot-scope="scope">
                <slot :name="slot" v-bind="scope" />
              </template>
            </node>
          </td>
        </tr>
      </template>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "node",
  props: {
    datasource: Object,
    handleClick: Function,

    nodeTitle: {
      type: String,
      default: "name"
    },

    nodeContent: {
      type: String,
      default: ""
    }
  },
  methods: {}
};
</script>

<style>
</style>
