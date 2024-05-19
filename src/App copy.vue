<script>
import { createApp, onBeforeMount, ref } from "vue";
import { AgGridVue } from "ag-grid-vue3";
import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-quartz.css";
import incomes from "./data.json";
import "ag-grid-charts-enterprise";

export default {
  components: {
    "ag-grid-vue": AgGridVue,
  },
  setup(props) {
    const columnDefs = ref([
      {
      headerName: "Athlete Details",
        children: [
          {
            field: "athlete",
            width: 150,
            suppressSizeToFit: true,
            enableRowGroup: true,
            rowGroupIndex: 0,
          },
          {
            field: "age",
            width: 90,
            minWidth: 75,
            maxWidth: 100,
            enableRowGroup: true,
          },
          { field: "country", enableRowGroup: true },
          { field: "year", width: 90, enableRowGroup: true, pivotIndex: 0 },
          { field: "sport", width: 110, enableRowGroup: true },
          {
            field: "gold",
            enableValue: true,
            suppressHeaderMenuButton: true,
            filter: "agNumberColumnFilter",
            aggFunc: "sum",
          },
          {
            field: "silver",
            enableValue: true,
            suppressHeaderMenuButton: true,
            filter: "agNumberColumnFilter",
            aggFunc: "sum",
          },
          {
            field: "bronze",
            enableValue: true,
            suppressHeaderMenuButton: true,
            filter: "agNumberColumnFilter",
            aggFunc: "sum",
          },
          {
            field: "total",
            enableValue: true,
            suppressHeaderMenuButton: true,
            filter: "agNumberColumnFilter",
            aggFunc: "sum",
          },
        ],
      }
    ]);

    console.log("user data--------->", incomes);
    const gridApi = ref();

    const defaultColDef = ref({
      editable: true,
      enableRowGroup: true,
      enablePivot: true,
      enableValue: true,
      filter: true,
      flex: 1,
      minWidth: 100,
    });

    const autoGroupColumnDef = ref(null);
    const rowSelection = ref(null);
    const rowGroupPanelShow = ref(null);
    const pivotPanelShow = ref(null);
    const rowData = ref(null);

    onBeforeMount(() => {});

    const onGridReady = (params) => {
      gridApi.value = params.api;
      const updateData = (data) => (rowData.value = incomes);
      // const updateData = (data) => (rowData.value = data);
      fetch("https://www.ag-grid.com/example-assets/olympic-winners.json")
        .then((resp) => resp.json())
        .then((data) => updateData(data));
    };

    return {
      columnDefs,
      gridApi,
      autoGroupColumnDef,
      defaultColDef,
      rowSelection,
      rowGroupPanelShow,
      pivotPanelShow,
      rowData,
      onGridReady,
      themeClass: "ag-theme-quartz-dark",
    };
  },
};
</script>
<template>
  <header>
    <img
      alt="Vue logo"
      class="logo"
      src="./assets/logo.svg"
      width="125"
      height="125"
    />
  </header>

  <main style="width: 800px; height: 500px">
    <div style="height: 100%">
      <ag-grid-vue
        style="width: 100%; height: 100%"
        :class="themeClass"
        :columnDefs="columnDefs"
        @grid-ready="onGridReady"
        :autoGroupColumnDef="autoGroupColumnDef"
        :defaultColDef="defaultColDef"
        :suppressRowClickSelection="true"
        :groupSelectsChildren="true"
        :rowSelection="rowSelection"
        :rowGroupPanelShow="rowGroupPanelShow"
        :pivotPanelShow="pivotPanelShow"
        :pagination="true"
        :rowData="rowData"
      ></ag-grid-vue>
    </div>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
