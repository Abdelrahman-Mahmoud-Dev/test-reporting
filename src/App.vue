<template>
  <div id="app">
    <button @click="click()">click</button>
    <div>
      <h2>Stimulsoft Reports.JS Viewer</h2>
      <div id="viewer"></div>
    </div>
  </div>
</template>

<script>
const report = new window.Stimulsoft.Report.StiReport();
const viewer = new window.Stimulsoft.Viewer.StiViewer(
      null,
      "StiViewer",
      false
    );
export default {
  name: "app",
  data() {
    return {
      report: null,
      viewer: null,
      dataSet: []
    };
  },
  mounted() {
    console.log("Loading Viewer view");
    console.log("Creating the report viewer with default options");
    console.log("Creating a new report instance");
    console.log("Load report from url");
    let data = []
          let response = fetch(
            "https://api-dev.finiexsoft.net/api/v1/accounting/account-card/parent/0"
      )
        .then(response => response.json())
        .then(({ data }) => {
          data = data
        });
      var dataSet = new Stimulsoft.System.Data.DataSet("SimpleDataSet");
          report.loadFile("/reports/SimpleList.mrt");
          dataSet.readJson(JSON.stringify(data));
          report.regData(dataSet.dataSetName, "", dataSet);




    viewer.report = report;

    console.log("Rendering the viewer to selected element");
    viewer.renderHtml("viewer");

    console.log("Loading completed successfully!");
  },
  methods: {
    click() {
      console.log("ere");

        // clear the report
        // report.report.clear();
        console.log(report)
// // var dataSet = new Stimulsoft.System.Data.DataSet("Demo");
      // // report.dictionary.databases.clear();
      // // console.log(new Stimulsoft.System.Data.DataSet("Demo"));
      // this.viewer.report.dictionary.databases.clear();
    }
  }
};
</script>

<style></style>
