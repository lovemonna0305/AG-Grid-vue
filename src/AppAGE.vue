<script>
import { createApp, onBeforeMount, ref } from "vue";
import { AgGridVue } from "ag-grid-vue3";
import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-quartz.css";
import incomes from "./dataAGE.json";
import "ag-grid-charts-enterprise";
import CustomHeader from "./CustomHeader.vue";

export default {
  components: {
    "ag-grid-vue": AgGridVue,
  },
  setup(props) {
    const gridApi = ref();

    const defaultColDef = ref({
      editable: true,
      filter: true,
      flex: 1,
      minWidth: 60,
      wrapHeaderText: true,
    });

    const dates = ref([
      "4/26",
      "4/27",
      "4/28",
      "4/29",
      "4/30",
      "5/1",
      "5/2",
      "5/3",
      "5/4",
      "5/5",
      "5/6",
      "5/7",
      "5/8",
      "5/9",
      "5/10",
      "5/11",
      "5/12",
      "5/13",
      "5/14",
      "5/15",
      "5/16",
      "5/17",
      "5/18",
      "5/19",
      "5/20",
      "5/21",
      "5/22",
      "5/23",
      "5/24",
      "5/25",
      "5/26",
      "5/27",
      "5/28",
      "5/29",
      "5/30",
    ]);
    const totalSum = ref(0);
    const rowSelection = ref(null);

    const autoGroupColumnDef = ref(null);
    const rowGroupPanelShow = ref(null);
    const pivotPanelShow = ref(null);
    const rowData = ref(null);
    const aggFuncs = ref(null);
    const rowClassRules = ref(null);

    const columnDefs = ref([
      {
        field: "organization",
        wrapText: true,
        autoHeight: true,
        rowGroup: true,
        hide: true,
        pinned: "left",
        lockPinned: true,
        wrapHeaderText: true,
        editable:'false',
      },
      {
        field: "team",
        wrapText: true,
        autoHeight: true,
        rowGroup: true,
        hide: true,
        pinned: "left",
        lockPinned: true,
        wrapHeaderText: true,
        editable:'false',
      },

      {
        headerName: "Details",
        children: [
          {
            field: "plan",
            wrapText: true,
            autoHeight: true,
            pinned: "left",
            aggFunc: "sum",
            lockPinned: true,
            wrapHeaderText: true,
            width: 100,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: "Plan" },
            cellClass: "rag-blue" 
          },
          {
            field: "earning",
            wrapText: true,
            autoHeight: true,
            pinned: "left",
            aggFunc: "sum",
            lockPinned: true,
            wrapHeaderText: true,
            width: 100,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: "Earning" },
            type: "totalColumn",
            valueGetter:
              " getValue('1day') + getValue('2day') + getValue('3day') + getValue('4day')+ getValue('5day')+ getValue('6day')+ getValue('6day')+ getValue('8day')+ getValue('9day')+ getValue('10day')+ getValue('11day')+ getValue('12day')+ getValue('13day')+ getValue('14day')+ getValue('15day')+ getValue('16day')+ getValue('17day')+ getValue('18day')+ getValue('19day')+ getValue('20day')+ getValue('21day')+ getValue('22day')+ getValue('23day')+ getValue('24day')+ getValue('25day')+ getValue('26day')+ getValue('27day')+ getValue('28day')+ getValue('29day')+ getValue('30day')+ getValue('31day')",
            editable:'false',
          },
        ],
      },
      {
        headerName: "Daily Incomes",
        children: [
          {
            field: "1day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[0] ?? "-" },
          },
          {
            field: "2day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[1] ?? "-" },
          },
          {
            field: "3day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[2] ?? "-" },
          },
          {
            field: "4day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[3] ?? "-" },
          },
          {
            field: "5day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[4] ?? "-" },
          },
          {
            field: "6day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[5] ?? "-" },
          },
          {
            field: "7day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[6] ?? "-" },
          },
          {
            field: "8day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[7] ?? "-" },
          },
          {
            field: "9day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[8] ?? "-" },
          },
          {
            field: "10day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[9] ?? "-" },
          },
          {
            field: "11day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[10] ?? "-" },
          },
          {
            field: "12day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[11] ?? "-" },
          },
          {
            field: "13day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[12] ?? "-" },
          },
          {
            field: "14day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[13] ?? "-" },
          },
          {
            field: "15day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[14] ?? "-" },
          },
          {
            field: "16day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[15] ?? "-" },
          },
          {
            field: "17day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[16] ?? "-" },
          },
          {
            field: "18day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[17] ?? "-" },
          },
          {
            field: "19day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[18] ?? "-" },
          },
          {
            field: "20day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[19] ?? "-" },
          },
          {
            field: "21day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[20] ?? "-" },
          },
          {
            field: "22day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[21] ?? "-" },
          },
          {
            field: "23day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[22] ?? "-" },
          },
          {
            field: "24day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[23] ?? "-" },
          },
          {
            field: "25day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[24] ?? "-" },
          },
          {
            field: "26day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[25] ?? "-" },
          },
          {
            field: "27day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[26] ?? "-" },
          },
          {
            field: "28day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[27] ?? "-" },
          },
          {
            field: "29day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[28] ?? "-" },
          },
          {
            field: "30day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[29] ?? "-" },
          },
          {
            field: "31day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[30] ?? "-" },
          },
          {
            field: "32day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[31] ?? "-" },
          },
          {
            field: "33day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[32] ?? "-" },
          },
          {
            field: "34day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[33] ?? "-" },
          },
          {
            field: "35day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[34] ?? "-" },
          },
          {
            field: "36day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[35] ?? "-" },
          },
          {
            field: "37day",
            wrapText: true,
            autoHeight: true,
            aggFunc: "sum",
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[36] ?? "-" },
          },
        ],
      },
    ]);

    onBeforeMount(() => {
      autoGroupColumnDef.value = {
        headerName: "Company, Group",
        field: "name",
        minWidth: 200,
        cellRenderer: "agGroupCellRenderer",
        pinned: "left",
        lockPinned: true,
        sortable: false,
        wrapHeaderText: true,
        suppressHeaderMenuButton: true,
        cellClass: "rag-blue",
        editable:'false',
      };
      aggFuncs.value = {
        // this overrides the grids built in sum function
        sum: sumFunction,
      };
      rowSelection.value = "single";
      gridApi.suppressAggFuncInHeader = true;

      rowClassRules.value = {
        // row style function
        "display-company": (params) => {
          console.log('params--->',params.node.key);
          var numSickDays = params.node.key;
          return numSickDays =="3*9";
        },
        // row style expression
        // "display-team": "data.team >= 'team 1'",
      };
    });

    const calculateTotalSum = () => {
      let sum = 0;
      const displayedRowCount = gridApi.value.getDisplayedRowCount();
      for (let i = 0; i < displayedRowCount; i++) {
        const rowData = gridApi.value.getDisplayedRowAtIndex(i);
        for (const [key, value] of Object.entries(rowData)) {
          if (typeof value === "number") {
            sum += value;
          }
        }
      }
      totalSum.value = sum;
      console.log("sum", sum);
    };

    const onGridReady = (params) => {
      gridApi.value = params.api;
      params.api.addAggFuncs({ sum: sumFunction });
      const updateData = (data) => (rowData.value = incomes);
      // const updateData = (data) => (rowData.value = data);
      fetch("https://www.ag-grid.com/example-assets/olympic-winners.json")
        .then((resp) => resp.json())
        .then((data) => updateData(data));

      const selectedRows = gridApi.value.getSelectedRows();
      // console.log("gridApi.value", gridApi.value);
      // console.log("selectedRows[0]--->", selectedRows[0]);

      calculateTotalSum();
    };

    const onBtnExport = () => {
      gridApi.value.exportDataAsCsv();
    };

    const onSelectionChanged = () => {
      const selectedRows = gridApi.value.getSelectedRows();
      // console.log("selectedRows[0]--->", selectedRows[0]);
      // document.querySelector("#selectedRows").innerHTML =
      //   selectedRows.length === 1 ? selectedRows[0].athlete : "-";
    };

    // Custom sum function
    window.sumFunction = function sumFunction(params) {
      let result = 0;
      params.values.forEach((value) => {
        if (typeof value === "number") {
          result += value;
        }
      });
      return result;
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
      aggFuncs,
      onSelectionChanged,
      rowClassRules,
      onBtnExport,
    };
  },
};
</script>
<template>
  <main style="min-width: 1124px; height: 700px">
    <div style="margin: 10px 0;">
        <button v-on:click="onBtnExport()">Download CSV export file</button>
      </div>
    <div style="height: 100%">
      <ag-grid-vue
        style="width: 100%; height: 100%"
        :class="themeClass"
        :columnDefs="columnDefs"
        @gridReady="onGridReady"
        :autoGroupColumnDef="autoGroupColumnDef"
        :defaultColDef="defaultColDef"
        :suppressRowClickSelection="true"
        :rowSelection="rowSelection"
        :rowGroupPanelShow="rowGroupPanelShow"
        :pivotPanelShow="pivotPanelShow"
        :pagination="true"
        :rowData="rowData"
        :aggFuncs="aggFuncs"
        :rowClassRules="rowClassRules"
        @selection-changed="onSelectionChanged"
      ></ag-grid-vue>
    </div>
    <div>Total Sum: {{ totalSum }}</div>
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
