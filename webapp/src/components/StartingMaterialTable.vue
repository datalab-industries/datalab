<template>
  <DynamicDataTable
    :columns="startingMaterialColumn"
    :data="startingMaterials"
    :data-type="'startingMaterials'"
    :global-filter-fields="['item_id', 'name', 'chemform', 'chemical_purity', 'nblocks']"
  />
</template>

<script>
import DynamicDataTable from "@/components/DynamicDataTable";
import { getStartingMaterialList } from "@/server_fetch_utils.js";

export default {
  components: { DynamicDataTable },
  data() {
    return {
      startingMaterialColumn: [
        { field: "item_id", header: "ID", body: "FormattedItemName", filter: true, label: "ID" },
        { field: "name", header: "Name", label: "Name" },
        { field: "chemform", header: "Formula", body: "ChemicalFormula", label: "Formula" },
        { field: "date", header: "Date", label: "Date" },
        { field: "chemical_purity", header: "Purity", label: "Purity" },
        {
          field: "blocks",
          header: "",
          body: "BlocksIconCounter",
          icon: ["fa", "cubes"],
          label: "Block",
        },
        {
          field: "nfiles",
          header: "",
          body: "FilesIconCounter",
          icon: ["fa", "file"],
          label: "Files",
        },
      ],
    };
  },
  computed: {
    startingMaterials() {
      return this.$store.state.starting_material_list;
    },
  },
  mounted() {
    this.getStartingMaterials();
  },
  methods: {
    getStartingMaterials() {
      getStartingMaterialList();
    },
  },
};
</script>
