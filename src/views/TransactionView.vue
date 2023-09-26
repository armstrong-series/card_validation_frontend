<template>
  <div class="transaction">
    <h3 class="">Enter Card Details</h3>

    <div class="mb-3">
      <input type="number" v-model="pan" class="form-control" id="pan" placeholder="Enter card PAN">
    </div>

    <div class="mb-3">
      <input type="number" v-model="cvv" class="form-control" id="cvv" placeholder="Enter your card CVV">
    </div>

    <div class="mb-3">
      <input type="text" v-model="expiry_date" class="form-control" id="expiry_date" placeholder="Expiration date in YY-MM format">
    </div>

    <div class="mb-3">
      <Button class="btn btn-sm btn-primary btn-block" @click.prevent="validateCardDetails()">Submit Details</Button>
    </div>

  </div>
</template>

<style>
@media (min-width: 1038px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>

<script>
import toastr from 'toastr';
import axios from 'axios';

export default {

  data() {
    return {
      pan: '',
      cvv: '',
      expiry_date: ''
    }

  },

  methods: {

    async validateCardDetails() {
      try {
        // const BASEURL = process.env.baseUrl;

        const response = await axios.post('http://127.0.0.1:8000/validate-credit-card', {
        // const response = await axios.post(`${BASEURL}/card/validate-credit-card`, {
          'pan': this.pan,
          'cvv': this.cvv,
          'expiry_date': this.expiry_date
        })
        console.log('data', response.data)
        return toastr.success(response.data.message)
      } catch (error) {
        toastr.error(error)
      }
    }
  },
}

</script>
