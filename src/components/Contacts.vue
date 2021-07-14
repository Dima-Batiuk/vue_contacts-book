<template>

  <div class="container">
    <contacts-list
      :contacts="contacts"
      @userSelected="setUser"
      @removeContact="removeContact"
      @addContact="addContact"
    ></contacts-list>
    <contacts-details
      :numbers="selectedContact.numbers"
      :userName="userName"
      @numberRemove="removeNumber"
      @addNumber="addNumber"
      v-show="userId"
    ></contacts-details>
  </div>

</template>

<script>
import ContactsDetails from './ContactsDetails.vue';
import ContactsList from './ContactsList.vue';
import numbers from '../api/numbers';
import users from '../api/users';

const getNumbersById = (userId) => (
  numbers.filter((numb) => numb.userId === userId)
);

const usersWithNumbers = users.map((user) => ({
  ...user,
  numbers: getNumbersById(user.id),
}));

export default {
  data() {
    return {
      userId: 0,
      contacts: [],
      selectedContact: {},
      userName: '',
    };
  },

  components: {
    ContactsDetails,
    ContactsList,
  },

  mounted() {
    this.contacts = usersWithNumbers;
  },

  methods: {
    setUser(userId) {
      this.userId = userId;
      this.selectedContact = this.contacts.find((contact) => contact.id === this.userId);
      this.userName = this.selectedContact.name;
    },

    removeContact(userId) {
      this.contacts = this.contacts.filter((contact) => contact.id !== userId);
      if (this.selectedContact.id === userId) {
        this.selectedContact = {};
        this.userId = 0;
      }
      console.log(this.contacts);
    },

    addNumber(number) {
      this.selectedContact.numbers = [
        ...this.selectedContact.numbers,
        {
          number,
          userId: this.userId,
          id: Date.now(),
        },
      ];
    },

    removeNumber(numbId) {
      this.selectedContact.numbers = [
        ...this.selectedContact.numbers
          .filter((number) => number.id !== numbId),
      ];
    },

    addContact(number, name) {
      this.contacts = [
        ...this.contacts,
        {
          name,
          id: this.contacts.length + 1,
          numbers: [{
            number,
            userId: this.contacts.length + 1,
            id: Date.now(),
          }],
        },
      ];
    },
  },
};

</script>

<style>
.container {
  width: 100%;
  box-sizing: border-box;
  padding: 36px;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 40px;
}
</style>
