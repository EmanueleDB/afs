<template>
  <div class="home">
    <h1>This is a table with some important data</h1>
    <button @click="showModal = true">New Class</button>
    <AddClassModal v-if="showModal" @close="showModal = false" @newClass="setNewClass"/>
    <b-table :data="tableData" :columns="columns">
      <template slot="footer">
        <td>{{ totals.name }}</td>
        <td>{{ totals.totAuthorizedAmount }}</td>
        <td>{{ totals.totIssuedAmount }}</td>
        <td>{{ totals.totAuthorizedCapital }}</td>
        <td>{{ totals.totIssuedCapital }}</td>
      </template>
    </b-table>
  </div>
</template>

<script lang="ts">
import {Component, Vue} from "vue-property-decorator";
import {TableData} from "@/types/types";
import AddClassModal from '../utilities/AddClassModal.vue'

@Component({
  components: {AddClassModal},
})

export default class Home extends Vue {
  tableData: TableData[] = [];
  columns = [
    {
      label: "Security class",
      field: "name",
    },
    {
      label: "Authorized amount",
      field: "authorizedAmount",
    },
    {
      label: "Issued amount",
      field: "issuedAmount",
    },
    {
      label: "Authorized Capital",
      field: "authorizedCapital",
    },
    {
      label: "Issued capital",
      field: "issuedCapital",
    },
  ];
  loading = false;
  totals = {
    name: 'Total',
    totAuthorizedAmount: 0,
    totIssuedAmount: 0,
    totAuthorizedCapital: 0,
    totIssuedCapital: 0,
  };
  showModal = false
  // mounted works fine if your ide complains about it
  // eslint-disable-next-line @typescript-eslint/explicit-module-boundary-types
  mounted() {
    this.setData()
  }

  async setData() {
    this.loading = true
    try {
      const response = await this.getData()
      this.tableData = response.map((dataItem: TableData) => {
        return {
          ...dataItem,
          randomNumber: Math.random(),
        }
      })
      await this.getTotal()
      this.loading = false
    } catch (e) {
      console.log(e, "This is not good")
    }
  }


  async getTotal() {
    for (let item of this.tableData) {
      this.totals.totAuthorizedAmount += item.authorizedAmount
      this.totals.totIssuedAmount += item.issuedAmount
      this.totals.totAuthorizedCapital += item.authorizedCapital
      this.totals.totIssuedCapital += item.issuedCapital
    }
  }

  setNewClass(newClass: TableData) {
    this.totals.totAuthorizedAmount = 0
    this.totals.totIssuedAmount = 0
    this.totals.totAuthorizedCapital = 0
    this.totals.totIssuedCapital = 0
    this.tableData.push(newClass)
    this.getTotal()
  }

  async getData(): Promise<TableData[]> {
    return [
      {
        id: "42f2462d-49d0-4e91-8fe1-de2e656b0f06",
        name: "Series A",
        nominalValue: 5,
        authorizedAmount: 1500,
        issuedAmount: 500,
        authorizedCapital: 7550,
        issuedCapital: 2500,
      },
      {
        id: "42f2462d-49d0-4e91-8fe1-de2e656b0f06",
        name: "Series B",
        nominalValue: 10,
        authorizedAmount: 15000,
        issuedAmount: 5000,
        authorizedCapital: 150000,
        issuedCapital: 50000,
      },
      {
        id: "fd78c11b-e3d2-455a-99b0-49907a75c463",
        name: "Series C",
        nominalValue: 1,
        authorizedAmount: 96876,
        issuedAmount: 61760,
        authorizedCapital: 96876,
        issuedCapital: 61760,
      },
      {
        id: "d8654cb0-8986-4fbc-b969-025e514cb934",
        name: "Series D",
        nominalValue: 1,
        authorizedAmount: 10110,
        issuedAmount: 1100,
        authorizedCapital: 10110,
        issuedCapital: 1100,
      },
    ];
  }
}
</script>

<style lang="scss">
.table-footer {
  font-weight: bold;
}
</style>
