<template>
    <div class="container mt-3">
        <div class="row">
            <div class="col">
                <p class="h3 text-success fw-bold">Edit Contact</p>

            </div>
        </div>
    </div>

    <div class="container mt-3">
        <div class="row">
            <div class="col-md-4">
                <form @submit.prevent="updateSubmit()">
                    <div class="mb-2">
                        <input required v-model="contact.name" type="text" class="form-control" placeholder="Name"
                            name="" id="">
                    </div>
                    <div class="mb-2">
                        <input required v-model="contact.photo" type="text" class="form-control" placeholder="Photo URL"
                            name="" id="">
                    </div>
                    <div class="mb-2">
                        <input required v-model="contact.email" type="email" class="form-control" placeholder="Email"
                            name="" id="">
                    </div>
                    <div class="mb-2">
                        <input required type="number" v-model="contact.mobile" class="form-control" placeholder="Mobile"
                            name="" id="">
                    </div>

                    <div class="mb-2">
                        <input required type="text" v-model="contact.company" class="form-control" placeholder="Company"
                            name="" id="">
                    </div>
                    <div class="mb-2">
                        <input required type="text" v-model="contact.title" class="form-control" placeholder="Title"
                            name="" id="">
                    </div>
                    <div class="mb-2">
                        <select required v-model="contact.groupId" name="" class="form-control" id=""
                            v-if="groups.length>0">
                            <option value="">Select Group</option>
                            <option :value="group.id" v-for="group of groups" :key="group.id">{{group.name}}</option>
                        </select>
                    </div>

                    <div class="d-flex ">
                        <div class="mb-2 me-3">
                            <input type="submit" class="btn btn-success" value="Update">
                        </div>
                        <div class="mb-2">
                            <input type="submit" class="btn btn-success" value="Clear">
                        </div>
                    </div>

                </form>
            </div>
            <div class="col-md-4">
                <img :src="contact.photo" alt="" class="contact-img">
            </div>
        </div>

    </div>

</template>
  
<script>
import { ContactService } from '@/services/ContactService';

export default {
    name: 'EditContact',
    data: function () {
        return {
            contactId: this.$route.params.contactId,
            loading: false,
            contact: {
                name: '',
                photo: '',
                email: '',
                mobile: '',
                company: '',
                title: '',
                groupId: ''

            },
            errorMessage: null,
            groups: []
        }
    },
    created: async function () {
        try {
            this.loading = true;
            let response = await ContactService.getContact(this.contactId);
            let groupResponse = await ContactService.getAllGroups();

            this.contact = response.data;
            this.groups = groupResponse.data;
            this.loading = false;
        }
        catch (error) {
            this.errorMessage = error;
            this.loading = false;

        }

    },
    methods: {
        updateSubmit: async function () {
            try {
                let response = await ContactService.updateContact(this.contact, this.contactId);
                if (response) {
                    return this.$router.push('/');

                }
                else {
                    return this.$router.push(`/contacts/edit/${this.contactId}`);

                }
            }
            catch (error) {
                console.log(error);

            }

        }
    }
}
</script>
  
<style>

</style>
  