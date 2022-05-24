<template>
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <button class="close-button" @click.stop="$emit('close')">x</button>

          <div class="modal-header">
            <slot name="header">
              <h1>New security class</h1>
            </slot>
          </div>
          <div class="modal-body">
            <slot name="body">
              <form class="form-container" @submit.prevent="addClass()">
                <div class="form-container__item">
                  <label>Name</label>
                  <input v-model="securityClass.name" type="text"/>
                </div>
                <div class="form-container__item">
                  <label>Authorized amount</label>
                  <input v-model="securityClass.authorizedAmount" type="number"/>
                </div>
                <div class="form-container__item">
                  <label>Issued amount </label>
                  <input v-model="securityClass.issuedAmount" type="number"/>
                </div>
                <div class="form-container__item">
                  <label>Authorized capital </label>
                  <input v-model="securityClass.authorizedCapital" type="number"/>
                </div>
                <div class="form-container__item">
                  <label>Issued capital</label>
                  <input v-model="securityClass.issuedCapital" type="number"/>
                </div>
                <button type="submit" class="modal-button">
                  Add
                </button>
              </form>
            </slot>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script lang="ts">
import Vue from "vue";
import {Component} from "vue-property-decorator";

@Component({
  name: "AddClassModal",
})
export default class AddClassModal extends Vue {

  securityClass = {
    id: "d8654cb0-8986-4fbc-b969-025e598cb934",
    name: "",
    nominalValue: 1,
    authorizedAmount: 0,
    issuedAmount: 0,
    authorizedCapital: 0,
    issuedCapital: 0,
  }

  addClass() {
    this.$emit('newClass', this.securityClass)
    this.$emit('close')
  }
}

</script>

<style lang="scss">
.form-container {
  display: flex;
  flex-direction: column;

  input[type='text'], input[type="number"] {
    text-align: center;
    border: 1px solid black;
    border-radius: 5px;
  }

  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }

  &__item {
    width: 100%;
    display: flex;
    margin-bottom: 5px;
    justify-content: space-between;
  }
}

.close-button {
  position: absolute;
  width: 30px;
  height: 30px;
  top: -35px;
  right: -10px;
  border-radius: 50%;
  &:hover {
    background-color: #808080;
    color: #fff;
  }
}

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  position: relative;
  width: 400px;
  margin: 0 auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
}

.modal-body {
  margin: 20px 0;
}

.modal-button {
  border: 1px solid black;
  border-radius: 5px;
  background-color: #00966c;
  color: #fff;

  &:hover {
    background-color: #007a58;
  }
}

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>
