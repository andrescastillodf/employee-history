<template>
  <LayoutManager :name="$system_config.viewSettings.Home.layout">
    <div>
      <!-- <h1>Employees History</h1> -->
      <GChart
        style="height: calc(100VH - 50px)"
        :settings="{ packages: ['timeline'] }"
        type="Timeline"
        :data="employees"
        :options="chartOptions"
      />
    </div>
    <!-- type="ColumnChart" -->
    <!-- https://developers.google.com/chart/interactive/docs/gallery/timeline -->
    <!-- https://www.npmjs.com/package/vue-google-charts -->
  </LayoutManager>
</template>

<script>
import { GChart } from "vue-google-charts";
import * as employeesSource from "@/api/employees.js";
export default {
  name: "Home",
  data() {
    return {
      chartOptions: {
        chart: {
          title: "Employees History",
          subtitle: "Time spend at company",
          showRowLabels: true
        }
      },
      employees: [["Term", "Employee", "From Year", "To Year"]]
      // employees: []
    };
  },
  components: {
    GChart
  },
  mounted() {
    // eslint-disable-next-line no-console
    let employees = this.employees;
    // eslint-disable-next-line no-console
    employeesSource.default.forEach(element => {
      // eslint-disable-next-line no-console
      // console.log(
      //   index.toString(),
      //   element.name,
      //   new Date(element.fromDate),
      //   element.toDate != "" ? new Date(element.toDate) : new Date()
      // );
      employees.push([
        element.name,
        element.name,
        new Date(element.fromDate),
        element.toDate != "" ? new Date(element.toDate) : new Date()
      ]);
    });
    employees.sort(function(a, b) {
      if (a[2] > b[2]) {
        return 1;
      }
      if (a[2] < b[2]) {
        return -1;
      }
      // a must be equal to b
      return 0;
    });
    employees.sort(function(a, b) {
      if (a[3] > b[3]) {
        return 1;
      }
      if (a[3] < b[3]) {
        return -1;
      }
      // a must be equal to b
      return 0;
    });

    this.employees = employees;
  }
};
</script>
