<style scoped>

.addmargin {
    margin-top: 10px;
    margin-bottom: 10px;
}

.vue-logo-back {
    background-color: black;
}

</style>

<template>

<div class="home">
    <div class="vue-logo-back">
        <img src="../assets/logo.png" width="100px" height="100px">
    </div>
    <div class="card" v-if="customerDetails.id">
        <div class="card-header">
            Customer Details
        </div>
        <div class="card-body">
            <h5 class="card-title">{{customerDetails.first_name}}</h5>
            <p class="card-text">Name : {{customerDetails.last_name}}</p>
            <p class="card-text">Email : {{customerDetails.email}}</p>
            <a v-on:click="goToMainPage()" class="btn btn-primary"><span style="color:white">Go Back</span></a>
        </div>
    </div>


</div>

</template>

<script>

// @ is an alias to /src
import axios from 'axios'

export default {
    name: 'customerdetails',
    mounted() {
        axios({
            method: "GET",
            "url": "https://reqres.in/api/users/"+this.$route.params.id
        }).then(response => {
            this.customerDetails = response.data.data;
        }, error => {
            console.error(error);
        });
    },
    data() {
        return {
            customerDetails: {}
        }
    },
    methods: {
        goToMainPage: function() {
            this.$router.push("/customers");
        }
    }
}

</script>
