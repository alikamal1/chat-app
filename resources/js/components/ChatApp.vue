<template>
    <div class="chat-app">
        <Conversaction :contact="selectedContact" :messages="messages" />
        <ContactsList :contacts="contacts" @selected="startConversionWith"/>
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
        methods: {
            startConversionWith(contact) {
                axios.get(`/conversation/${contact.id}`).then((response) => {
                    this.messages = response.data;
                    this.selectedContact = contact;
                });
            }
        },
        components: {Conversaction, ContactsList}
    }
</script>

<style lang="scss" scoped>
.chat-app {
    display: flex,

}

</style>
