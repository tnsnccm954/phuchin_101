<template>
  <div class="content">
    <v-card class="mb-3 pa-3" color="indigo">
      <v-card-item>
        <!-- <label>Donator Name:</label>
        <input placeholder="None" name="donator_name" v-model="donatorName" /> -->
        <v-text-field clearable label="Donator Name" variant="solo" v-model="donatorName"></v-text-field>
      </v-card-item>
      <v-card-item>
        <!-- <label>Price:</label>
        <input type="number" name="price" v-model="price" min="1" /> -->
        <v-text-field clearable label="Price" variant="solo" v-model="price" type="number" min="1"></v-text-field>
      </v-card-item>
      <v-card-actions>
        <v-btn variant="flat" @click="donating" color="green" width="100%">Donate</v-btn>
      </v-card-actions>
    </v-card>
    <div class="text-center" v-if="donatorList.length > 0">
      <h1>Total: {{ donatorList.reduce((acc,donator)=> acc + donator.price,0) }}</h1>
    </div>
    <v-card class="pa-3" color="deep-purple">
      <v-card-item>
        <v-table class="pa-3 rounded" width="100%">
          <caption><h3><b>Donator Ranking</b></h3></caption>
          <thead>
            <tr>
              <th>*</th>
              <th>Donator Name</th>
              <th>Price</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="donator in donatorList">
              <td>{{ donator.id }}</td>
              <td>{{ donator.donatorName }}</td>
              <td>{{ donator.price }}</td>
            </tr>
          </tbody>
        </v-table>
      </v-card-item>
    </v-card>
  </div>
  <v-dialog v-model="dialog.display" max-width="290" persistent>
        <v-btn
          style="font-size: 20px;" 
          height="200" 
          @click="dialog.display = false"
        >
          Play!
        </v-btn>
  </v-dialog>
</template>

<script setup>
import { ref } from 'vue';

const latestDonatorId = ref(0)
const donatorName = ref('')
const price = ref(1)
const donatorList = ref([])
const dialog = ref({
  display: true
})

function donating() {
  // alert(donatorName.value)
  // alert(price.value)
  if(donatorName.value?.length > 0) {
    latestDonatorId.value++ 
    const donatorDetail = {
      id: latestDonatorId.value,
      donatorName: donatorName.value,
      price: price.value
    }
    donatorList.value.push(donatorDetail)
    donatorList.value.sort((a, b) => b.id - a.id)
  } else if (donatorName.value?.length <= 0) {
    alert('pls input name')
  }

}


</script>

<style>
.content {
  display: block;
  min-width: 600px;
  /* background-color: bisque;
  padding: 1rem;
  color: black;
  border-radius: 0.5rem; */
}
.donator-form {
  background-color: bisque !important;
}

</style>