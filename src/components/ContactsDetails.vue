<template>

  <div class="contacts-details">
    <div
      class="details"
    >
      <div class="details__header">
        <h2>Contact info</h2>
        <h3>{{ userName }}</h3>
      </div>
      <form @submit.prevent="showValue" class="form">
        <input
          type="text"
          maxlength="11"
          placeholder="Number"
          required
          v-model="number"
          onkeyup="this.value = this.value.replace (/\D/, '')"
          class="form__input"
        >
        <button type="submit" class="form__button">
          Add for this contact
        </button>
      </form>
      <div class="details__body">
        <h3 class="details__body--title"></h3>
        <div class="info">
          <div class="info__wrapper">
            <ul class="info__list" >
              <li
                class="info__item"
                v-for="number of numbers"
                :key="number.id"
              >
                <p
                  class="info__item--number"
                >
                  {{ number.number }}
                </p>
                <button
                  type="button"
                  class="remove-button"
                  v-show="numbers.length > 1"
                  @click.prevent="removeNumber(number.id)"
                ></button>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>

  </div>

</template>

<script>

export default {
  data() {
    return {
      number: '',
      id: 0,
      visible: Boolean,
    };
  },

  props: {
    numbers: Array,
    userName: String,
  },

  methods: {
    removeNumber(numbId) {
      this.$emit('numberRemove', numbId);
    },

    showValue() {
      this.$emit('addNumber', this.number);
      this.number = '';
    },
  },

};
</script>

<style lang="scss" scoped>
h2, h3 {
  text-align: center;
  margin: 0;
  padding: 16px;
}

h3 {
  font-size: 20px;
}

.form {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 20px;
  &__input {
    height: 30px;
    border-radius: 10px;
    border: grey 1px solid;
    padding: 0 16px;
    outline: none;
    transition: all 0.3s ease;
    &:hover {
      transform: scale(1.1);
    }
    &:focus {
      transform: scale(1.1);
      box-shadow: 2px 2px 4px;
    }
  }

  &__button {
    height: 32px;
    background-color: inherit;
    border-radius: 10px;
    outline: none;
    transition: all 0.3s ease;
    &:hover {
      background-color: grey;
      box-shadow: 2px 2px 4px;
    }
    &:active {
      background-color: black;
      color: white;
    }
  }
}
.contacts-details {
  width: 100%;
  height: 100%;
}

.details {
  background-color: white;
  border-radius: 10px;
  width: 100%;
  height: 100%;
}

.info__list {
  padding: 16px 36px;
}

.info__item {
  display: flex;
  justify-content: space-between;

  &--number {
    font-size: 20px;
    font-weight: 600;
  }
}
.remove-button {
  z-index: 0;
  position: relative;
  background-color: inherit;
  width: 25px;
  height: 25px;
  cursor: pointer;
  border: 2px solid black;
  border-radius: 50%;
  transition: all 0.3s ease;

  &:after {
    position: absolute;
    content: "";
    width: 15px;
    height: 18px;
    background-color: inherit;
    background-image: url("../svg/close.svg");
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    transition: background-color 0.3s ease;
  }

  &:hover {
    background-color: grey;
  }
}

</style>
