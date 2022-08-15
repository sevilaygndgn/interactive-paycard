<template>
  <div class="container">
    <header>
      <span class="title">Add Credit Card</span>
    </header>
    <div class="credit-card" :class="{behind : cardIsFlip}" >
      <div class="card-wrapper">
        <div class="front">
          <img src="../assets/icons/chip.png" alt="" width="50px" height="50px"/>
          <transition name="slide">
            <span class="card-number">
              {{ card.number }}
            </span>
          </transition>
          <div class="name-valid">
            <div class="name-area">
              <span class="card-holder">Cardholder Name</span>
              <span class="fullname">{{ card.name }}</span>
            </div>
            <div class="expires">
              <span class="valid-thru">Valid Thru</span>
              <span class="date">{{ card.valid }}</span>
            </div>
          </div>
        </div>
        <div class="back">
          <div class="color-area"></div>
          <div class="security-code-area">
            <span class="security-code-text">Security Code</span>
            <span class="cvv-text">{{ card.cvv }}</span>
          </div>
        </div>
      </div>
    </div>
    <div class="card-number-name-area">
      <div class="card-input">
        <label>Card Number</label>
        <input
          v-model="card.number"
          v-mask="'#### #### #### ####'"
        />
      </div>
      <div class="card-input">
        <label>Cardholder Name</label>
        <input
          type="text"
          v-model="card.name"
        />
      </div>
    </div>
    <div class="valid-expires">
      <div class="valid-expires-input valid">
        <label>Valid Thru</label>
        <input
          v-model="card.valid"
          v-mask="'##/##'"
        />
      </div>
      <div class="valid-expires-input">
        <label>CVV</label>
        <input
          v-model="card.cvv"
          v-mask="'###'"
          @focus="cardIsFlip = true"
          @focusout="cardIsFlip = false"
        />
      </div>
    </div>
    <button class="save-card">Save Card</button>
  </div>
</template>
<script>
import { TheMask } from "vue-the-mask";
export default {
  name: "HomeView",
  data() {
    return {
      cardIsFlip: false,
      card: {
        number: "",
        name: "",
        valid: "",
        cvv: "",
      },
    };
  },
  components: { TheMask },

  // methods: {
  //   flipCardFunc(className) {
  //     const creaditCard = document.querySelector(".credit-card");
  //     if (className === "behind") {
  //       creaditCard.classList.add(className);
  //       return;
  //     }
  //     creaditCard.classList.remove("behind");
  //   },
  // },
};
</script>
<style lang="scss" scoped>
.container {
  background-color: #ffffff;
  height: 650px;
  border-radius: 20px;
  padding: 2em;
  display: grid;
  row-gap: 20px;
  header {
    display: flex;
    justify-content: center;
    .title {
      font-family: "Roboto", sans-serif;
      font-size: 30px;
      color: #434768;
    }
  }
  label{
      display: grid;
      row-gap: 5px;
      color: #99a5af;
      font-family: "Roboto", sans-serif;
  }
  input{
        border: 1px solid #dee7eb;
        border-radius: 5px;
        height: 40px;
        &:focus{
          border-color: rgba(147, 147, 255, 0.962);
        }
  }
  .credit-card {
    perspective: 1200px;
    &.behind {
      .card-wrapper {
        transform: rotateY(180deg);
      }
    }
    .card-wrapper {
      position: relative;
      height: 200px;
      transform-style: preserve-3d; //arka tarafa döndürüyor, kullanmazsak kartı ters çeviriyo
      transition: transform 0.6s;
    }
    .front,
    .back {
      position: absolute;
      width: 100%;
      height: 200px;
      backface-visibility: hidden; //arka yüzünü gizledik
      border-radius: 10px;
      display: grid;
      row-gap: 15px;
      background-color: #343eaf;
    }
    .front {
      padding: 1em;
    }
    .back {
      transform: rotateY(180deg); //arkada dursun diye 180 derece döndürdük
      .color-area {
        background-color: #2c3383;
        height: 45px;
        margin-top: 30px;
      }
      .security-code-area {
        padding: 1em;
        display: grid;
        justify-items: flex-end;
        font-family: "Roboto", sans-serif;
        font-size: 15px;
        color: #faf9fc;
      }
    }
    .card-number {
      display: flex;
      justify-content: center;
      font-family: "Farsan", cursive;
      font-size: 35px;
      color: #faf9fc;
      font-weight: bold;
    }
    .name-valid {
      display: flex;
      justify-content: space-between;
      font-family: "Roboto", sans-serif;
      .name-area {
        display: grid;
        color: #faf9fc;
        .card-holder {
          font-size: 13px;
        }
      }
      .expires {
        display: grid;
        color: #faf9fc;
        font-family: "Roboto", sans-serif;
        .valid-thru {
          font-size: 13px;
        }
      }
    }
  }
  .card-number-name-area {
    display: grid;
    row-gap: 10px;
    .card-input {
      display: grid;
      row-gap: 5px;
      color: #99a5af;
    }
  }
  .valid-expires {
    display: flex;
    .valid-expires-input {
      display: grid;
      row-gap: 5px;
      &.valid{
        margin-right: 10px;
      }
    }
  }
  .save-card {
    border-radius: 20px;
    border: none;
    height: 50px;
    background-color: #ff7143;
    color: #ffffff;
    font-family: "Roboto", sans-serif;
    font-size: 20px;
    &:hover {
      cursor: pointer;
    }
  }
}
</style>
