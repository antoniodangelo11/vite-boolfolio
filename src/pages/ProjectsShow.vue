<script>
import axios from "axios";
import { store } from "../store";
import { DateTime } from "luxon";
import { router } from "../router";
import App404 from "./App404.vue";

export default {
    components: { App404 },
    
    data() {
        return {
            store,
            DateTime,
            is404: false,
            singleProject: {},
        };
    },
    created() {
        // fai la richiesta axios
        axios
            .get(this.store.baseUrl + "api/projects/" + this.$route.params.slug)
            .then((response) => {
                if (response.data.success) {
                    this.singleProject = response.data.results;
                } else {
                    // this.$router.push({ name: "page404" });
                    this.is404 = true;
                }
            });
    },
};
</script>

<template>
    <App404 v-if="is404" />
    <template v-else-if="singleProject">
        <h2>{{ singleProject.title }}</h2>
        <h3>Last update: {{ this.DateTime.now().toFormat("dd-MM-yyyy") }}</h3>
        <div class="card h-100">
            <img 
                class="card-img-top h-100" 
                :src="this.store.baseUrl + 'storage/' + singleProject.image" 
                :alt="singleProject.id" 
            />
        </div>
    </template>
</template>

<style lang="scss" scoped></style>