<template>
    <div>
        <base-header class=" pb-6 pt-5 pt-md-3 bg-gradient-success"></base-header>

        <b-container>
            <div class="text-right">
                <b-button type="submit" variant="primary" class="btn btn-primary mt-5" v-b-modal.add-org>Add Organization</b-button>
                
                <!-- Dialogbox_org_form -->
                
                <div class="mt-3"></div>

                <b-modal
                    id="add-org"
                    ref="modal"
                    title="Add Organization"
                    @show="resetModal"
                    @hidden="resetModal"
                    size="lg"
                    
                >
                    <form @submit.prevent="validate">
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': nameError }" id="name" placeholder="Organization name" v-model="name">
                            <div class="invalid-feedback" id="feedback-1" v-if="errors[0]">
                                {{ errors[0].message }}
                            </div>
                        </div>
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': emailError }" id="email" placeholder="Email" v-model="email">
                            <div class="invalid-feedback" id="feedback-2" v-if="errors[1]">
                                {{ errors[1].message }}
                            </div>
                        </div>
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': contactError }" id="contact" placeholder="Contact No" v-model="contact">
                            <div class="invalid-feedback" id="feedback-3" v-if="errors[2]">
                                {{ errors[2].message }}
                            </div>
                        </div>
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': anameError }" id="aname" placeholder="Admin name" v-model="aname">
                            <div class="invalid-feedback" id="feedback-4" v-if="errors[3]">
                                {{ errors[3].message }}
                            </div>
                        </div>
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': aemailError }" id="aemail" placeholder="Admin email" v-model="aemail">
                            <div class="invalid-feedback" id="feedback-5" v-if="errors[4]">
                                {{ errors[4].message }}
                            </div>
                        </div>
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': acontactError }" id="acontact" placeholder="Admin Contact No" v-model="acontact">
                            <div class="invalid-feedback" id="feedback-6" v-if="errors[5]">
                                {{ errors[5].message }}
                            </div>
                        </div>
                        
                        <div class="form-group">
                            <multiselect v-bind:class="{ 'is-invalid': statusError }" id="status" :multiple="true" v-model="status" :options="statusOptions"></multiselect>
                            <div class="invalid-feedback" v-if="errors[6]">
                                {{ errors[6].message }}
                            </div>
                        </div>

                        <!-- <button class="btn btn-primary" type="submit">Validate</button> -->
                    </form>
                    <template v-slot:modal-footer="{}">
                        <div @click="$refs.modal.hide()">
                            <button class="btn btn-primary" @click="resetModal">Close</button>
                        </div>
                        <div @click="addOrg">
                            <button class="btn btn-primary" type="submit" @click="validate">Add Organization</button>
                        </div>
                    </template>
                    
                </b-modal>

            </div>

            <!-- Edit Form -->
            <b-modal
                    id="edit-org"
                    ref="modal"
                    title="Edit Organization"
                    @show="resetModal"
                    @hidden="resetModal"
                    size="lg"
                    
                >
                    <form @submit.prevent="validate">
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': nameError }" id="name" placeholder="Organization name" v-model="name">
                            <div class="invalid-feedback" id="feedback-1" v-if="errors[0]">
                                {{ errors[0].message }}
                            </div>
                        </div>
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': emailError }" id="email" placeholder="Email" v-model="email">
                            <div class="invalid-feedback" id="feedback-2" v-if="errors[1]">
                                {{ errors[1].message }}
                            </div>
                        </div>
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': contactError }" id="contact" placeholder="Contact No" v-model="contact">
                            <div class="invalid-feedback" id="feedback-3" v-if="errors[2]">
                                {{ errors[2].message }}
                            </div>
                        </div>
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': anameError }" id="aname" placeholder="Admin name" v-model="aname">
                            <div class="invalid-feedback" id="feedback-4" v-if="errors[3]">
                                {{ errors[3].message }}
                            </div>
                        </div>
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': aemailError }" id="aemail" placeholder="Admin email" v-model="aemail">
                            <div class="invalid-feedback" id="feedback-5" v-if="errors[4]">
                                {{ errors[4].message }}
                            </div>
                        </div>
                        <div class="form-group">
                            <input type="text" class="form-control" v-bind:class="{ 'is-invalid': acontactError }" id="acontact" placeholder="Admin Contact No" v-model="acontact">
                            <div class="invalid-feedback" id="feedback-6" v-if="errors[5]">
                                {{ errors[5].message }}
                            </div>
                        </div>
                    
                        <div class="form-group">
                        <multiselect
                        v-bind:class="{ 'is-invalid': statusError }" id="status" :multiple="true" v-model="status" :options="statusOptions"></multiselect>
                            <div class="invalid-feedback" v-if="errors[6]">
                                {{ errors[6].message }}
                            </div>
                        </div>    
                        <!-- <button class="btn btn-primary" type="submit">Validate</button> -->
                    </form>
                    <template v-slot:modal-footer="{}">
                        <div @click="$refs.modal.hide()">
                            <button class="btn btn-primary" @click="resetModal">Close</button>
                        </div>
                        <div @click="updateOrg">
                            <button class="btn btn-primary" type="submit" @click="validate">Update</button>
                        </div>
                    </template>
                    
                </b-modal>
            

        <!-- Organization Cards -->
                <div v-if="items.length" :class="{ 'custom-margin': cardLengthIsThree }">
                    <b-row>
                        <b-col cols="12" sm="4" class="my-1" :key="index" v-for="(item, index) in paginatedItems">
                            <b-card
                            class=" mt-4" 
                            >
                            <b-card-title align='left' style="color:#7C8DA0" class="text-uppercase d-flex justify-content-between mt-1">
                                {{item.orgName}}
                                <!-- Dropdown option -->
                                <b-dropdown  variant="link" toggle-class="text-decoration-none" no-caret class="mt--3">
                                    <template #button-content>
                                        <i class="fa fa-ellipsis-v" aria-hidden="true"></i>
                                    </template>
                                    <b-dropdown-item-button @click="viewItem(item.oname, item.body)">View</b-dropdown-item-button>
                                    <div @click="editOrg(item)">
                                        <b-dropdown-item-button  v-b-modal.edit-org>Edit</b-dropdown-item-button>
                                    </div>
                                    <div variant="primary" @click="$bvToast.show('example-toast')">
                                        <b-dropdown-item-button @click="deleteCard(item)">Delete</b-dropdown-item-button>
                                    </div>
                                </b-dropdown>
                            </b-card-title>
                                <h3 class="card-text text-dark fw-bold">{{"Primary"}}</h3>
                                <h5 class="card-text text-dark fw-bold">Member Type:</h5>
                                <div class="lts">
                                <small class="card-text" >
                                    <!-- {{item.memberType && item.memberType.join(',')}} -->
                                    <ul>
                                        <li v-for="type in item.memberType" :key="type">{{ type }}</li>

                                    </ul>
                                </small>
                            </div>
                                <footer class="mb-2"  style="position: absolute; bottom: 0;">
                                    <small><cite title="Source Title" class="text-success">4.56%</cite> Since last month </small>
                                </footer>
                            </b-card>
                        </b-col>
                    </b-row>
                </div>

                <div class="text-center mt-8 mb-8" v-else> 
                    <b-icon icon="search" font-scale="10px"></b-icon>
                    <div class="text-muted text-center mt-2">NO ORGANIZATIONS FOUND</div>
                </div>   

        <!-- Pagination -->
                <div class="pagination-container">
                    <b-row  v-if="items.length > perPage">
                        <b-col class="my-3">
                            <b-pagination
                            @change="onPageChanged"
                            :total-rows="totalRows"
                            :per-page="perPage"
                            v-model="currentPage"
                            class="mb-7"
                            align="right"
                            />
                        </b-col>
                    </b-row>
                </div>
        </b-container>
    </div>

</template>

<script>
const items = [
    {
    id: 1,
    oname: "Hello",
    title: "Primary",
    body: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Amet minim mollit non deserunt ullamco est sit aliqua dolor do amet sint.",
    
  },
  {
    id: 2,
    oname: "Hello",
    title: "Secondary",
    body: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Amet minim mollit non deserunt ullamco est sit aliqua dolor do amet sint.",
    
  },
];

import BaseHeader from '../components/BaseHeader.vue'
import Multiselect from 'vue-multiselect'
import "vue-multiselect/dist/vue-multiselect.min.css"
import axios from 'axios';
export default {
  components: { BaseHeader, Multiselect },

  data() {
      return {

        // Validations
        name: '',
        email: '',
        contact: '',
        aname: '',
        aemail: '',
        acontact: '',
        nameError: false,
        emailError: false,
        contactError: false,
        anameError: false,
        aemailError: false,
        acontactError: false,
        status: [],
        statusOptions: ['Basic', 'Corporate', 'Partner', 'Sponsor'],
        statusError: false,
        errors: [],

        // Pagination
        items: items,
        paginatedItems: items,
        currentPage: 1,
        perPage: 6,
        totalRows: items.length
      }
    },

    mounted() {
        this.paginate(this.perPage, 0);
        
      },
    
    computed: {
        cardLengthIsThree() {
      return this.items.length <= 3 && this.currentPage === 1;
    },
    },

    created() {
        this.fetchData();
    },

    methods: {

        // Validations
       validate() {
            this.errors = [];

            // name validate
            this.nameError = this.validateName(this.name);
            if (this.nameError) {
                this.errors.push({
                'field': 'name',
                'message': 'Name must be between 5 to 20 characters long.'
                });
            }

            // email validate
            this.emailError = this.validateEmail(this.email);
            if (this.emailError) {
                this.emailError = true;
                this.errors.push({
                'field': 'email',
                'message': 'Please provide a valid email address.'
                }); 
            }

            // contact validate
            this.contactError = this.validatePhoneNumber(this.contact);
            if (this.contactError) {
                this.errors.push({
                'field': 'contact',
                'message': 'Please provide a valid number'
                });
            }

            // Admin name validate
            this.anameError = this.validateName(this.aname);
            if (this.anameError) {
                this.errors.push({
                'field': 'aname',
                'message': 'Name must be between 5 to 20 characters long.'
                });
            }

            // Admin email validate
            this.aemailError = this.validateEmail(this.aemail);
            if (this.aemailError) {
                this.errors.push({
                'field': 'aemail',
                'message': 'Please provide a valid email address.'
                });
            }

            // Admin contact validate
            this.acontactError = this.validatePhoneNumber(this.acontact);
            if (this.acontactError) {
                this.errors.push({
                'field': 'acontact',
                'message': 'Please provide a valid number'
                });
            }

            //
            if (!this.status.length) {
                this.statusError = true
                this.errors.push({
                'field': 'status',
                'message': 'Please select a status'
                })
            } else {
                this.statusError = false
            }
            },
            validateName(name) {
            return name.length < 5 || name.length > 20;
            },
            validateEmail(email) {
            var regex = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,4}$/;
            return !regex.test(email);
            },
            validatePhoneNumber(contact) {
            var regex = /^[0-9 .-]+$/;
            return contact.length !== 10 || !regex.test(contact);
            },
            

            //clear form
            resetModal() {
                this.name = '';
                this.email = '';
                this.contact = '';
                this.aname = '';
                this.aemail = '';
                this.acontact = '';
                this.status = [];
                this.nameError= false,
                this.emailError= false,
                this.contactError= false,
                this.anameError= false,
                this.aemailError= false,
                this.acontactError= false,
                this.statusError= false,
                this.errors = [];
            },

        // Pagination    
        paginate(page_size, page_number) {
            let itemsToParse = this.items;
            this.paginatedItems = itemsToParse.slice(
                page_number * page_size,
                (page_number + 1) * page_size
            );
            },
            onPageChanged(page) {
            this.paginate(this.perPage, page - 1);

        },

        //GET data from DB
        fetchData() {
            axios.get('http://localhost:6010/get')
            .then(response => {
                this.items = response.data.filter(item => item.orgActive === true);
                this.paginate(this.perPage, this.currentPage - 1);
                this.totalRows = this.items.length;
            })
            .catch(error => {
                console.error(error);
            })
        },

        //add cards
        addOrg(){
            
            this.validate();
            if(this.errors.length > 0) return;

           if( this.validate){
            axios.post('http://localhost:6010/post',{
                orgName: this.name,
                orgEmail: this.email,
                orgContactNo: this.contact,
                orgAdminName: this.aname,
                orgAdminEmail: this.aemail,
                orgAdminContactNo: this.acontact,
                memberType: this.status
            })
            .then(response => {

                if(response.data.message === 'User with this email already exists') {
                    this.$toast.error("User with this email already exists", {
                        position: "bottom-right",
                        timeout: 3000,
                        closeOnClick: true,
                        pauseOnFocusLoss: true,
                        pauseOnHover: true,
                        draggable: true,
                        draggablePercent: 0.6,
                        showCloseButtonOnHover: false,
                        hideProgressBar: false,
                        closeButton: false,
                        icon: true,
                        rtl: false
                    });
                } else {

                this.paginate(this.perPage, this.currentPage - 1);
                this.totalRows = this.items.length;
                this.$refs.modal.hide();

                //Alerts
                this.$toast.success("Added Successfully!", {
                    position: "bottom-right",
                    timeout: 3000,
                    closeOnClick: true,
                    pauseOnFocusLoss: true,
                    pauseOnHover: true,
                    draggable: true,
                    draggablePercent: 0.6,
                    showCloseButtonOnHover: false,
                    hideProgressBar: false,
                    closeButton: false,
                    icon: true,
                    rtl: false
                });
              }
            })
            .catch(error => {
                console.error(error);
                this.$toast.error("Error adding organization.", {
                    position: "bottom-right",
                    timeout: 3000,
                    closeOnClick: true,
                    pauseOnFocusLoss: true,
                    pauseOnHover: true,
                    draggable: true,
                    draggablePercent: 0.6,
                    showCloseButtonOnHover: false,
                    hideProgressBar: false,
                    closeButton: false,
                    icon: true,
                    rtl: false
                });
            })
           }
                // this.name= '',
                // this.email= '',
                // this.contact= '',
                // this.aname= '',
                // this.aemail= '',
                // this.acontact= '',
                // Close the modal
        },

        //Edit cards
        updateOrg() {
            this.validate;
            if(this.errors.length > 0) return;
            if( this.validate){
            axios.put(`http://localhost:6010/update?id=${this.id}`, {
                orgName: this.name,
                orgEmail: this.email,
                orgContactNo: this.contact,
                orgAdminName: this.aname,
                orgAdminEmail: this.aemail,
                orgAdminContactNo: this.acontact,
                memberType: this.status
            })
            .then(response => {
                this.paginate(this.perPage, this.currentPage - 1);
                this.totalRows = this.items.length;
                this.$refs.modal.hide();

                // Alerts
                this.$toast.success("Updated Successfully!", {
                    position: "bottom-right",
                    timeout: 3000,
                    closeOnClick: true,
                    pauseOnFocusLoss: true,
                    pauseOnHover: true,
                    draggable: true,
                    draggablePercent: 0.6,
                    showCloseButtonOnHover: false,
                    hideProgressBar: false,
                    closeButton: false,
                    icon: true,
                    rtl: false
                });
            })
            .catch(error => {
                console.error(error);
                this.$toast.error("Error updating organization.", {
                    position: "bottom-right",
                    timeout: 3000,
                    closeOnClick: true,
                    pauseOnFocusLoss: true,
                    pauseOnHover: true,
                    draggable: true,
                    draggablePercent: 0.6,
                    showCloseButtonOnHover: false,
                    hideProgressBar: false,
                    closeButton: false,
                    icon: true,
                    rtl: false
                });
            });
        }
        },

        //pre-populate the data
        editOrg(item){
            this.id = item._id;
            this.name = item.orgName;
            this.email = item.orgEmail;
            this.contact = item.orgContactNo;
            this.aname = item.orgAdminName;
            this.aemail = item.orgAdminEmail;
            this.acontact = item.orgAdminContactNo;
            this.status = item.memberType;
  
        },

        //to fetch the data from the database based on the id.
        // editOrg(item){
        //     axios.get(`http://localhost:6010/get/${item._id}`)
        //         .then(response => {
        //         this.name = response.data.orgName;
        //         this.email = response.data.orgEmail;
        //         this.contact = response.data.orgContactNo;
        //         this.aname = response.data.orgAdminName;
        //         this.aemail = response.data.orgAdminEmail;
        //         this.acontact = response.data.orgAdminContactNo;
        //         this.status = response.data.memberType;
        //         })
        //         .catch(error => {
        //         console.error(error);
        //         this.$toast.error("Error fetching organization data.", {
        //             position: "bottom-right",
        //             timeout: 3000,
        //             closeOnClick: true,
        //             pauseOnFocusLoss: true,
        //             pauseOnHover: true,
        //             draggable: true,
        //             draggablePercent: 0.6,
        //             showCloseButtonOnHover: false,
        //             hideProgressBar: false,
        //             closeButton: false,
        //             icon: true,
        //             rtl: false
        //         });
        //         });
        // },

        //delete cards
        deleteCard(item){
              axios.delete(`http://localhost:6010/delete?id=${item._id}`)
              //Alerts
            this.$toast.success("Deleted Successfully!", {
                    position: "bottom-right",
                    timeout: 3000,
                    closeOnClick: true,
                    pauseOnFocusLoss: true,
                    pauseOnHover: true,
                    draggable: true,
                    draggablePercent: 0.6,
                    showCloseButtonOnHover: false,
                    hideProgressBar: false,
                    closeButton: false,
                    icon: true,
                    rtl: false
                });

        },


        // deleteCard(item){
        //     const index = this.items.findIndex(item => item.id === id)
        //     this.items.splice(index, 1);
        //     this.paginate(this.perPage, this.currentPage - 1);
        //     this.totalRows = this.items.length;

        //     if (this.currentPage > 1 && this.paginatedItems.length === 0) {
        //         this.currentPage -= 1;
        //     }
        //     this.paginate(this.perPage, this.currentPage - 1);

        //     //Alerts
        //     this.$toast.success("Deleted Successfully!", {
        //             position: "bottom-right",
        //             timeout: 3000,
        //             closeOnClick: true,
        //             pauseOnFocusLoss: true,
        //             pauseOnHover: true,
        //             draggable: true,
        //             draggablePercent: 0.6,
        //             showCloseButtonOnHover: false,
        //             hideProgressBar: false,
        //             closeButton: false,
        //             icon: true,
        //             rtl: false
        //         });
        // },

        //Push the data through router
        viewItem(name, body) {
            this.$router.push({ name: 'view', params: { name, body } });
        }

    }
    
}
</script>

<style>
.dropdown-toggle::after {
  display: none;
}

.custom-margin {
  margin-bottom: 170px;
}

.card {
  height: 254px;
}


</style>