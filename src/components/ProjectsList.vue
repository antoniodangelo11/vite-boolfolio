<script>
    import axios from 'axios';
    import ProjectCard from './ProjectCard.vue';
    
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
            };
        },
        
        methods: {
            changePage(page) {
                this.currentPage = page;
                this.getProjects();
            },
            getProjects() {
                axios
                .get('http://localhost:8000/api/projects', {
                    params: {
                        page: this.currentPage,
                    },
                })
                .then(response => {
                    this.arrProjects = response.data.data;
                    this.nPages = response.data.last_page;
                });
            }
        },      

        created() {
            axios
            .get('http://localhost:8000/api/projects', {
                params: {
                    page: this.currentPage,
                }
            })
            .then(response=>{
                this.arrProjects = response.data.data;
                this.nPages = response.data.last_page;
            });
        },
    };
</script>

<template>
    <main>
        <div class="container">
            <h2 class="text-center">My Projects</h2>
            <ProjectCard 
                v-for="project in arrProjects" 
                :key="project.id" 
                :project="project"
            />
        </div>
    </main>

    <div class="container">
        <nav>
            <ul class="pagination">
                <li class="page-item disabled">
                    <a class="page-link">Previous</a>
                </li>

                <li
                    v-for="page in nPages"
                    :key="page"
                    class="page-item"
                    :class="{ active: page == currentPage }"
                >
                    <span class="page-link" @click="changePage(page)">
                        {{ page }}
                    </span>
                </li>

                <li class="page-item">
                    <a class="page-link" href="#">Next</a>
                </li>
            </ul>
        </nav>
    </div>
</template>

<style lang="scss" scoped>
    
</style>