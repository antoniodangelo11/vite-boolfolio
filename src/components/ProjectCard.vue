<script>
    export default {
        props: {
            ObjCard: Object,
        }
    };
</script>

<template>
    <div 
        v-for="card in this.ObjCard" 
        :key="card.id" 
        class="card h-100 card_pro"
    >
        <img :src="'http://localhost:8000/storage/' + card.image" class="card-img-top" :alt="id">
        <div class="card-body">
            <h5 class="card-title">{{ card.title }}</h5>
            <p class="card-text">{{ card.description }}</p>
        </div>
        <ul class="list-group list-group-flush">
            <li class="list-group-item">Author: {{ card.author }}</li>
            <li class="list-group-item">Creation Date: {{ card.creation_date }}</li>
            <li class="list-group-item">Last Update: {{ card.last_update }}</li>
            <li class="list-group-item">Collaborators: {{ card.collaborators }}</li>
            <li class="list-group-item">Technologies: {{ card.technologies[0].name }}</li>
            <li class="list-group-item">Type: {{ card.type_id }}</li>
        </ul>
        <div class="card-body">
            <a :href="card.link_github" class="card-link">Link Github</a>
        </div>
    </div>
</template>

<style lang="scss" scoped>
</style>