<script>
import { createApp, onBeforeMount, ref } from "vue";
import { AgGridVue } from "ag-grid-vue3";
import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-quartz.css";
import incomes from "./dataAG.json";
import CustomHeader from "./CustomHeader.vue";
import "./styles.css";

class ShowCellRenderer {
  init(params) {
    const cellBlank = !params.value;
    if (cellBlank) {
      return;
    }

    this.ui = document.createElement("div");
    this.ui.innerHTML =
      '<div class="show-name">' + params.value + "" + "</div>";
  }

  getGui() {
    return this.ui;
  }

  refresh() {
    return false;
  }
}

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
        field: "show",
        // cellRenderer: ShowCellRenderer,
        // rowSpan: (params) => {
        //   if (params.data.show) {
        //     return 4;
        //   } else {
        //     return 1;
        //   }
        // },
        cellClassRules: { "show-cell": "value !== undefined" },
        width: 100,
        cellDataType: false,
        editable: false,
        pinned: "left",
        headerComponent: CustomHeader,
        headerComponentParams: { displayName: "Company" },
      },
      // {
      //   field: "organization",
      //   wrapText: true,
      //   autoHeight: true,
      //   hide: true,
      //   pinned: "left",
      //   lockPinned: true,
      //   wrapHeaderText: true,
      //   editable: "false",
      // },
      {
        headerName: "Details",
        children: [
          {
            field: "team",
            wrapText: true,
            autoHeight: true,
            pinned: "left",
            width: 50,
            lockPinned: true,
            wrapHeaderText: true,
            editable: "false",
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: "Team" },
          },
          {
            headerName: "Name",
            field: "name",
            width: 80,
            pinned: "left",
            lockPinned: true,
            sortable: false,
            wrapHeaderText: true,
            editable: "false",
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: "Name" },
          },
          {
            field: "plan",
            wrapText: true,
            autoHeight: true,
            pinned: "left",
            lockPinned: true,
            wrapHeaderText: true,
            width: 100,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: "Plan" },
            // cellClass: "rag-blue",
          },
          {
            field: "earning",
            wrapText: true,
            autoHeight: true,
            pinned: "left",
            lockPinned: true,
            wrapHeaderText: true,
            width: 100,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: "Earning" },
            valueGetter:
              " getValue('1day') + getValue('2day') + getValue('3day') + getValue('4day')+ getValue('5day')+ getValue('6day')+ getValue('6day')+ getValue('8day')+ getValue('9day')+ getValue('10day')+ getValue('11day')+ getValue('12day')+ getValue('13day')+ getValue('14day')+ getValue('15day')+ getValue('16day')+ getValue('17day')+ getValue('18day')+ getValue('19day')+ getValue('20day')+ getValue('21day')+ getValue('22day')+ getValue('23day')+ getValue('24day')+ getValue('25day')+ getValue('26day')+ getValue('27day')+ getValue('28day')+ getValue('29day')+ getValue('30day')+ getValue('31day')",
            editable: "false",
          },
        ],
      },
      {
        headerName: "Daily Incomes",
        children: [
          {
            field: "1day",
            headerName: dates.value[0] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[0] ?? "-" },
          },
          {
            field: "2day",
            headerName: dates.value[1] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[1] ?? "-" },
          },
          {
            field: "3day",
            headerName: dates.value[2] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[2] ?? "-" },
          },
          {
            field: "4day",
            headerName: dates.value[3] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[3] ?? "-" },
          },
          {
            field: "5day",
            headerName: dates.value[4] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[4] ?? "-" },
          },
          {
            field: "6day",
            headerName: dates.value[5] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[5] ?? "-" },
          },
          {
            field: "7day",
            headerName: dates.value[6] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[6] ?? "-" },
          },
          {
            field: "8day",
            headerName: dates.value[7] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[7] ?? "-" },
          },
          {
            field: "9day",
            headerName: dates.value[8] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[8] ?? "-" },
          },
          {
            field: "10day",
            headerName: dates.value[9] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[9] ?? "-" },
          },
          {
            field: "11day",
            headerName: dates.value[10] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[10] ?? "-" },
          },
          {
            field: "12day",
            headerName: dates.value[11] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[11] ?? "-" },
          },
          {
            field: "13day",
            headerName: dates.value[12] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[12] ?? "-" },
          },
          {
            field: "14day",
            headerName: dates.value[13] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[13] ?? "-" },
          },
          {
            field: "15day",
            headerName: dates.value[14] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[14] ?? "-" },
          },
          {
            field: "16day",
            headerName: dates.value[15] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[15] ?? "-" },
          },
          {
            field: "17day",
            headerName: dates.value[16] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[16] ?? "-" },
          },
          {
            field: "18day",
            headerName: dates.value[17] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[17] ?? "-" },
          },
          {
            field: "19day",
            headerName: dates.value[18] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[18] ?? "-" },
          },
          {
            field: "20day",
            headerName: dates.value[19] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[19] ?? "-" },
          },
          {
            field: "21day",
            headerName: dates.value[20] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[20] ?? "-" },
          },
          {
            field: "22day",
            headerName: dates.value[21] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[21] ?? "-" },
          },
          {
            field: "23day",
            headerName: dates.value[22] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[22] ?? "-" },
          },
          {
            field: "24day",
            headerName: dates.value[23] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[23] ?? "-" },
          },
          {
            field: "25day",
            headerName: dates.value[24] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[24] ?? "-" },
          },
          {
            field: "26day",
            headerName: dates.value[25] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[25] ?? "-" },
          },
          {
            field: "27day",
            headerName: dates.value[26] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[26] ?? "-" },
          },
          {
            field: "28day",
            headerName: dates.value[27] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[27] ?? "-" },
          },
          {
            field: "29day",
            headerName: dates.value[28] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[28] ?? "-" },
          },
          {
            field: "30day",
            headerName: dates.value[29] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[29] ?? "-" },
          },
          {
            field: "31day",
            headerName: dates.value[30] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[30] ?? "-" },
          },
          {
            field: "32day",
            headerName: dates.value[31] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[31] ?? "-" },
          },
          {
            field: "33day",
            headerName: dates.value[32] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[32] ?? "-" },
          },
          {
            field: "34day",
            headerName: dates.value[33] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[33] ?? "-" },
          },
          {
            field: "35day",
            headerName: dates.value[34] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[34] ?? "-" },
          },
          {
            field: "36day",
            headerName: dates.value[35] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[35] ?? "-" },
          },
          {
            field: "37day",
            headerName: dates.value[36] ?? "-",
            wrapText: true,
            autoHeight: true,
            minWidth: 70,
            headerComponent: CustomHeader,
            headerComponentParams: { displayName: dates.value[36] ?? "-" },
          },
        ],
      },
    ]);

    onBeforeMount(() => {
      rowSelection.value = "single";
      gridApi.suppressAggFuncInHeader = true;

      rowClassRules.value = {
        // row style function
        "display-company": (params) => {
          if (params.data.show == null) {
            return null;
          }
          var company = params.data.show;
          return (
            company == "3*9" ||
            company == "5*4" ||
            company == "8*2" ||
            company == "AI" ||
            company == "Net Manager"
          );
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
      let flag_show_3 = false;
      let sum_company_earning = {
        0:0,
        1:0,
        2:0,
      };
      let sum_company_plan = {};
      let newArray = [];
      incomes.forEach(function (item) {
        if (item.organization.includes("3*9")) {
          if (flag_show_3) {
            console.log("329 groups", item.earning);
            sum_company_earning += item.earning;
            return;
          }
          sum_company_earning += item.earning;
          flag_show_3 = true;
          console.log("329 set!");
        } else if (item.organization.includes("5*4")) {
          // console.log(item.organization);
        } else if (item.organization.includes("8*1")) {
          // console.log(item.organization);
        } else if (item.organization.includes("AI")) {
          // console.log(item.organization);
        } else {
          // console.log(item.organization);
        }
      });

      console.log("sum_company_earning for 3*9--->", sum_company_earning[0]);

      // foreach (let i in incomes) {
      //   console.log('let i-->', i);
      // }
      const updateData = (data) => (rowData.value = incomes);

      // const updateData = (data) => (rowData.value = data);
      fetch("https://www.ag-grid.com/example-assets/olympic-winners.json")
        .then((resp) => resp.json())
        .then((data) => updateData(data));

      const selectedRows = gridApi.value.getSelectedRows();

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

    window.rowSpan = function rowSpan(params) {
      if (params.data.show) {
        return 4;
      } else {
        return 1;
      }
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
    <div style="margin: 10px 0">
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
