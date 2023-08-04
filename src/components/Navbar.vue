<template>
    <nav
        :class="[`navbar-${theme}`, `bg-${theme}`, 'navbar', 'navbar-expand-lg']"
    >
        <div class="container-fluid">
            <a class="navbar-brand" href="#" >My Vue</a>
            <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                <li v-for="(page, index) in pages" class="nav-item" :key="index">
                    <a
                        class="nav-link"
                        :class="{active: activePage == index}"
                        aria-current="page"
                        :href="page.link.url"
                        :title="`This link goes to the ${page.link.text} page`"
                        @click.prevent="navLinkClick(index)"
                        >{{ page.link.text }}
                    </a>
                </li>
            </ul>
            <form class="d-flex">
                <button
                    class="btn btn-primary"
                    @click.prevent="changeTheme()"
                >Toggle Navbar</button>
            </form>
        </div>
    </nav>
</template>

<script lang="ts">
export default {
    props: ['pages','activePage', 'navLinkClick', 'showButton'],
    data() {
        return {
            theme: 'light' as string
        }
    },
    methods: {
        changeTheme() {
            let theme:string = 'light';

            if (this.theme == 'light') {
                theme = 'dark';
            }
            
            this.theme = theme;
        }
    }
}
</script>

<!-- Adding the 'scoped' attribute limits the scope of the defined styles to this component -->
<style scoped>

</style>