<template>
<div style="margin-top: 20px">
      <form @submit="onSubmit" class="formgroup-inline">
    <div class="field">
        <label for="name" class="p-sr-only">Name</label>
        <InputText v-model="name" id="name" type="text"  placeholder="Name"/>
    </div>
    <div class="field">
        <label for="age" class="p-sr-only">Age</label>
        <InputText v-model="age" id="age" type="number"  placeholder="Age"/>
    </div>
    <div class="field">
        <label for="URL" class="p-sr-only">URL</label>
        <InputText v-model="url" id="url" type="text"  placeholder="Image URL"/>
    </div>
    <Button type="submit" label="Save"/>
</form>
</div>
</template>

<script>
export default {
    name: 'AddPet',
    methods: {
        onSubmit(e){
            e.preventDefault();
            const newPet = {
                id: Math.random(),
                name: this.name,
                age: this.age,
                url: this.url,
                favorite: false
            }
            this.$emit('add-pet', newPet)
            this.name = '',
            this.age = '',
            this.url = ''
            
        }
    },
    data() {
        return {
            name: "",
            age: '',
            url: '',
        }
    }
}
</script>

<style>

</style>