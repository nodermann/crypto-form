<template>
	<div class="card-payment d-flex flex-column">
		<div class="card-payment__header pt-2 pb-2">
    		<h3 class="display-1 text-center font-weight-regular">Video Inc.</h3>
    		<p class="title text-center font-weight-regular mb-0 card-payment__subtitle">12 Month Membership</p>
    	</div>
    	<div class="card-payment__body flex-grow-1">
    		<template v-if="!walletGenerated">
	    		<h3 class="headline text-center font-weight-regular mt-3 mb-4 color-gray">Select payment currency</h3>
	    		<v-combobox 
	    			v-model="selectedCrypto" 
	    			class="combobox" 
	    			hide-details="auto"
	    			:items="cryptoCurrencies"
	    			auto-select-first
	    			dense
	    			outlined>
	    				<template #item="{item}">
	    					<div class="combobox__item d-flex align-center justify-space-between">
	    						<div class="d-flex align-center">
		    						<img class="icon icon_sm mr-2" :src="require(`../assets/icons/${item.logo}`)" alt="">
									<span>{{item.name}}</span>
	    						</div>
	    						<div>
	    							<span class="mr-1">{{item.rate}}</span>
	    							<span>{{item.label}}</span>
	    						</div>
	    					</div>
	    				</template>
	    				<template #selection="{item}">
	    					<div class="combobox__item d-flex align-center justify-space-between">
	    						<div class="d-flex align-center">
		    						<img class=" icon icon_sm mr-2" :src="require(`../assets/icons/${item.logo}`)" alt="">
									<span>{{item.name}}</span>
	    						</div>
	    						<div >
	    							<span class="mr-1">{{item.rate}}</span>
	    							<span>{{item.label}}</span>
	    						</div>
	    					</div> 
	    				</template>
	    		</v-combobox>
	    		<p class="text-center mb-5 mt-5 color-gray-lighten">Your payment will be confirmed after the transaction is mined in the Ethereum network.</p>
	    		<div class="d-flex justify-space-between border-top pt-2">
	    			<span class="text-muted">Total</span>
	    			<span class="text-primary headline">${{total}}</span>
	    		</div>
    		</template>
    		<template v-else>
    			<h4 class="headline font-weight-regular mt-4 mb-4 text-center">19:35</h4>
    			<img :src="require('../assets/qr.png')" alt="" class="d-block ml-auto mr-auto mb-5">
    			<p class="color-gray-lighten text-center mb-2 body-2">Send the amount to the address below</p>
    			<v-text-field 
    				v-model="selectedCrypto.rate" 
    				append-icon="'mdi-eye-off'" 
    				outlined 
    				readonly 
    				dense 
    				hide-details="auto" 
    				class="mb-2 input input_has-prepend">
    				<template #prepend-inner>
    					<div class="d-flex align-center input__prepend mr-1">
	    					<img :src="require(`../assets/icons/${selectedCrypto.logo}`)" alt="" class="icon icon_sm mr-1">
	    					<span class="body-2 font-weight-regular">{{selectedCrypto.label}}</span>
    					</div>
    				</template>
    				<template #append>
    					<v-btn icon>
	    					<img :src="require('../assets/icons/copy.svg')" alt="" class="icon icon_md" @click="copyToClipboard(selectedCrypto.rate)">
    					</v-btn>
    				</template>
    			</v-text-field>
    			<v-text-field 
    				v-model="walletGenerated" 
    				append-icon="'mdi-eye-off'" 
    				outlined 
    				readonly 
    				dense 
    				hide-details="auto"
    				class="input mb-3">
    				<template #append>
    					<v-btn icon>
	    					<img :src="require('../assets/icons/copy.svg')" alt="" class="icon icon_md" @click="copyToClipboard(walletGenerated)">
    					</v-btn>
    				</template>
    			</v-text-field>
    			<p class="text-center color-gray-lighten mb-4 body-2">Do not send funds from an exchange.</p>
	    		<p class="text-center mb-5 mt-5 color-gray-lighten">Your payment will be confirmed after the transaction is mined in the Ethereum network.</p>
    		</template>
    	</div>
    	<div class="card-payment__footer d-flex flex-column align-center">
    		<v-btn v-if="!walletGenerated" color="primary" class="card-payment__action mb-3" x-large :disabled="!selectedCrypto" @click="generateWallet">{{selectedCrypto ? `Pay with ${selectedCrypto.name}` : 'Pay'}}</v-btn>
    		<div class="card-payment__copyright text-center">Powered by Company</div>
    	</div>
    </div>
</template>

<script>
export default {

  name: 'CardPayment',

  data () {
    return {
    	walletGenerated: null,
	  	total: 15.00,
	  	cryptoCurrencies: [
		  	{
		  		name: 'Ethereum',
		  		logo: 'ethereum.svg',
		  		rate: 0.593,
		  		label: 'ETH'	
		  	}
	  	],
	    selectedCrypto: null
    }
  },
  methods: {
  	/**
  	 * Метод копирования текста в буфер
  	 * @param  {String} string
  	 */
  	copyToClipboard(string){
    	let input = document.createElement('input');
    	input.value = string;
    	document.body.appendChild(input);
    	input.select();
    	document.execCommand('copy');
    	document.body.removeChild(input);
    },
    /**
     * Метод генерации кошелька
     */
    generateWallet(){
    	this.walletGenerated = '0xa9bff538a906154c80a8dbccd229f3deddfa52d6';
    }
  }
}
</script>

<style lang="css" scoped>

</style>