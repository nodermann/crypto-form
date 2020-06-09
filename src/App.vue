<template>
  <v-app>
    <v-container>
    	<v-row justify="center">
	      		<v-col lg="3">
			      	<card-payment></card-payment>
	      		</v-col>
    	</v-row>
    </v-container>
  </v-app>
</template>

<script>
require("./assets/sass/index.scss");
import CardPayment from './components/CardPayment.vue';
export default {
  name: 'App',

  components: {
  	CardPayment
  },

  data: () => ({
  	
  })

};
</script>
