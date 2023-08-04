<template>
    <div class="container">
        <h1>{{ page.pageTitle }}</h1>
        <p>{{ page.content }}</p>
        <label>{{ userData }}</label>
        <br>
        <button
            type="button"
            class="btn btn-secondary"
            @click.prevent="fetchData()"
        >Get Data</button>
        
    </div>
</template>

<script lang="ts">
import axios from 'axios';
export default {
    props: ['page'],
    data() {
        return {
            loading: true,
            userData: []
        }
    },
    methods: {
        async fetchData():Promise<void> {
            try {
                const response = await axios.get('http://localhost:3000/profile');
                this.userData = response.data;
                this.loading = false;
            } catch (error) {
                console.error('Error fetching user profile:', error);
                this.loading = false;
            }
        }
    }
}
</script>

<!-- Adding the 'scoped' attribute limits the scope of the defined styles to this component -->
<style scoped>

</style>