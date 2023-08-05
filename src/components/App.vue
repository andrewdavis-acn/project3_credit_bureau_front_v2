<template>
    <!--
        Pass the parent's state variables into the children that share/use them
        I.e :pages, :page, :user-info, :show-profile, :show-credit, ...
    -->
    <navbar
        :pages="pages"
        :activePages="activePage"
        @nav-link-click="navLinkClick"
        @toggle-user="fetchData"
    >
    </navbar>

    <!--
        Pass the parent's state variables into the children that share/use them
        I.e :pages, :page, :user-info, :show-profile, :show-credit, ...
    -->
    <page-viewer
        :page="pages[activePage]"
        :user-info="userInfo"
        :current-user="currentUser"
        :show-profile="showProfile"
        :show-credit="showCredit"
    ></page-viewer>
</template>

<script lang="ts">
// Pull/import in the required modules/libraries
import axios from 'axios';
// Pull/import in the child components
import PageViewer from './PageViewer.vue'
import Navbar from './Navbar.vue'

export default {
    components: {
        PageViewer,
        Navbar
    },
    data() {
        return {
            // All of the parent's state that is used in the parent and/or passed/used in the chitlin components is here in the data() option
            // Any changes to these states within the chitlins need to be emitted/called from them
            // Those changes/functions are defined here though, either in the methods option below or above in an {expression} within the chitlin component
            activePage: 0,
            currentUser: 0,
            showProfile: false,
            showCredit: false,
            loading: true,
            pages: [
                {
                    link: {text: 'Home', url: 'index.html'},
                    pageTitle:'Home Page',
                    content:'This is the home content'
                },
                {
                    link: {text: 'Profile', url: 'profile.html'},
                    pageTitle:'Profile Page',
                    content:'This is the profile content'
                },
                {
                    link: {text: 'Credit', url: 'credit.html'},
                    pageTitle:'Credit Page',
                    content:'This is the credit content'
                }
            ],
            userInfo: [
                {
                    first_name: "",
                    last_name: "",
                    occupation: "",
                    credit_score: ""
                }
            ]
        };
    },
    methods: {
        // Function to make an API call to the backend server for the current user information
        async fetchData():Promise<void> {
            try {
                const response = await axios.get('http://localhost:3000/profile');
                // The 'data' being returned is an array
                // This version of the application doesn't implement user sessions or multiple users
                // Use the 0th user for now
                this.userInfo[this.currentUser].first_name = response.data[0].first_name;
                this.userInfo[this.currentUser].last_name = response.data[0].last_name;
                this.userInfo[this.currentUser].occupation = response.data[0].occupation;
                this.loading = false;
            } catch (error) {
                console.error('Error fetching user profile:', error);
                this.loading = false;
            }
        },
        // CToP Methods
        navLinkClick(index:number):void {
            this.activePage = index;
            this.activePage == 1? this.showProfile = true: this.showProfile = false;
            this.activePage == 2? this.showCredit = true: this.showCredit = false;
        }
    },
    // The created() option is often used to get data to load on the page initially
    created() {
        this.fetchData();
    }
}
</script>

<!-- Adding the 'scoped' attribute limits the scope of the defined styles to this component -->
<style scoped>

</style>