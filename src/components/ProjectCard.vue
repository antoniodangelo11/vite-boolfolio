<script>
    export default {
        props: {
            project: {
                type: Object,
                required: true,
            }
        }
    };
</script>

<template>
    <div class="card h-100">
        <img :src="'http://localhost:8000/storage/' + project.image" class="card-img-top w-100" :alt="id">
        <div class="card-body">
            <h5 class="card-title">{{ project.title }}</h5>
            <p class="card-text">{{ project.description }}</p>
        </div>
        <ul class="list-group list-group-flush">
            <li class="list-group-item">Author: {{ project.author }}</li>
            <li class="list-group-item">Creation Date: {{ project.creation_date }}</li>
            <li class="list-group-item">Last Update: {{ project.last_update }}</li>
            <li class="list-group-item">Collaborators: {{ project.collaborators }}</li>
            <li class="list-group-item">Technologies:
                <span v-for="technology in project.technologies" :key="technology.name">
                    {{ technology.name }},
                </span>
            </li>
            <li class="list-group-item">Type: {{ project.type.name }}</li>
        </ul>
        <div class="card-body">
            <a :href="project.link_github" class="card-link">Link Github</a>
        </div>
    </div>
</template>

<style lang="scss" scoped>
</style>