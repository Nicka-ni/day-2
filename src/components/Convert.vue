<template>
    <div class="curse">
<center><h2>Exchange rates</h2></center> 
		<span>Enter the amount</span><input type="number" v-model = "currency"> <br><br>
		<span>from</span>
		<select  v-model = "rate1">
			<option v-for="item in conver" :value="item.buy"  v-bind:key="item.ccy">{{ item.ccy }}</option>
		</select>
		<span>to</span>
		<select v-model = "rate2">
			<option v-for="item in conver" :value="item.buy"  v-bind:key="item.ccy">{{ item.ccy }}</option>
		</select><br><br>
		<button v-on:click="calculate()">Конвертировать</button>
		<h3 v-if="converted">{{ res }}</h3>
    </div>
    
</template>

<script>

import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'


export default {
    data: function(){
        return {
           currency:1,
        conver:[],
        res: "",
        converted: true,
        rate1: "",
        rate2: "",
        };
    },
    mounted: function(){
        axios.get("https://api.privatbank.ua/p24api/pubinfo?json&exchange&coursid=5").then((response) =>{
            console.log(response.data);
            this.conver = response.data;
        })
    },
    methods: {
        calculate: function(){
            this.res = this.rate1 / this.rate2 * this.currency
        }
    }
}
</script>

