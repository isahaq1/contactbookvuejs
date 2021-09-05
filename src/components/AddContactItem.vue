<template>
    <div>
    <form @submit="addContact">
  <div class="form-group row">
    <label for="title" class="col-sm-2 col-form-label">Name</label>
    <div class="col-sm-4">
       <input type="text" name="title" v-model="title" placeholder="Name" class="form-control">
    </div>
  </div>
  <div class="form-group row">
    <label for="phone" class="col-sm-2 col-form-label">Phone</label>
    <div class="col-sm-4">
      <input type="text" name="phone" v-model="phone" placeholder="Phone" class="form-control">
    </div>
  </div>
  <div class="form-group row">
    <label for="company" class="col-sm-2 col-form-label">Company</label>
    <div class="col-sm-4">
      <input type="text" name="company" v-model="company" placeholder="Company" class="form-control">
    </div>
  </div>
  <div class="form-group row">
    <label for="address" class="col-sm-2 col-form-label">Address</label>
    <div class="col-sm-4">
     <input type="text" name="address" v-model="address" placeholder="address"  class="form-control">
    </div>
  </div>
   <div class="form-group row">
       <label for="submintf" class="col-sm-2 col-form-label"></label>
       <div class="col-sm-4">
            <button type="submit" class="btn btn-success form-control">Save</button>
       </div>
   </div>
</form>
    </div>
</template>

<script>
    export default {
        name: "AddContactItem",
        props: ['editContact'],
        data () {
            return {
                title: '',
                 phone: '',
                company: '',
                 address: '',
                id: '',
                edit: false
            }
        },
        methods: {
            addContact(e){
                e.preventDefault();
                if (this.edit === false){
                   // add contact
                    const newContact = {
                        title: this.title,
                        phone: this.phone,
                        company: this.company,
                        address: this.address,
                        created_at: new Date(),
                        id: Math.floor(Math.random() * 100)
                    };
                    if (newContact.title !== ''){
                        this.$emit('add-contact-event', newContact);
                    }
                    this.title = ''
                }else{
                    //edit contact
                    const contactItem = {
                        title: this.title,
                        phone: this.phone,
                        company: this.company,
                        address: this.address,
                        created_at: new Date(),
                        updated_at:'',
                        id: this.id
                    };
                    //send to parent (App.vue)
                    this.$emit('edit-contact-event', contactItem);
                    // clear input field
                         this.title = '';
                         this.phone = '';
                         this.company= '';
                         this.address= '';
                         this.created_at= '';
                         this.updated_at = '';
                         this.edit = false;
                }
            }
        },
        watch: {
            editContact: {
                handler() {
                    this.title = this.editContact.title;
                    this.phone = this.editContact.phone;
                    this.company = this.editContact.company;
                    this.address = this.editContact.address;
                    this.id = this.editContact.id;
                    this.id = this.editContact.id;
                    this.updated_at = new Date();
                    this.edit = true
                },
                deep: true
            },
            title:{
                handler(){
                    if(this.title === ''){
                        this.edit = false;
                    }
                }
            }
        }
    }
</script>

<style scoped>

</style>