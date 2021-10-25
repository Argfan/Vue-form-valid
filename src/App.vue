<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-6">
          <UserForm/>
        </div>
      </div>      
    </div>    
  </div>
</template>

<script>

import UserForm from './components/UserForm.vue'

export default {
  name: 'App',
  components: {
    UserForm
  }
}
</script>

