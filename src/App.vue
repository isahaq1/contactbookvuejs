<template>
  <div id="app">
    <AddContactItem v-on:add-contact-event="addContactItem" v-on:edit-contact-event="editContactItemEvent" v-bind:editContact="editContact"/>
    <div>
      <Contacts v-bind:contacts="contacts" v-on:del-contact-event="deleteContactItem" v-on:edit-contact-event="editContactItem" />
    </div>
  </div>
</template>

<script>
import Contacts from "./components/Contacts";
import AddContactItem from "./components/AddContactItem";

import axios from 'axios';

export default {
  name: 'App',
  components: {
    Contacts,
    AddContactItem
  },
  data () {
    return {
      contacts   : [],
      editContact: {
      title      : '',
      phone      : '',
      company    : '',
      address    : '',
      created_at : '',
      id         : ''
      }
    }
  },
  methods: {
    addContactItem(newContact){
        this.contacts = [...this.contacts, newContact];
    },
    deleteContactItem(id){
       axios
      .post('http://localhost/saleserp_v9.8/api/delete_contact/{id}')
      .then(response => (console.log(response.data.message)))
      this.contacts = this.contacts.filter(contact => contact.id !== id);
    },
    editContactItem(id){
      //find the index of the contact's id
      let objIndex = this.contacts.findIndex(obj=> obj.id === id);
      this.editContact.title   = this.contacts[objIndex].title;
      this.editContact.phone   = this.contacts[objIndex].phone;
      this.editContact.company = this.contacts[objIndex].company;
      this.editContact.address = this.contacts[objIndex].address;
      this.editContact.id      = id;
    },
    editContactItemEvent(contactItem){
      //find the index of this id's object
      let objIndex = this.contacts.findIndex(obj => obj.id === contactItem.id)
      //update the item
      this.contacts[objIndex].title   = contactItem.title;
      this.contacts[objIndex].phone   = contactItem.phone;
      this.contacts[objIndex].company = contactItem.company;
      this.contacts[objIndex].address = contactItem.address;
      this.contacts[objIndex].updated_at = new Date();
    }
  },
  watch: {
    contacts: {
      handler() {
        // localStorage.setItem('contacts',JSON.stringify(this.contacts))

      
          axios
      .post('http://localhost/saleserp_v9.8/api/add_contact',this.contacts)
      .then(response => (console.log(response)))
      },
      deep: true
    }
  },
  mounted() {
      axios
      .get('http://localhost/saleserp_v9.8/api/contact_list')
      .then(response => (this.contacts = response.data.contacts))
  }
}
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>