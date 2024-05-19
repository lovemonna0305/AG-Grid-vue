<template>
  <div align="left">
    <button type="button" @click="addRow">Add Row</button>
    <button type="button" @click="removeRow">Remove Row</button>
    <button @click="exportAsExcel">Export Excel</button>
    <button @click="exportAsCsv">Export CSV</button>
  </div>
  <br />

  <vue-excel-editor
    ref="grid"
    v-model="jsondata"
    @cell-focus="onCellFocus"
    @delete="onDelete"
    @update="onUpdate"
    filter-row
    :localized-label="myLabels"
  >
    <vue-excel-column
      field="company"
      label="User ID"
      type="string"
      width="80px"
      key-field
    />
    <vue-excel-column field="name" label="Name" type="string" width="150px" />
    <vue-excel-column
      field="phone"
      label="Contact"
      type="string"
      width="130px"
    />
    <vue-excel-column
      field="gender"
      label="Gender"
      type="select"
      width="50px"
      :options="['F', 'M', 'U']"
    />
    <vue-excel-column
      field="age"
      label="Age"
      type="number"
      width="70px"
      summary="sum"
    />
    <vue-excel-column
      field="birth"
      label="Date Of Birth"
      type="date"
      width="80px"
    />
  </vue-excel-editor>
  <div align="left">
    <p>logging jsondata</p>
    <ul>
      <li v-for="json in jsondata" :key="json.$id">
        {{ json.$id }} - {{ json.user }}
      </li>
    </ul>
  </div>
</template>

<script>
// import incomes from './dataexcel.json';

export default {
  name: "App",
  data() {
    return {
      myLabels: {
        footerLeft: (top, bottom) => `纪录 ${top} 至 ${bottom}`,
        first: "头页",
        previous: "上一页",
        next: "下一页",
        last: "尾页",
        footerRight: {
          selected: "选择：",
          filtered: "过滤：",
          loaded: "载入：",
        },
        processing: "工作中",
        tableSetting: "表格设定",
        exportExcel: "汇出 Excel",
        importExcel: "汇入 Excel",
        back: "关",
        reset: "预设",
        sortingAndFiltering: "排序及过滤",
        sortAscending: "小至大排序",
        sortDescending: "大至小排序",
        near: "≒ 接近",
        exactMatch: "= 等于",
        notMatch: "≠ 不等于",
        greaterThan: "&gt; 大于",
        greaterThanOrEqualTo: "≥ 大于或等于",
        lessThan: "&lt; 少于",
        lessThanOrEqualTo: "≤ 少于或等于",
        regularExpression: "~ 正规表示式",
        customFilter: "过滤内容",
        listFirstNValuesOnly: (n) => `只列出 ${n} 项`,
        apply: "应用",
        noRecordIsRead: "没有纪录被读取",
        readonlyColumnDetected: "不可更新唯读纪录",
        columnHasValidationError: (name, err) =>
          `纪录栏位 ${name} 发生核实错误: ${err}`,
        noMatchedColumnName: "没有能配对之栏位",
        invalidInputValue: "输入错误内容",
        missingKeyColumn: "找不到关键栏位",
        noRecordIndicator: "沒有纪录",
      },
      jsondata: [
        {
          name: "다다다",
          organization: "3*9",
          team: "team-main 1",
          plan: 2000,
          earning: 1000.0,
          pending: -1000.0,
          "1day": 100,
          "2day": 100,
          "3day": 100,
          "4day": 100,
          "5day": 100,
          "6day": 100,
          "7day": 100,
          "8day": 100,
          "9day": 100,
          "10day": 100,
          "11day": 100,
          "12day": 100,
          "13day": 100,
          "14day": 100,
          "15day": 100,
          "16day": 100,
          "17day": 100,
          "18day": 100,
          "19day": 100,
          "20day": 100,
          "21day": 100,
          "22day": 100,
          "23day": 100,
          "24day": 100,
          "25day": 100,
          "26day": 100,
          "27day": 100,
          "28day": 100,
          "29day": 100,
          "30day": 100,
          "31day": 100,
        },
      ],
      selectedRow: {},
      currentRowPos: 0,
      currentColPos: 0,
    };
  },
  methods: {
    onCellFocus(event) {
      let { record, rowPos, colPos } = event;
      this.selectedRow = { ...record };
      this.currentRowPos = rowPos;
      this.currentColPos = colPos;
      console.log("onCellFocus : ", event);
      console.log("selectedRow : ", this.selectedRow);
    },
    addRow() {
      let rec = {
        user: "kl",
        name: "Kenny Linus",
        phone: "1-891-2345685",
        gender: "M",
        age: 29,
        birth: "1990-09-01",
      };
      this.jsondata.splice(this.currentRowPos + 1, 0, rec);
      // fix by this block
      // let newJsonData = this.jsondata;
      // this.jsondata = [...newJsonData];
      // fix by this block
      this.$refs.grid.moveTo(this.currentRowPos + 1, this.currentColPos);
      console.log(this.jsondata);
    },
    removeRow() {
      this.jsondata.splice(this.currentRowPos, 1);
      // fix by this block
      let newJsonData = this.jsondata;
      this.jsondata = [...newJsonData];
      // fix by this block
      this.$refs.grid.moveTo(this.currentRowPos, this.currentColPos);
      console.log(this.jsondata);
    },

    exportAsExcel() {
      const format = "xlsx";
      const exportSelectedOnly = true;
      const filename = "test";
      this.$refs.grid.exportTable(format, exportSelectedOnly, filename);
    },
    exportAsCsv() {
      const format = "csv";
      const exportSelectedOnly = true;
      const filename = "test";
      this.$refs.grid.exportTable(format, exportSelectedOnly, filename);
    },
  },
};
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
</style>
