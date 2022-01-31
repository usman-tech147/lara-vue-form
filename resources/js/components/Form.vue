<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header bg-dark text-white">Form Component</div>
                    <div class="card-body">
                        <form class="row g-3" @submit="addUser" novalidate>
                            <div class="col-md-12" v-if="errors.length">
                                <div class="alert alert-danger pb-0" role="alert">
                                    <ul>
                                        <li v-for="error in errors"> {{error}} </li>
                                    </ul>
                                </div>
                            </div>
                            <div class="col-md-6">
                                <label for="name" class="form-label">Name</label>
                                <input type="text" class="form-control" id="name" name="name" v-model="name">
                            </div>
                            <div class="col-md-6">
                                <label for="email" class="form-label">Email</label>
                                <input type="email" class="form-control" id="email" name="email" v-model="email">
                            </div>
                            <div class="col-md-12">
                                <button class="btn btn-success" v-on:click="addContact"> + Add Contact </button>
                            </div>
                            <div class="col-md-12" v-for="(contact, counter) in contacts" :key="counter">
                                <div class="row">
                                    <div class="col-md-6">
                                        <label for="contact" class="form-label">{{counter+1}}: Contact</label>
                                        <input type="text" class="form-control" id="contact" v-model="contact.phoneNumber" name="contactList[]">
                                    </div>
                                    <div class="col-md-6">
                                        <button class="btn btn-danger" v-on:click="removeContact(counter, $event)" style="margin-top: 29px"> Remove </button>
                                    </div>
                                </div>
                            </div>
                            <div class="col-12">
                                <button type="submit" class="btn btn-primary">Save</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data(){
            return {
                email:null,
                name:null,
                contacts: [],
                contactsCounter:0,
                errors:[],
            }
        },
        renderTracked({ key, target, type }){
            console.log({ key, target, type })
        },
        methods : {
            addContact(e) {
                e.preventDefault();
                this.contacts.push({
                    phoneNumber: ''
                });
            },
            removeContact(counter, e) {
                e.preventDefault();
                this.contacts.splice(counter,1)
            },
            addUser(e){
                e.preventDefault();
                this.errors = [];
                this.contactsCounter = 0;
                if(!this.name)
                {
                    this.errors.push('Please enter name!')
                }
                if(!this.email)
                {
                    this.errors.push('Please enter email!')
                }

                for(let i=0; i<this.contacts.length; i++)
                {
                    if(!this.contacts[i].phoneNumber.length)
                    {
                        this.contactsCounter++;
                    }
                }
                if(this.contactsCounter)
                {
                    this.errors.push('Please enter all contacts field')
                }
                if(this.name && this.email && this.contactsCounter === 0)
                {
                    alert("ready to submit")
                }
            }
        },
        // beforeMount() {
        //     console.log("before mount hook called")
        // },
        // mounted() {
        //     console.log("created hook called")
        // },
        // beforeCreate() {
        //     console.log("before create hook called")
        // },
        // created() {
        //     console.log("created hook called")
        // },
        // beforeUpdate() {
        //     console.log("before update hook called")
        // },
        // updated() {
        //     console.log("updated hook called")
        // },
        // beforeDestroy() {
        //     console.log("before destroy hook called")
        // },
        // destroyed() {
        //     console.log("destroyed hook called")
        // },

    }
</script>
