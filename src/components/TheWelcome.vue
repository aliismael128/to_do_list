<script setup>
import headerk from './headerk.vue';
import footerk from './footerk.vue'
</script>

<template>
  <headerk></headerk>
  <div class="gobal">
    <div class="contenuk">
    <div class="titre_page">
      <p>
        <h3>lists des taches affaires </h3>
        <br>
        <h3 id="days"  >{{ heure }} 🥳 </h3>
        
        
      </p>
    </div>
    
      <ul class="liste1">
        <li class="premier"  v-for="liste_chose_affaire,index in liste_chose_affaire " v-show="liste_chose_affaire.fini === !showCompleted2">
          <button @click="supprime(index)">supprime</button>
          {{ liste_chose_affaire.texte}}
          <input type="checkbox" name="" class="checkbox" v-model="liste_chose_affaire.fini">
        </li>
      </ul>
    </div>
    <div class="motie_gobal">
      <div class="tache_effectue">
        <br>
 <br>
        <h2>taches deja effectués</h2>
        
        <ul >
          <li v-for="liste_chose_affaire,index in liste_chose_affaire" v-show="liste_chose_affaire.fini || !showCompleted2">
            <button @click="supprime(index)">supprime</button>
            {{ liste_chose_affaire.texte}}
            <input type="checkbox" name="" class="checkbox" v-model="liste_chose_affaire.fini">
          </li>
        </ul>
      </div>
      <div class="tache_a_venir">
        <!-- <br> -->
        <!-- <br> -->
       
          <h2 class="pading">taches a venir</h2>
         
         
          <div class="modale">  <p class="clik">
   <a href="#" v-on:click="clique"><img src="../assets/icons8-plus-150.png" alt=""></a>
 </p>

          <div class="inputk">
            
            <h3> tache :</h3>
     <input type="text" value="" class="nouvaux" @keyup.enter="nouvelleTachek">
    <p  class="croix">
      <a href="#" v-on:click="clique_efface"><img src="../assets/icons8-x-64.png" alt=""></a>
    </p>
    </div>
  </div>
  <ul>
        <li v-for="nouveau_element,index in nouveau_element ">
          <button @click="supprime2(index)">supprime</button>
          {{ nouveau_element.texte}}
        <button @click="envoyer">Ajout</button>
        </li>
      </ul>
     
     
     
    </div>
    </div>
  </div>
  <footerk></footerk>
</template>

<script>
export default {
  data() {
    return {
      nouveau_element:[
      {texte: 'goats', fini:false},
 {texte: 'sheep', fini:false},
      ],

      liste_chose_affaire: [
        {texte: 'nettoyer ma voiture', fini: true},
        {texte: 'lectures de livre', fini: true},
        {texte: 'film one piece', fini: true},
        {texte: 'achetter un sac dos', fini: false},
        {texte: 'achetter une femme', fini: false}
      ],
      showCompleted2: { fini: false },
      heure: '',
     
    }
  },mounted(){
   
  
	let date2= new Date();
  let actuel = date2.toLocaleDateString(navigator,{weekday: 'long', year: 'numeric', month: 'long', day: 'numeric'});
  this.heure =actuel;
  

  const savedData = localStorage.getItem('todoList');
    if (savedData) {
      this.nouveau_element = JSON.parse(savedData);}

      const savedData2   = localStorage.getItem('todoList2');
   if (savedData2) {
     this.liste_chose_affaire = JSON.parse(savedData2);}


  
  }
   
  
  ,
  methods: {
    envoyer: function() {
  if (this.nouveau_element.length > 0) {
    let nouvelleTache = this.nouveau_element[0];
    this.liste_chose_affaire.push(nouvelleTache);
    this.nouveau_element.splice(0, 1);
  }
},
supprime:function(index){
  this.liste_chose_affaire.splice(index, 1);
  
},
supprime2:function(index){
  this.nouveau_element.splice(index, 1);
  
},
nouvelleTachek:function(){
  let input = document.querySelector('.nouvaux').value;
  let newElement = { texte: input, fini: false };
  this.nouveau_element.push(newElement);
  document.querySelector('.nouvaux').value = '';
},

clique:function(){
   let clique_affiche = document.querySelector('.inputk')
   clique_affiche.style.display= "flex";
},
clique_efface:function(){
  let clique_efface= document.querySelector('.inputk')
 clique_efface.style.display= "none";
}





  },
  watch:{
    nouveau_element: {
      deep: true,
      handler() {
        // Sauvegarder les données de la liste dans le stockage local à chaque modification
        localStorage.setItem('todoList', JSON.stringify(this.nouveau_element));
      }

  },
  liste_chose_affaire: {
     deep: true,
     handler() {
       // Sauvegarder les données de la liste dans le stockage local à chaque modification
       localStorage.setItem('todoList2', JSON.stringify(this.liste_chose_affaire))
     }
 }
  
}
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Lilita+One&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Darumadrop+One&display=swap');
.gobal {
  height: 80vh;
  background-color: aqua;
  display: flex;
}
.contenuk{
  background-color:#00B4D8;
  width:60%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  border:6px solid  aliceblue;
  height: 100%;
}
.tache_effectue{
  background-color: #FCA311;
  height: 49%;
  overflow: hidden;
  overflow-y: auto;

}
.tache_a_venir{
  background-color:#9B2226;
  height: 49%;
  overflow: hidden;
  overflow-y: auto;
  
}
.motie_gobal{
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
background-color: aliceblue;
width: 40%;
padding: 0.6rem;

}
li{
  list-style: none;
  text-decoration: none;
margin: 4rem;
text-align: center;
font-size: 1.5rem;
text-transform: uppercase;
display: flex;
justify-content: space-around;
align-items: center;
/* background-color: #9B2226; */
width: 90%;
font-family: 'Lilita One', cursive;
}
.premier{
  padding: 1rem;
}

h2,h3{
  text-align: center;
  font-size: 2rem;
  color: azure;
  text-transform: capitalize;
  font-family: 'Darumadrop One', cursive;
}
input[type="checkbox"]{
    width: 50px;
    height: 50px;
 
 -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
 border: 2px solid #cae9ff;
 border-radius:50%;

    /* Add a background color */
    background-color: #EDF2F4;

 }
 input[type=checkbox]:checked {
    /* Add a background color */
/*    background-color: #007bff;*/
    background-image: url("../assets/checkbox.png");
   background-position: center;
   background-size: cover;
}

/* Hover state */
input[type=checkbox]:hover {
    /* Add a border color */
    border-color: #187177;
}
button{
			border:transparent;
			font-size: 22px;
			border-radius: 30px;
			width:10vw;
			height:5vh;
			 background: linear-gradient(90deg, #5DE0E6, #0078A6);
			 color:white;
/*		font-family: 'Monoton', cursive;*/
font-family: 'Braah One', sans-serif;
				}
        button:hover{
					border: 2px solid white;
				}

.inputk{
  display: flex;
  background-color: black;
  padding: 1rem;
  justify-content: space-around;
  border-radius:10px;
  /* border: solid 1px pink; */
 
}
.nouvaux{
  width: 65%;
  height:4rem;
  text-align: center;
  border: solid 2px #41ead4;
  border-radius: 30px;
  outline: none;
}
.nouvaux:focus{
  border: solid 2px #41ead4 ;
}

.clik img {
  width:3rem;
}
.clik{
  text-align: center;
  padding: 1rem;
}
.pading{
  padding:0.2rem;
}
.inputk{
  display: none;
}


.croix img{
  height:4rem;
}

.liste1{
  overflow: hidden;
	   overflow-y: auto;
     height: 30vh;
     /* padding:2rem; */
    
}
::-webkit-scrollbar {
  width: 20px;
}

/* Track */
::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px grey; 
  border-radius: 10px;
}
 
/* Handle */
::-webkit-scrollbar-thumb {
  background: #edf6f9; 
  border-radius: 10px;
}

/* Handle on hover */
::-webkit-scrollbar-thumb:hover {
  background: #f8f7ff; 
}

</style>
