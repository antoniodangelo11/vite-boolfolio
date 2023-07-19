<script>
    import axios from 'axios';
    import ProjectCard from './ProjectCard.vue';
    import { store } from '../store';

    export default {
        components: {
            ProjectCard,
        },
        
        data() {
            return {
                arrProjects: [],
                currentPage: 1,
                nPages: 0,
                activePage: 1,
                store,
            };
        },
        
        methods: {
            toPrevPage() {
                this.currentPage != 1 ? this.currentPage-- : null;
            },

            toNextPage() {
                this.currentPage != this.nPages ? this.currentPage++ : null;
            },

            getProjects() {
                this.loader = true;
                axios
                .get(this.store.baseUrl + 'api/projects', {
                    params: {
                        page: this.currentPage,
                        q: new URLSearchParams(window.location.search).get('q'),
                    },
                })
                .then(response => {
                    this.arrProjects = response.data.results.data;
                    this.nPages = response.data.results.last_page;
                    this.loader = false;
                });
            }
        },      

        created() {
            this.getProjects();
        },

        watch: {
            currentPage() {
                this.getProjects();
            }
        }
    };
</script>

<template>
    <main>
        <div class="container">
            <div v-if="!loader" class="row row-cols-1 row-cols-sm-2 row-cols-md-3 my-5">
                <div class="col" v-for="project in arrProjects" :key="project.id">
                    <ProjectCard :objProject="project"/>
                </div>
            </div>
            <div v-else>
                <h2>PLEASE WAIT!</h2>
            </div>
        </div>
    </main>
    
    <div class="container mt-2">
        <nav>
            <ul class="pagination">
                <li class="page-item" :class="{ disabled: currentPage == 1 }">
                    <a class="page-link" href="#" @click="toPrevPage">Previous</a>
                </li>

                <li
                    v-for="page in nPages"
                    :key="page"
                    class="page-item"
                    :class="{ active: page == currentPage }"
                >
                    <a class="page-link" href="#" @click="currentPage = page">
                        {{ page }}
                    </a>
                </li>

                <li class="page-item" :class="{ disabled: currentPage == nPages }">
                    <a class="page-link" href="#" @click="toNextPage()">Next</a>
                </li>
            </ul>
        </nav>
    </div>
</template>

<style lang="scss" scoped></style>