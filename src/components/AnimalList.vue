<template>
    <div>
       <h2>Add List</h2>
 
 <form @submit.prevent>
    <label>Species</label><br>
    <input v-model="newAnimal.species" type="text" placeholder="Species"><br><br> 
    <label>Name</label><br>
    <input v-model="newAnimal.name" type="text" placeholder="name"><br><br>
    <label>Date of Birth</label><br>
    <input v-model="newAnimal.dateOfBirth" type="date"><br><br>
    <select v-model="newAnimal.sector">
       <option disabled value="">Please select one sector</option>
       <!--v-bind:value='sector' kada kliknemo na ime u padajucoj listi, kupi se value u ovom slucaju
       ceo objekat sector i cuvamo ga u newAnimal -->
        <option v-for='(sector, index) in sectors' :key='index' v-bind:value='sector'>
        {{sector.name}}</option>
    </select><br><br>
    <button @click="addAnimal" type="submit">Add Animal</button><br><br>
</form>
<h2>Animal List</h2>

<table id="animals">
  <tr>
    <th>Species</th>
    <th>Name</th>
    <th>Date of Birth</th>
     <th>Name of sector</th>
  </tr>
  <tr v-for="(animal, key) in animals" :key="key" >
    <td>{{ animal.species }}</td> 
    <td >{{ animal.name }}</td> 
    <td>{{ animal.dateOfBirth ? animal.dateOfBirth : 'Unknown' }}</td> 
    <td>{{ animal.sector.name }}</td>
    <td></td>
     <span>
         <button @click ="moveToTop(animal)">Top</button>
    </span>
    <span>
         <button @click ="removeAnimal(animal)">Remove</button>
    </span>
  </tr>
</table>

<h2>Sectors</h2>
<table id="animals">
  <tr>
    <th>Name</th>
  </tr>
  <tr v-for="(sector, key) in sectors" :key="key" >
    <td>{{ sector.name }}</td> 
     <span>
         <button @click ="showAnimal(animal)">Show Animal</button>
    </span>
  </tr>
</table>
    </div> 
</template>

<script>
const sectors = [
    {name:"predator", surface:"cage" },
    {name:"reptile", surface:"glassBox" },
];

export default {
  name: 'AnimalList',
  data()
  {
      return { 
      animals: [
            {species: "Snake", name:"Milica",dateOfBirth:"12.06.2011", sector:sectors[1]}, 
            {species: "Puma", name:"Dragan",dateOfBirth:'', sector:sectors[0]},
            {species: "Lion", name:"King",dateOfBirth:"12.06.2008", sector:sectors[0]},
            {species: "Tiger", name:"Jack",dateOfBirth:'', sector:sectors[0]},
            {species: "Alligator", name:"Mile",dateOfBirth:"23.07.2000", sector:sectors[1]},
          
      ],  
      selected:'',  
      newAnimal:{},
      sectors:sectors //mora ovde da ga ubacimo jer ga u data samo moze gore prepoznati
      // tu se zapravo nalazi const tj niz sectors, template vidi data()
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
                this.removeAnimal(animal);
                this.animals.unshift(animal);
            }
        },

         addAnimal()
         {
          this.animals.push(this.newAnimal); 
          this.newAnimal = {};
         },

         showAnimal()
         {  
             alert('caoo');
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

#animals {
    font-family: "Trebuchet MS", Arial, Helvetica, sans-serif;
    border-collapse: collapse;
    width: 100%;
}

#animals td, #animals th {
    border: 1px solid #ddd;
    padding: 8px;
}

#animals tr:nth-child(even){background-color: #f2f2f2;}

#animals tr:hover {background-color: #ddd;}

#animals th {
    padding-top: 12px;
    padding-bottom: 12px;
    text-align: left;
    background-color: #4CAF50;
    color: white;
}


</style>