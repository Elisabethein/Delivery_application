<template>
  <main>
    <div class="slide-container" :class="{ 'active': citySelected }">
      <h1 class="welcome-text">Welcome to food delivery application!</h1>
      <h2 class="choose-city">Please choose your location</h2>
      <div class="city-container">
        <div class="city" @click="selectCity('Tallinn')">
          <p>Tallinn</p>
        </div>
        <div class="city" @click="selectCity('Tartu')">
          <p>Tartu</p>
        </div>
        <div class="city" @click="selectCity('Pärnu')">
          <p>Pärnu</p>
        </div>
      </div>
    </div>
    <div class="information" :class="{ 'visible': citySelected }">
      <div class=vehicle-container>
        <h2 class="choose-vehicle" :class="{ 'visible-text': !vehicleSelected }">Please choose your vehicle</h2>
        <h2 class="choose-vehicle" :class="{ 'visible-text': vehicleSelected }">Delivery fee for {{ chosenVehicle }} in
          {{ chosenCity }} is:</h2>
        <p v-if="error" class="error-message">{{ error }}</p>
        <div class="choose-vehicle-container">
          <div class="vehicle" @click="selectVehicle('Car')">
            <img src="@/assets/icons8-car-100.png" alt="Car">
          </div>
          <div class="vehicle" @click="selectVehicle('Scooter')">
            <img src="@/assets/icons8-scooter-100.png" alt="Scooter">
          </div>
          <div class="vehicle" @click="selectVehicle('Bike')">
            <img src="@/assets/icons8-bike-100.png" alt="Bike">
          </div>
          <div class="delivery-fee-outside">
            <div class="delivery-fee-inside">
              <p class="delivery-fee-text">{{ deliveryFee }}</p>
            </div>
          </div>
        </div>
      </div>
      <p class="welcome-text">Offers near you:</p>
      <div class="offers">

        <div class="offer">
          <img src="@/assets/alexander-startsev-ndNw_6QGR_c-unsplash.jpg" alt="Burger">
        </div>
        <div class="offer">
          <img src="@/assets/deborah-rainford-zOlZgELBMRg-unsplash.jpg" alt="Taco">
        </div>
        <div class="offer">
          <img src="@/assets/jonathan-borba-7TeR1A1MUpM-unsplash.jpg" alt="Milkshake">
        </div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'Home',
  data() {
    return {
      citySelected: false,
      chosenCity: '',
      vehicleSelected: false,
      chosenVehicle: '',
      deliveryFee: '',
      error: '',
    };
  },
  methods: {
    selectCity(city) {
      this.citySelected = true;
      this.chosenCity = city;
      this.getDeliveryFee(city, this.chosenVehicle);
    },
    selectVehicle(vehicle) {
      this.vehicleSelected = true;
      this.chosenVehicle = vehicle;
      this.getDeliveryFee(this.chosenCity, vehicle);
    },
    getDeliveryFee(city, vehicle) {
      if (!this.citySelected || !this.vehicleSelected) {
        return '';
      }
      const url = new URL('http://localhost:8080/api/calculateRbf');
      url.searchParams.append('city', city);
      url.searchParams.append('vehicleType', vehicle);

      fetch(url)
          .then(response => response.json())
          .then(data => {
            if (data === -1) {
              this.error = 'Usage of selected vehicle type is forbidden';
              return;
            }
            this.error = '';
            this.deliveryFee = data;
          })
          .catch(error => {
            this.error = 'Usage of selected vehicle type is forbidden';
            console.error(error);
          });
    }
  }
};
</script>

<style scoped>
main {
  user-select: none;
}

.slide-container {
  position: absolute;
  padding-top: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 95%;
  transition: transform 0.3s ease; /* Slide transition */
}

.active {
  transform: translateY(-30%);
}

.information {
  display: none;
  width: 95%;
  position: absolute;
  top: calc(200px + 30%);
  background-color: #E9FBD2;
}

.visible {
  display: block;
}

.welcome-text {
  font-size: 40px;
  font: Krub;
  font-weight: bold;
  text-align: center;
}

.choose-city {
  font-size: 32px;
  font: Krub;
  font-weight: light;
}

.city-container {
  display: flex;
  justify-content: space-around;
  padding-top: 10px;
}

.city {
  background-color: #84BF70;
  padding: 20px;
  margin: 10px;
  border-radius: 25px;
  cursor: pointer;
  width: 272px;
  height: 123px;
  transition: transform 0.3s ease;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.5);
}

.city:hover {
  transform: scale(1.1);
}

.city p {
  font-size: 48px;
  font: Krub;
  font-weight: bold;
  text-align: center;
}

.choose-vehicle {
  display: none;
  font-size: 32px;
  font: Krub;
  font-weight: light;
  justify-content: center;
  align-items: center;
}

.visible-text {
  display: flex;

}

.delivery-fee-text {
  font-size: 45px;
  font: Krub;
  font-weight: bold;
  text-align: center;
}

.choose-vehicle-container {
  display: flex;
  padding-top: 5px;
  justify-content: center;
}

.error-message {
  display: flex;
  font-size: 32px;
  font: Krub;
  font-weight: bold;
  justify-content: center;
  align-items: center;
  color: rgb(131, 60, 16);
  background-color: rgb(226, 192, 141);
}

.vehicle {
  background-color: #BEEFAD;
  margin: 20px;
  border-radius: 25px;
  width: 94px;
  height: 87px;
  transition: transform 0.3s ease;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.5);
}

.vehicle:hover {
  transform: scale(1.1);
}

.vehicle img {
  width: 86px;
  height: 86px;
  padding-left: 10px;
}

.delivery-fee-outside {
  margin: 20px;
  background-color: #BEEFAD;
  border-radius: 25px;
  width: 165px;
  height: 87px;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.5);
}

.delivery-fee-inside {
  background-color: #EBF4E8;
  border-radius: 20px;
  width: 145px;
  height: 70px;
  margin-top: 8px;
  margin-left: 10px;
}

.offers {
  width: 100%;
  padding-top: 40px;
  display: flex;
  justify-content: space-around;
}

.offer {
  background-color: #BEEFAD;
  width: 30%;
  min-height: 200px;
  border-radius: 25px;
  transition: transform 0.3s ease;
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.5);
}

.offer:hover {
  transform: scale(1.1);
}

.offer img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 20px;
  padding: 10px;
}

</style>