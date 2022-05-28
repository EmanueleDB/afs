<template>
  <div class="transfers">
    <h1 class="title is-1">Transfers</h1>
    <label
    >Search
      <input v-model="searchTerms" type="text"/>
    </label>
    <div>
      <button class="edit-btn" @click="updateTransfers">
        Update transfers
      </button>
      <div class="card-container">
        <TransferRow
            v-for="(transfer, index) in searchedTransfers"
            :key="transfer.forgottenProperty ? transfer.forgottenProperty : transfer.transactionIdentifier"
            :transfer="transfer"
            :color="colors[index % colors.length]"
            :class="colors[index % colors.length]"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {Component, Vue} from "vue-property-decorator";
import {Transaction} from "@/types/types";
import TransferRow from "@/components/transferRow.vue";
import transfers from "@/assets/data";

@Component({
  name: "Transfers",
  components: {TransferRow},
})

export default class Transfers extends Vue {
  searchTerms = "";
  transfers = transfers;
  colors = ['purple', 'green', 'orange', 'red', 'pink'];

// eslint-disable-next-line @typescript-eslint/explicit-module-boundary-types
  get searchedTransfers() {
    if (this.searchTerms)
      return this.transfers.filter((transfer: Transaction) => transfer.recordDate?.includes(this.searchTerms))
    return this.transfers;
  }

  // The button wasn't working properly because Vue 2 cannot detect when you update a single index in an array
  // this.transfers[0] = {...} The array will update, but Vue won't know that anything changed. (Reactivity)
  // Splice in combination with the new key in the for loop, will make the component re-render
  // The only property that is new and will make all the items of the array being re-render is the forgottenProperty
  // but it would be undefined when the component mounts so I set the key to the transactionIdentifier if the forgottenProperty
  // is not present yet

  updateTransfers(): void {
    this.transfers.splice(0, 1, {
      splitFactor: null,
      exDate: null,
      amount: 10000,
      companyId: "568fa387-43d1-499a-bba2-25089f5a881a",
      notes: null,
      pricePerShare: null,
      recordDate: "2021-07-01",
      securityClassId: "ab983cfe-a932-4e25-98ea-f5928a839fe1",
      securityClass: {name: "Common"},
      state: "OLD",
      toSecurityHolderId: "dd971e7f-386b-45dd-93e1-666fbeed0a55",
      toSecurityHolder: {
        fullName: "Jeff Dunlap",
        type: "PERSON",
      },
      transactionIdentifier: "41095fdb-6b52-4257-aef8-dc523d782e53",
      positionWithinDay: 3,
      type: "ISSUE_STOCK",
    })
    this.transfers.forEach((transfer) => {
      transfer.forgottenProperty = `Important data: ${(Math.random() * 100000000).toString().slice(1, 8)}`
    });
  }
}
</script>
<style scoped lang="scss">
$colors: purple, pink, red, orange, green;
.edit-btn {
  margin: 2rem;
}

.card-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

@each $color in $colors {
  .#{$color} {
    border-left: 10px solid $color;
  }
}
</style>
