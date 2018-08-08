<template>
    <div>
       <h2>Add Animal</h2>

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

<table>
    <tr>
        <th>Species</th>
        <th>Name</th>
        <th>Date of Birth</th>
        <th>Name of sector</th>
    </tr>
    <tr v-bind:class="{background:activeColor(animal)}" v-for="(animal, key) in animals" :key="key" >
        <td>{{ animal.species }}</td> 
        <td >{{ animal.name }}</td> 
        <td>{{ animal.dateOfBirth ? animal.dateOfBirth : 'Unknown' }}</td> 
        <td>{{ animal.sector.name }}</td>
    <span>
         <button @click ="moveToTop(animal)">Top</button>
    </span>
    <span>
         <button @click ="removeAnimal(animal)">Remove</button>
    </span>
    <span>
         <button @click ="toggleBackground(animal)">Toggle button</button>
    </span>
    </tr>
</table>

<h2>Sectors</h2>
<table class="tableSector">
  <tr>
    <th>Name</th>
  </tr>
  <tr v-for="(sector, key) in sectors" :key="key" >
    <td>{{ sector.name }}</td> 
     <span>
         <button @click ="showAnimal(sector)">Show Animal</button>
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
            {
                species: "Snake",
                name:"Milica",
                dateOfBirth:"12.06.2011",
                sector:sectors[1],
                background:true
            }, 
            {
                species: "Puma",
                name:"Dragan",dateOfBirth:'',
                sector:sectors[0],
                background:false
            },
            {
                species: "Lion",
                name:"King",
                dateOfBirth:"12.06.2008",
                sector:sectors[0],
                background:true
            },
            {
                species: "Tiger",
                name:"Jack",
                dateOfBirth:'',
                sector:sectors[0],
                background:false
            },
            {
                species: "Alligator",
                name:"Mile",
                dateOfBirth:"23.07.2000",
                sector:sectors[1],
                background:true
            },
          ],  
      selected:'',  
      newAnimal:{background:true},
       //mora sectors ovde da ga ubacimo jer ga u data samo moze gore prepoznati
      // tu se zapravo nalazi const tj niz sectors, template vidi data()
      sectors:sectors
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

         showAnimal(sector)
         {  
            let listOfAnimal = [];
            this.animals.forEach(function(animal){
                if(sector == animal.sector){
                    listOfAnimal.push(`${animal.species}  ${animal.name}`);
               }
           })
           alert(listOfAnimal);
         },

         activeColor(animal)
         {  
             return animal.background;
         },

         toggleBackground(animal)
         {  
             if(animal.background == true){
                 animal.background = false;
             }else{
                 animal.background  = true;
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
table, td, th {    
    border: 1px solid #ddd;
    text-align: left;
}

table tr th{
    background-color:#ccffff;
}
table {
    width:60%;
    margin:0 auto;
    border-collapse: collapse;
   
}

th, td {
    padding: 15px;
}
form  input{
    padding:10px;
    margin-top:10px;
    width:30%;
    border-radius:7px;
}

form label{
    font-weight:bold;
    font-size:1.1rem;
}

.background{
    background-color:#80ffbf;
}
</style>