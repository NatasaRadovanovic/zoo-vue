<template>
    <div>
        <h2>Animal List</h2>

<table id="customers">
  <tr>
    <th>Species</th>
    <th>Name</th>
    <th>Date of Birth</th>
  </tr>
  <tr v-for="(animal, key) in animals" :key="key" >
    <td>{{ animal.species }}</td> 
    <td >{{ animal.name }}</td> 
    <td>{{ animal.dateOfBirth ? animal.dateOfBirth : 'Unknown' }}</td> 
     <span>
         <button @click ="moveToTop(animal)">Top</button>
    </span>
    <span>
         <button @click ="removeAnimal(animal)">Remove</button>
    </span>
  </tr>
</table>
    </div> 
</template>

<script>

export default {
  name: 'AnimalList',
  data()
  {
      return { 
      animals: [
            {species: "Snake", name:"Milica",dateOfBirth:"12.06.2011"}, 
            {species: "Monkey", name:"Dragan",dateOfBirth:''},
            {species: "Lion", name:"King",dateOfBirth:"12.06.2008"},
            {species: "Tiger", name:"Jack",dateOfBirth:''},
            {species: "Alligator", name:"Mile",dateOfBirth:"23.07.2000"},
          
      ],
     }
    },
    
    methods: {
         removeAnimal(animal)
         {
            let index = this.animals.indexOf(animal);
            this.animals.splice(index, 1);
         },
        
        moveToTop(animal)
        {
            if(this.animals.indexOf(animal) > 0) {
            this.animals.splice(this.animals.indexOf(animal), 1);
            this.animals.unshift(animal);
}
        }
    }

}
  

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

#customers {
    font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
    border-collapse: collapse;
    width: 100%;
}

#customers td, #customers th {
    border: 1px solid #ddd;
    padding: 8px;
}

#customers tr:nth-child(even){background-color: #f2f2f2;}

#customers tr:hover {background-color: #ddd;}

#customers th {
    padding-top: 12px;
    padding-bottom: 12px;
    text-align: left;
    background-color: #4CAF50;
    color: white;
}

</style>