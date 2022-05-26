<template>
  <div class="card">
    <div class="card__header">
      <p v-if="transfer.fromSecurityHolder">{{ transfer.fromSecurityHolder }}</p>
      <div class="card__container" style="width: 40px">
        <p class="card__header__amount">{{ transfer.amount }}</p>
      </div>
      <div style="display: flex; flex-direction: row;">
        <div style="display: flex; flex-direction: column; align-items: center; width: 20px; margin-left:40px">
          <div class="circle" :style="'border: 1px solid ' + color + ';'"></div>
          <div class="line" :style="'border: 1px dashed ' + color + ';'"></div>
          <div class="circle" :style="'border: 1px solid ' + color + ';'"></div>
        </div>
        <div class="box-text">
          <div style="position: relative">
            <p style="position: absolute; top: -7px">{{ transfer.type }}</p>
          </div>
          <div v-if="transfer.forgottenProperty" style="position: relative; width: 200px; height: 30px">
            <p style="position: absolute; bottom: -7px">{{ transfer.forgottenProperty }}</p>
          </div>
        </div>
      </div>
    </div>
    <div class="card__body">
      <p>Date</p>
      <p>Position Within Day</p>
      <p>State</p>
    </div>
    <div class="card__footer">
      <p>{{ transfer.recordDate }}</p>
      <p>{{ transfer.positionWithinDay }}</p>
      <p>{{ transfer.state }}</p>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import {Component, Prop} from "vue-property-decorator";
import {Transaction} from "@/types/types";

@Component({
  name: "TransferRow",
})
export default class TransferRow extends Vue {
  @Prop({required: true}) transfer!: Transaction;
  @Prop({required: true}) color!: string;


  mounted() {
    console.log(this.transfer)
  }
}
</script>

<style lang="scss">
.card {
  position: relative;
  width: 400px;
  height: 200px;
  border: 1px solid lightgray;
  border-radius: 10px;
  margin: 1rem;
  padding: 15px;
  box-shadow: rgba(0, 0, 0, 0.35) 0 5px 15px;

  &__header {
    display: flex;
    justify-content: flex-start;
    margin: 20px 0 40px 0;
  }

  &__body {
    display: flex;
    justify-content: space-between;
  }

  &__footer {
    display: flex;
    justify-content: space-between;
  }

  .circle {
    width: 10px;
    height: 10px;
    border-radius: 50%;
  }

  .line {
    width: 0;
    height: 30px;
    margin: 2px 0;
  }

  .box-text {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
}
</style>
