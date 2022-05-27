<template>
  <div class="card">
    <div class="card__header">
      <p v-if="transfer.fromSecurityHolder">{{ transfer.fromSecurityHolder }}</p>
      <div class="card__container">
        <p class="card__header__amount">{{ transfer.amount }}</p>
      </div>
      <div class="card__container__circles">
        <div class="card__container__circles__container">
          <div class="circle" :style="'border: 2px solid ' + color + ';'"></div>
          <div class="line" :style="'border: 1px dashed ' + color + ';'"></div>
          <div class="circle" :style="'border: 2px solid ' + color + ';'"></div>
        </div>
        <div class="card__container__circles__content">
          <div class="card__container__circles__content__first">
            <p class="card__container__circles__content__first-text">{{ transfer.type }}</p>
          </div>
          <div class="card__container__circles__content__second" v-if="transfer.forgottenProperty">
            <p class="card__container__circles__content__second-text">
              {{ transfer.forgottenProperty }}</p>
          </div>
        </div>
      </div>
    </div>
    <div class="card__body">
      <div class="card__body__content">
        <p>DATE</p>
        <p class="card__body__content__date">{{ transfer.recordDate }}</p>
      </div>
      <div class="card__body__content">
        <p>POSITION</p>
        <p>{{ transfer.positionWithinDay }}</p>
      </div>
      <div class="card__body__content">
        <p>STATE</p>
        <p>{{ transfer.state }}</p>
      </div>
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
}
</script>

<style lang="scss">
.card {
  position: relative;
  width: 370px;
  height: 180px;
  border: 1px solid lightgray;
  border-radius: 10px;
  margin: 1rem;
  padding: 15px;
  box-shadow: rgba(0, 0, 0, 0.35) 0 5px 15px;

  &__container {
    width: 110px;
    text-align: left;

    &__circles {
      display: flex;
      flex-direction: row;

      &__content {
        display: flex;
        flex-direction: column;
        justify-content: space-between;

        &__first {
          position: relative;

          &-text {
            position: absolute;
            top: -4px;
            font-size: 12px;
            font-weight: 500;

          }
        }

        &__second {
          position: relative;
          width: 200px;
          height: 30px;

          &-text {
            position: absolute;
            bottom: -4px;
            font-size: 12px;
            font-weight: 500;

          }
        }
      }

      &__container {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-right: 10px;
      }
    }
  }

  &__header {
    display: flex;
    justify-content: flex-start;
    margin: 10px 0 40px 0;

    &__amount {
      font-size: 16px;
      font-weight: 500;
    }
  }

  &__body {
    display: flex;
    justify-content: space-between;

    &__content {
      width: 110px;
      text-align: left;

      p:first-child {
        font-size: 12px;
        font-weight: 400;
        opacity: 0.4;
      }

      p:last-child {
        font-size: 15px;
        font-weight: 800;
        opacity: 0.5;
      }

      &__date {
        font-size: 12px !important;
        font-weight: 500 !important;
        opacity: 0.6 !important;
      }
    }
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
}
</style>
