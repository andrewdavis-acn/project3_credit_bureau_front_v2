<template>
    <navbar
        :pages="pages"
        :activePages="activePage"
        :nav-link-click="(index:number) => {
            activePage = index;
            activePage == 1? showProfile = true: showProfile = false;
            activePage == 2? showCredit = true: showCredit = false;
        }"
    >
    </navbar>

    <page-viewer
        :page="pages[activePage]"
        :user-info="userInfo"
        :current-user="currentUser"
        :show-profile="showProfile"
        :show-credit="showCredit"
    ></page-viewer>
</template>

<script lang="ts">
import axios from 'axios';
import PageViewer from './PageViewer.vue'
import Navbar from './Navbar.vue'

export default {
    components: {
        PageViewer,
        Navbar
    },
    data() {
        return {
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
        async fetchData():Promise<void> {
            try {
                const response = await axios.get('http://localhost:3000/profile');
                // The 'data' being returned is an array
                // This version of the application doesn't implement user sessions or multiple users
                // Use the 0th user for now
                this.userInfo[0].first_name = response.data[0].first_name;
                this.userInfo[0].last_name = response.data[0].last_name;
                this.userInfo[0].occupation = response.data[0].occupation;
                this.loading = false;
            } catch (error) {
                console.error('Error fetching user profile:', error);
                this.loading = false;
            }
        }
    },
    created() {
        this.fetchData();
    }
}
</script>

<!-- Adding the 'scoped' attribute limits the scope of the defined styles to this component -->
<style scoped>

</style>