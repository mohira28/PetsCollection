<template>
  <AddPet @add-pet="addPet"/>
  <Pets 
    @remove-pet="removePet" 
    :pets="pets"
    @add-favorite="addFavorite"
    />
</template>

<script>
import Pets from '../components/Pets.vue'
import AddPet from '../components/AddPet.vue'

export default {
  name: 'HomeView',
  components: {Pets, AddPet},
  methods: {
    /* addPet(pet){
      this.pets = [ ...this.pets, pet]
    }, */
    async addPet(pet){
      const res = await fetch('https://626c308650a310b8a3416c8a.mockapi.io/pets',{
        method: 'POST',
        headers: {
          "Content-type": "application/json"
        },
        body: JSON.stringify(pet)
      })
       const data = await res.json()
       this.pets = [...this.pets, data]
    },
    /* removePet(id){
        if(confirm('Are you sure you want to remove this pet?')){
          this.pets = this.pets.filter((pet) => pet.id !== id); 
        }
    }, */
    async removePet(id){
      if(confirm('Are you sure you want to remove this pet?')){
        const res = await fetch(
          `https://626c308650a310b8a3416c8a.mockapi.io/pets/${id}`,
            {
              method: "DELETE",
            }
        );
        res.status === 200 
        ? (this.pets = this.pets.filter((pet) => pet.id !== id)) 
        : alert('Delete failed!') 
      }
    },
    /* addFavorite(id){
      console.log('favorite: ', id );
      this.pets = this.pets.map((pet) => 
      pet.id === id ? { ...pet, favorite: !pet.favorite } : pet )
    }, */
    async addFavorite(id){
      const addFavorite = await this.fetchPet(id)
      const updatedFavorite = {
        ...addFavorite, favorite: !addFavorite.favorite
      }
      const res = await fetch(`https://626c308650a310b8a3416c8a.mockapi.io/pets/${id}`,  {
        method: "PUT",
        headers: {
          "Content-type": "application/json"
        },
        body: JSON.stringify(updatedFavorite)
      })
      const data = await res.json()

      this.pets = this.pets.map((pet) => pet.id === id? 
      {...pet, favorite: data.favorite} :
      pet)
    },
    async fetchPets(){
      const res = await fetch('https://626c308650a310b8a3416c8a.mockapi.io/pets')
      const data = await res.json()
      return data
    },
    async fetchPet(id){
      const res = await fetch(`https://626c308650a310b8a3416c8a.mockapi.io/pets/${id}`)
       const data = await res.json()
       return data
    }
  },
  data(){
    return {
      pets: []
    }
  },
  async created(){
     this.pets = await this.fetchPets()
   // this.pets = [
     
      /* {
          id: 1,
          name: "Ruby",
          age: 2,
          url: "https://i.ytimg.com/vi/MPV2METPeJU/maxresdefault.jpg",
          favorite: true
        },
        {
          id: 2,
          name: "Coco",
          age: 2,
          url: "https://ggsc.s3.amazonaws.com/images/uploads/The_Science-Backed_Benefits_of_Being_a_Dog_Owner.jpg",
          favorite: false
        } */
   // ]
  }
}
</script>
