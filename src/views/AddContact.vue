<template>
    <div class="container mt-3">
        <div class="row">
            <div class="col">
                <p class="h3 text-success fw-bold">Add Contact</p>

            </div>
        </div>
    </div>
    <div class="container mt-3">
        <div class="row">
            <div class="col-md-4">
                <form>
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
                        <input required v-model="contact.mobile" type="number" class="form-control" placeholder="Mobile"
                            name="" id="">
                    </div>

                    <div class="mb-2">
                        <input required v-model="contact.company" type="text" class="form-control" placeholder="Company"
                            name="" id="">
                    </div>
                    <div class="mb-2">
                        <input required v-model="contact.title" type="text" class="form-control" placeholder="Title"
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
                            <input @click.prevent="submitCreate()" type="submit" class="btn btn-success" value="Create">
                        </div>
                        <div class="mb-2">
                            <input type="submit" class="btn btn-success" @click="resetForm()" value="Clear">
                        </div>
                    </div>

                </form>
            </div>
            <div class="col-md-4">
                <img :src="contact.photo" alt="" class="contact-img">
            </div>
            <div class="row mt-3">
                <div class="col">
                    <router-link to="/" class="btn btn-success"> <i class="fa fa-arrow-alt-circle-left"></i> Go Back
                    </router-link>
                </div>
            </div>
        </div>

    </div>


</template>
  
<script>
import { ContactService } from '@/services/ContactService';

export default {
    name: 'AddContact',
    data: function () {
        return {
            contact: {
                name: '',
                photo: '',
                email: '',
                mobile: '',
                company: '',
                title: '',
                groupId: ''

            },
            groups: []
        }
    },
    created: async function () {
        try {
            let response = await ContactService.getAllGroups();
            this.groups = response.data;

        }
        catch (error) {
            console.log(error);

        }

    },
    methods: {
        submitCreate: async function () {
            try {
                let response = await ContactService.createContact(this.contact);
                if (response) {
                    return this.$router.push('/');

                }
                else {
                    return this.$router.push('/contacts/add')

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
  