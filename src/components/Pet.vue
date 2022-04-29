<template>
    <div class="pet">
         <Card>
            <template #header>
                <img 
                    :src="pet.url" alt="Pet"
                />
            </template>
            <template #title>
                {{ pet.name }}
            </template>
            <template #subtitle>
                Age: {{ pet.age }}
            </template>
            
            <template #footer>
                
                <Button 
                    @click="onRemove(pet.id)"
                    icon="pi pi-times" 
                    label="Remove" 
                    class="p-button-danger" 
                    style="margin-right: 4em" 
                />
                <Button 
                @click="$emit('add-favorite', pet.id)"
                icon="pi pi-heart" 
                :class="[pet.favorite ? 
                'p-button-rounded p-button-danger': 
                'p-button-rounded p-button-danger p-button-outlined']" 
                />
                 
            </template>
        </Card>
    </div>
</template>
<script>
export default {
    props: ["pet"],
    props: {
        pet: Object
    },
    components: {},
    methods: {
        onRemove(id){
            console.log('clicked', id);
            this.$emit("remove-pet", id)
        }
    }
}
</script>
<style>
img{
    height: 250px;
    object-fit: cover;
}
</style>