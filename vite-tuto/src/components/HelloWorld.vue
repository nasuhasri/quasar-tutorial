<template>
  <!-- <h1>{{ msg }}</h1>
  <button @click="count++">count is: {{ count }}</button>
  <p>Edit <code>components/HelloWorld.vue</code> to test hot module replacement.</p> -->

  <div>
    <h2> Filter Learn Vue Articles </h2>
    <input 
      type="text"
      placeholder="Filter Search"
      v-model="query"
    /> <br>
    {{ query }} <br>

    <button @click="reset">Reset</button>
    <!-- add the components declared her -->
    <!-- passing props from parent(HW) to child(SR) -->
    <result :query="query"/>
  </div>
</template>

<script>
/* Creating Reactive Data with ref */
/* ref: used to declare reactive variables */
import { ref } from 'vue';
/* Add components in HelloWorld.vue */
import result from './result.vue'

/* This is options API */
// export default {
//   name: 'HelloWorld',
//   props: {
//     msg: String
//   },
//   data() {
//     return {
//       count: 0
//     }
//   }
// }

/* Receive data in the Composition API */
/* setup run masa component tengah di-create */
/* Tempat kita define semua reactive data, computed properties, methods etc  */
export default {
  /* Declare the components here */
  components: {
    result
  },

  setup () {
    const query = ref('')

    const reset = (evt) => {
      // Clear the query
      query.value = ''
    }

    return {
      reset,
      query
    }
  }
}
</script>

<style>
  input[type='text'] {
    margin-bottom: 20px;
    padding: 10px;
  }
</style>
