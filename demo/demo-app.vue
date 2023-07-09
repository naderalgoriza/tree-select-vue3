<template>
  <div>
    <vue-treeselect
      ref="treeselect"
      :multiple="true"
      :options="treeData"
      noResultsText="No results..."
      placeholder="Select items..."
      v-model="selected"
      :default-expand-level="0"
      :autoSelectDescendants="true"
      :autoDeselectDescendants="true"
      :flat="false"
      :searchable="true"
      :show-count="true"
      :normalizer="normalizer"
      :enableSelectionFromCheckboxOnly="true"
      valueConsistsOf="LEAF_PRIORITY"
    >
    </vue-treeselect>
    <div>Selected: {{ selected }}</div>
  </div>
</template>
<script>
import { defineComponent, ref, reactive, onMounted } from "vue";
import { industriesOptions } from "./options";

export default defineComponent({
  setup() {
    const treeselect = ref();
    let selected = ref([]);
    let treeOrientation = ref("0");

    const normalizer = (option) => {
      const newOption = {
        ...option,
        label: option.nameAr,
      };
      if (option.children?.length === 0) {
        delete newOption.children;
      }
      return newOption;
    };

    return {
      treeData: industriesOptions,
      selected,
      treeselect,
      normalizer,
    };
  },
});
</script>
