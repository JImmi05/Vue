<template>
  <section>
    <header>
      <h1>Liste mit vfor</h1>
    </header>
    <ul>
      <new-friend @new-friend="newFriend"></new-friend>
      <button @click="loadContacts">Load contacts</button>
      <friend-contact
        v-for="friend in friends"
        :key="friend.id"
        :id="friend.id"
        :name="friend.name"
        :phoneNumber="friend.phone"
        :emailAddress="friend.email"
        :isFavorite="friend.isFavorite"
        @toggle-favorite="toggleFavorite"
        @delete-friend="deleteFriend"
      ></friend-contact>
    </ul>
  </section>
</template>

// ***************************************************************************
// Aufgaben: 1. toggleFavorite als Event in FriendContact einbauen // 2.
deleteContact in FriendContact einbauen 3. Übung für Schüler: Eigene Komponente
NewFriend.vue erstellen //
***************************************************************************
<script>
import FriendContact from "./components/FriendContact.vue";
import NewFriend from "./components/NewFriend.vue";
export default {
  components: {
    FriendContact,
    NewFriend,
  },
  data() {
    return {
      friends: [],
    };
  },

  methods: {
    /* toggleFavorite(friendId) {
      console.log("toggle-favorite", friendId);
      const identifiedFriend = this.friends.find(
        (friend) => friend.id === friendId
      );

      if (identifiedFriend !== undefined) {
        identifiedFriend.isFavorite = !identifiedFriend.isFavorite;
      }
    },
    deleteFriend(deleteId) {
      console.log("delete-friend", deleteId);
      this.friends = this.friends.filter((friends) => friends.id !== deleteId);
    },*/
    newFriend(enteredname, enteredemail, enteredphone) {
      let fakeID = new Date().toISOString();

      fetch(
        "https://vue-test-21ba0-default-rtdb.europe-west1.firebasedatabase.app/contacts.json",
        {
          method: "POST",
          headers: {
            "content-Type": "application/json",
          },
          body: JSON.stringify({
            id: fakeID,
            name: enteredname,
            email: enteredemail,
            phone: enteredphone,
          }),
        }
      ).then((response) => {
        console.log(response);
      });
      /* console.log("new-friend", enteredname, enteredemail, enteredphone);
      let friend = {
        name: enteredname,
        email: enteredemail,
        phone: enteredphone,  
      };
      this.friends.push(friend) */
    },
    loadContacts(){
      fetch("https://vue-test-21ba0-default-rtdb.europe-west1.firebasedatabase.app/contacts.json"
      ).then((response) => {
        return response.json();
      })
      .then((data) => {
        // Speichere Daten in einem temorären Feld
        const results = [];
        for (const id in data) {
          results.push ({
            id: id,
            name: data[id].name,
            phone: data[id].phone,
            email: data[id].email
          });
        }
        // ab hier stehen alle Daten im Array results
        this.friends = results;
      })
    }

  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: "Jost", sans-serif;
}
body {
  margin: 0;
}
header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: #58004d;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}
#app ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
#app li,
form {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 1rem auto;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}
#app h2 {
  font-size: 2rem;
  border-bottom: 4px solid #ccc;
  color: #58004d;
  margin: 0 0 1rem 0;
}
#app button {
  font: inherit;
  cursor: pointer;
  border: 1px solid #ff0077;
  background-color: #ff0077;
  color: white;
  padding: 0.05rem 1rem;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
}
#app button:hover,
#app button:active {
  background-color: #ec3169;
  border-color: #ec3169;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}

#app input {
  font: inherit;
  padding: 0.15rem;
}
#app label {
  font-weight: bold;
  margin-right: 1rem;
  width: 7rem;
  display: inline-block;
}
#app form div {
  margin: 1rem 0;
}
</style>