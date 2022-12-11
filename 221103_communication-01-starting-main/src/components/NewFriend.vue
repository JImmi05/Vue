<template>
    <li>
      <h2>Add Friend</h2>
  
      <label for="name">Name:</label><br />
      <input type="text" v-model="enteredname" /><br />
  
      <label for="email">E-Mail:</label><br />
      <input type="text" v-model="enteredemail" /><br />
  
      <label for="phone">Phonenumber:</label><br />
      <input type="number" v-model="enteredphone" /><br />
  
      <button @click="newFriend">Add Friend</button>
    </li>
  </template>
  <script>
  export default {
    emits: ["new-friend"],
    // props können als array angegeben werden
    // props: ['name','phoneNumber','emailAddress','isFavorite'],
  
    // props können als Objekte mit speziellen Eigenschaften angegeben werden
    props: {
  
      name: {
        type: String,
        required: true,
      },
      phoneNumber: {
        type: String,
        required: true,
      },
      emailAddress: {
        type: String,
        required: true,
        // Es kann auch ein validator angegeben werden
        // hier wird einfach überprüft, ob '1' oder '0' übergeben wurde
        validator: function(value) {
          return value=== '1' || value === '0';
        }
      },
    },
  
    // created()
    // wird aufgerufen nach der Erstellung der Komponente
    // Kann für Initalisierungen verwendet werden
    created() {
      this.isMyFavorite = this.isFavorite === "1";
      console.log("created : " + this.phoneNumber);
    },
  
    data() {
      return {
        enteredname: "",
        enteredemail: "",
        enteredphone: "",
      };
    },
    methods: {
      newFriend() {
        this.$emit("new-friend", this.enteredname, this.enteredemail, this.enteredphone);
      },
  
    },
  };
  </script>