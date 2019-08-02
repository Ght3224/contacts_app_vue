<template>
  <div class="container">
  <p>LastName: <input type="text" v-model="newContactName"><p>
  <button v-on:click="createContact ()">create Contact</button>
  <!-- </div> -->
   <h1> {{message}}</h1>
   <div v-for="contact in contacts">
    <p> {{contact.first_name}} </p>
  </div>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios'; 

export default {
  data: function() {
    return {
      message: "contacts",
      contacts: [], 
      newContactName: "",
      newEmail: "", 
      phoneNum: ""
    };
  },
  created: function() {
    console.log("i am contact");
    axios.get('/api/contacts').then(response => {
      this.contacts = response.data;
    });
  },
  methods: {
    createContact: function() {
      console.log("testing");

      var newContact = {
        last_name: this.newContactName
      }; 
      axios.post('/api/contacts', newContact).then(response => {
        console.log(response.data); 
        this.contacts.push(response.data); 
      }); 
    }
  }
};

</script>
