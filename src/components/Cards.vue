<script setup lang="ts">

import {defineProps} from 'vue'
import {GENDER, type Invitee} from '../types'
  

    defineProps<{
        invitee: Invitee
    }>()

</script>

<template>
    <div :style="{backgroundColor: invitee.gender === GENDER.FEMALE ? 'rgb(8,111,111)' : 'rgb(111,18,8)'}">
       {{invitee.name}}
    </div>
</template>

<style scoped>

    div{
        background-color: #4CAF50;
        border-radius: 5px;
        margin-top: 5px;
        text-align: center;
        padding:3px;
        color: white;
    }
    </style>