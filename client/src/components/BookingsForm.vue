<template lang="html">
  <div id="form">
    <form v-on:submit="addBooking" id="bookings-form">
  		<h2>Add a Booking</h2>
  		<div class="formWrap">
  			<label for="name">Name:</label>
  			<input  v-model="name" type="text" id="name" />
  		</div>
  		<div class="formWrap">
  			<label for="email">Email:</label>
  			<input v-model="email" type="text" id="email" />
  		</div>
  		<div class="formWrap">
  			<label for="checkedIn">Checked in:</label>
  			<input v-model="checkedIn" type="checkbox" id="checkedIn" :checked="checkedIn" />
  		</div>

  		<input type="submit" value="Save" id="save"/>
  	</form>
  </div>
</template>

<script>
import BookingsService from '@/services/BookingsService.js'
import { eventBus } from '../main.js'

export default {
  name: 'bookings-form',
  data() {
    return {
      name: "",
      email: "",
      checkedIn: false   
    }
  },

  methods: {
      addBooking(event){
        event.preventDefault()

        const payload = {
          name: this.name,
          email: this.email,
          checkedIn: this.checkedIn
        };

        BookingsService.postBooking(payload)
        .then(booking => {
          eventBus.$emit('booking-added', booking)
        })
      }
  }
}
</script>

<style lang="css" scoped>
</style>
