<template>
    <div>
        <form @submit.prevent="save">
            <div class="form-group">
                <label for="title">title</label>
                <input type="text" class="form-control" id="" placeholder="Title input" v-model="recipe.title">
            </div>
            <div class="form-group">
                <label for="description">Description</label>
                <input type="text" class="form-control" id="" placeholder="description input" v-model="recipe.description">
            </div>
            <div class="form-group">
                <label for="image">Image</label>
                <input type="text" class="form-control" id="" placeholder="image url input" v-model="recipe.image">
            </div>
            {{recipe}}
            <button class="btn btn-danger">Cancel</button>
            <button type="submit" class="btn btn-primary" >Save</button>
        </form>

    </div>
</template>

<script>
    export default {
        data (){
            return {
                recipe :{
                    id: '',
                    title:'',
                    description:'',
                    image:''
                }
            }
        },
        methods:{
            save(){
                this.recipe.id = Math.floor((Math.random() * 100) + 1);;
                this.$emit('formSaved', this.recipe)
            }
        }
    }
</script>

<style scoped>

</style>