<template>
  <div>
    <vue-treeselect
      ref="treeselect"
      :multiple="true"
      :options="[treeData]"
      noResultsText="No results..."
      placeholder="Select items..."
      v-model="selected"
      :default-expand-level="0"
      :autoSelectDescendants="true"
      :autoDeselectDescendants="true"
      :flat="false"
      :searchable="false"
      :show-count="true"
    >
    </vue-treeselect>
    <div>Selected: {{ selected }}</div>
  </div>
</template>
<script>
import { defineComponent, ref, reactive, onMounted } from "vue";

export default defineComponent({
  setup() {
    const treeselect = ref();
    let selected = ref([]);
    let treeOrientation = ref("0");
    let treeData = reactive({
      label: "root",
      expand: true,
      id: "1",
      children: [
        { label: "child 1", id: "2" },
        { label: "child 2", id: "3" },
        {
          label: "subparent 1",
          id: 4,
          expand: false,
          children: [
            { label: "subchild 1", id: 5 },
            {
              label: "subchild 2",
              id: 6,
              expand: false,
              children: [
                { label: "subchild 11", id: 7 },
                { label: "subchild 22", id: 8 },
              ],
            },
          ],
        },
      ],
    });

    onMounted(() => {
      if (treeselect.value) {
        console.log("treeselect exists");
        treeselect.value.selectNodes(["2"]);
      }

      setTimeout(() => {
        treeselect.value.selectNodes(["2", "3", 5, 8]);
      }, 5000);
    });

    return {
      treeData,
      selected,
      treeselect,
    };
  },
});
</script>
