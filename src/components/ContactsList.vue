<template>

  <div class="contacts">
    <form @submit.prevent="addContact" class="form">
      <input
        type="text"
        v-model="name"
        placeholder="Name"
        required
        class="form__input"
      >
      <input
        type="text"
        v-model="number"
        placeholder="Number"
        required
        maxlength="11"
        class="form__input"
        onkeyup="this.value = this.value.replace (/\D/, '')"
      >
      <button
        type="submit"
        class="form__button"
      >Save contact</button>
    </form>
    <h2>Your contacts</h2>
    <ul class="contacts__list">
      <li
        v-for="(contact, i) of contacts"
        :key="contact.id"
        class="contact__item">
        <p class="contact__name">{{ i + 1 }}. {{ contact.name }}</p>
        <div class="buttons">
          <button
            @click.prevent="viewDetails(contact.id)"
            class="contact__item--remove button"
          ></button>
          <button
            class="contact__item--details button"
            @click.prevent="removeUser(contact.id)"
          ></button>
        </div>
      </li>
    </ul>
  </div>

</template>

<script>

export default {
  data() {
    return {
      name: '',
      userId: 0,
      number: '',
      visible: false,
    };
  },

  props: {
    contacts: Array,
  },

  methods: {
    viewDetails(userId) {
      this.$emit('userSelected', userId);
    },

    removeUser(userId) {
      this.$emit('removeContact', userId);
    },

    addContact() {
      this.$emit('addContact', this.number, this.name);
      this.number = '';
      this.name = '';
    },
  },

};

</script>

<style lang="scss" scoped>

.form {
  width: 60%;
  display: flex;
  justify-content: space-around;
  align-items: center;
  margin: 0 auto;
  padding: 18px;
  gap: 20px;
  &__input {
    height: 30px;
    width: 35%;
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
    width: 30%;
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

.contacts {
  background-color: white;
  border-radius: 10px;
  width: 100%;
  height: 100%;
}

.contacts__list {
  width: 60%;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.contact__name {
  font-size: 20px;
  font-weight: 800;
}

.contact__item {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.buttons {
  padding: 36px;
  display: flex;
  gap: 10px;
}

h2 {
  text-align: center;
}
.button {
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
    width: 100%;
    height: 100%;
    position: absolute;
    color: black;
    top: 50%;
    left: 0;
    right: 0;
    text-align: center;
    transform: translateY(-50%);
  }
}

.contact__item--remove {

  &:after {
    content: "\26AC \26AC \26AC";
    font-weight: 600;
    font-size: 13px;
  }

  &:hover {
    background-color: gray;
    &:after {
      color: black;
    }
  }

  &:focus {
    background-color: black;
    &:after {
      color: white;
    }
  }
}

.contact__item--details {

  &:after {
    content: "\2716";
    font-weight: 800;
    font-size: 14px;
  }

  &:hover {
    background-color: gray;
    &:after {
      color: black;
    }
  }

  &:focus {
    background-color: black;
    &:after {
      color: white;
    }
  }
}

</style>
