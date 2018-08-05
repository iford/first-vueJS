<template>
    <div>
<div class="card" style="width: 180px;">
  <img class="card-img-top" :src="recipe.image" alt="Card image cap">
  <div class="card-body">
    <h5 class="card-title">{{recipe.title}}</h5>
    <p class="card-text">{{recipe.description}}</p>
    <button type="button" @click="sendDelete">Delete</button>
  </div>

</div>

    </div>
</template>

<script>
    export default {
        props:{
            recipe:{
                type: Object,
                require: true
            }
        },
        methods: {
            sendDelete () {
                this.$emit('cardDelete', this.recipe.id)
            }
        }
    }
</script>

<style scoped>

</style>