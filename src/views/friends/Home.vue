<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png"> -->
    <Slider />
    <hr class="my-3" />
    <router-link class="btn btn-primary" to="/createfriends"
      >Profile Diri</router-link
    >
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Nama </th>
          <th scope="col">TTL</th>
          <th scope="col">Alamat</th>
          <th scope="col">Jenis Kelamin</th>
        </tr>
      </thead>
      <tbody>
         <tr v-for="(friend, index) in friends" :key="index">
          <td>Erika Anjani</td>
          <td>Cirebon, 17 April 2000</td>
          <td>Pabuaran Kidul</td>
          <td>Perempuan</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'
// @ is an alias to /src
import Slider from '@/components/Slider.vue'
import { onMounted } from '@vue/runtime-core';

export default {
  name: "Home",
  components: {
    Slider,
  },
  setup(){
    let friends = ref ([])

    onMounted(() => {
      axios.get('http://127.0.0.1:8000/api/friends')
      .then(Response => {
        friends.value = response.data.data.data
      }) 
      .catch(eror => {
        console.log(error)
      })
    })
    
    return {
      friends
    }
  }
};
</script>
