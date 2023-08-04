<template>
    <div class="container">
        <h1>{{ page.pageTitle }}</h1>
        <p>{{ page.content }}</p>

        <div v-if="showProfile">
            <template v-if="userInfo[0].first_name && userInfo[0].last_name && userInfo[0].occupation">
                <label>{{ `Name: ${userInfo[0].first_name} ${userInfo[0].last_name}` }}</label><br>
                <label>{{ `Occupation: ${userInfo[0].occupation}` }}</label><br>
            </template>
            <template v-else>
                <p>Loading user profile...</p>
            </template>
        </div>

        <div v-if="showCredit">
            <label>{{ `Credit Score: ${userInfo.credit_score}` }}</label><br>
            
            <button
                type="button"
                class="btn btn-secondary"
                @click.prevent="fetchCredit()"
            >Get Score</button>
        </div>        
    </div>
</template>

<script lang="ts">
import axios from 'axios';
export default {
    props: ['page', 'userInfo' ,'currentUser', 'showProfile', 'showCredit'],
    data() {
        return { }
    },
    methods: {
        fetchCredit() {

        }
    }
}
</script>

<!-- Adding the 'scoped' attribute limits the scope of the defined styles to this component -->
<style scoped>

</style>