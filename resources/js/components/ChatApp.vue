<template>
    <div class="chat-app">
        <Conversaction :contact="selectedContact" :messages="messages" />
        <ContactsList :contacts="contacts" />
    </div>
</template>

<script>
    import Conversaction from './Conversaction';
    import ContactsList from './ContactsList';
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
            }
        },
        mounted() {
            axios.get('/contacts').then((response) => {
                this.contacts = response.data;
            });
        },
        components: {Conversaction, ContactsList}
    }
</script>
