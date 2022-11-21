<script setup>
import Todopedia from '@/components/Todopedia.vue'
import Navbar from '@/components/Navbar.vue'
</script>

<template>
  <Todopedia>
    <Navbar :user="{username: 'username'}" :signOut="() => {}" />
  </Todopedia>
</template>
