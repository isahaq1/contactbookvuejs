<template>

    <div class="container">
        <h2>Contact List</h2>
        <table class="table table-bordered">
            <thead>
                <tr>
                    <th class="text-center">Name</th>
                    <th  class="text-center">Phone</th>
                    <th  class="text-center">Company</th>
                    <th  class="text-center">Address</th>
                    <th  class="text-center">Created At</th>
                    <th  class="text-center">Updated At</th>
                    <th  class="text-center">Action</th>

                </tr>
            </thead>
            <tbody v-bind:key="contact.id" v-for="contact in contacts">
<ContactItem v-bind:contact="contact" v-on:del-contact-item="delContactMethod" v-on:edit-contact-item="editContactMethod" />
            </tbody>
             <tbody v-if="!contacts.length">
            <p>No Contacts to Read!!</p>
        </tbody>
        </table>
        
       
    </div>
</template>

<script>
    import ContactItem from "./ContactItem";
    export default {
        name: "Contacts",
        props: ["contacts"],
        components: {
            ContactItem
        },
        methods: {
            delContactMethod(id){
                //send to parent
                this.$emit('del-contact-event', id);
            },
            editContactMethod(id){
                //send to parent (App.vue)
                this.$emit('edit-contact-event', id)
            }
        }
    }
</script>

<style scoped>

</style>