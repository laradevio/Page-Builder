<template>
    <div class="user-profile" v-if="isUserLoggedIn">

        <main-nav></main-nav>

        <section class="user-data">
            <div class="container">
                <user-details :user="loggedInUser"></user-details>
            </div>
            <router-link to="/profile/edit"> Edit Profile </router-link>
        </section>

        <section class="user-sites">
            <div class="container">
                <site-list :addSite="true" :sites="sites" @on-delete="loadUserSites"></site-list>
            </div>
        </section>

        <main-footer></main-footer>

    </div>
</template>

<script>
import MainNav from '@/components/MainNav.vue';
import UserDetails from '@/components/UserDetails.vue';
import SiteList from '@/components/SiteList.vue';
import MainFooter from '@/components/MainFooter.vue';

export default {
    name: 'user-profile',
    components: { MainNav, SiteList, UserDetails, MainFooter },
    data() {
        return {
            sites: null
        };
    },
    computed: {
        loggedInUser() {
            return this.$store.getters.loggedInUser;
        },
        isUserLoggedIn() {
            return this.$store.getters.isUserLoggedIn;
        },
        sitesToDisplay() {
            return this.$store.getters.sitesToDisplay;
        }
    },
    watch: {
        'loggedInUser': {
            immediate: true,
            handler() {
                if (this.isUserLoggedIn) this.loadUserSites();
                else this.$router.push('/');
            }
        }
    },
    methods:{
        loadUserSites() {
            this.$store.dispatch({ type: 'loadSitesByUserName', userName: this.loggedInUser.userName })
                .then(sites => this.sites = sites );
        }
    }
};
</script>

<style scoped lang="scss">
section {
    padding: 20px 0;

    &.user-data {
        background-color: #eee;
        text-align: center;
    }
}
</style>
