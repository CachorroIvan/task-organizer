<template>
  <div class="container mt-3">
    <Header />
    <hr/>
    <Forms />
  </div >
</template>

<script>
import Forms from './components/Forms.vue';
import Header from './components/Header.vue'

export default {
  components: {
    Header,
    Forms
  }
}

</script>

