<script setup lang="ts">

  import { ref, computed } from 'vue' 
  import Card from './components/Cards.vue'
  import {GENDER, type Invitee} from './types'


  const addInvitees = ():void => {
    if(name.value){   // if name.value is not empty
      invitees.value.push({
        id: Math.floor(Math.random() * 1000000),
        name: name.value,
        gender: gender.value
      });
      name.value = ""; // Clears the input field after the user adds a new invitee
      gender.value = GENDER.MALE // Determines the default value of gender after the user adds a new invitee
    }
  }

  const count = computed<{
    female: number,
    male: number
  }>(() => {
    return invitees.value.reduce((countObject, invitee) => {
      if(invitee.gender === GENDER.MALE){
        return { 
          ...countObject, // spread operator
          male : countObject.male + 1 
        }
      }
        return {
          ...countObject, 
          female : countObject.female + 1
        }
      
    }, {male: 0, female: 0})
  })

// VARIABLES FOR HTML
  const name = ref("")
  const gender = ref(GENDER.MALE)
  const invitees = ref<Invitee[]>([]) // is an empty array declared through the interface Invitee properties

</script>

<template>

  <main>
    <div>
        <h1>People Invited to My Parté</h1>
      <div class="input-container">
        <input 
        type="text"
        placeholder="Name..."
        v-model="name "
        @keypress.enter="addInvitees"
        >
        <select 
        v-model="gender" 
        @keypress.enter="addInvitees"
        >
          <option :value="GENDER.MALE">Male</option>
          <option :value="GENDER.FEMALE">Female</option>
        </select>
      </div>
      <div class="card-container">
        <Card 
        v-for="invitee in invitees" 
        :key="invitee.id" 
        :invitee="invitee"
        />
      </div>
      <div>
        <p>Female - {{ count.female }}</p>
        <p>Males - {{ count.male }}</p>
      </div>
    </div>
  </main>

</template>

<style scoped>

  main{
    height: 100vh;
    display:flex;
    justify-content: center;
    align-items: center;
    background-color: bisque;
  }

  input, select{
    width:100%;
    padding:5px;
    margin-bottom:2px;
  }

</style>
./types