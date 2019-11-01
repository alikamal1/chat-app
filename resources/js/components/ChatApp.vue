<template>
  <div class="chat-app">
    <Conversaction :contact="selectedContact" :messages="messages" @new="saveNewMessage" />
    <ContactsList :contacts="contacts" @selected="startConversionWith" />
  </div>
</template>

<script>
import Conversaction from "./Conversaction";
import ContactsList from "./ContactsList";
export default {
  props: {
    user: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      selectedContact: null,
      messages: [],
      contacts: []
    };
  },
  mounted() {
    Echo.private(`messages.${this.user.id}`).listen("NewMessage", e => {
      this.handleIncoming(e.message);
    });
    axios.get("/contacts").then(response => {
      this.contacts = response.data;
    });
  },
  methods: {
    startConversionWith(contact) {
      axios.get(`/conversation/${contact.id}`).then(response => {
        this.messages = response.data;
        this.selectedContact = contact;
      });
    },
    saveNewMessage(text) {
      this.messages.push(text);
    },
    handleIncoming(message) {
      if (this.selectedContact && message.from == this.selectedContact.id) {
        this.saveNewMessage(message);
        return;
      }
      alert(message.text);
    }
  },
  components: { Conversaction, ContactsList }
};
</script>

<style lang="scss" scoped>
.chat-app {
  display: flex;
}
</style>
