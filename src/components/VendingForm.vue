<script>
import AppTitle from './AppTitle.vue'

export default{
    data() {
        return {
            bill: '',
            owed: '',
            change: '',
            result: [],
        }
    },
    methods: {
        getChange,
        reset
    },
    components: {
        AppTitle
    },
    computed: {
        isButtonDisabled() {
            return this.result.length != 0 
            
        }
    }
}

function getChange(bill, owed){
    let change = bill - owed;
    let denomination = [
        {name: 'P1000 bill', value: 1000},
        {name: 'P500 bill', value: 500},
        {name: 'P200 bill', value: 200},
        {name: 'P100 bill', value: 100},
        {name: 'P50 bill', value: 50},
        {name: 'P20 bill', value: 20},
        {name: 'P10 coin', value: 10},
        {name: 'P5 coin', value: 5},
        {name: 'P1 coin', value: 1},       
    ]
    if(bill < 0 || owed < 0){
        this.result.push("Avoid using negative numbers")
    }
    else if(bill < owed){
         this.result.push("Bill amount is not enough")
    }
    else if(bill == owed || owed == 0 ){
         this.result.push("No changes needed")
    }
    else{
        for(let i=0; i< denomination.length; i++){
            if(change >= denomination[i].value){
                let num = Math.floor(change / denomination[i].value)
                change = change % denomination[i].value
                this.result.push(`${num} ${denomination[i].name}`)
                this.change = `${bill - owed} Pesos`
            }
        }
    } 
 }

 function reset(){
    this.result = []
    this.change = ''
 }
</script>

<template>
    <form @submit.prevent="getChange(bill, owed)">
        <AppTitle title = "Vending Machine" />

        <label>Bill Amount:</label>
        <input type ="number" v-model="bill" required placeholder="Enter the bill payment amount" @focus="reset()">
        <label>Owed Amount:</label>
        <input type ="number" v-model="owed" required placeholder="Enter the owed amount" @focus="reset()"> 
        <label> Change: {{ `${change}` }}</label>
        <div class ="result">
             {{ ` ${result.join('\n')} `}}
        </div>
        <div class="submit">
            <button :disabled="isButtonDisabled">Calculate</button>
        </div>
    </form>
   
</template>

<style>
 form{
    max-width: 470px;
    margin: 30px auto;
    margin-top: 8%;
    background: #eee;
    padding: 40px;
    border-radius: 10px;
 }
 label, .change, .result{
    color: #5c5c5c;
    display: flex;
    margin: 25px 0 15px;
    font-size: 0.9rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
 }
 .result{
    justify-content: center;
    font-size: 1rem;
    font-weight: bold;
    white-space: pre-line;
 }
 input{
    background: #eee;
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
    outline: none;
 }
 input:hover, :focus{ border-bottom-color: #1d19ee; }
 
 button{
    background: #1d19ee;
    width: 100%;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
    cursor: pointer;
    transition: 0.3s;
    font-weight: bold;
    letter-spacing: 1px;
    text-transform: uppercase;
 }
 button:hover { opacity: 0.6 }

 .submit{ text-align: center; }

 .submit :disabled{
    opacity: 0.6;
    cursor: not-allowed;
 }

 @media (max-width: 450px) {
    form{
        width: 60%;
    }
    label, .result, .change{
        font-size: 0.7rem;
    }
 }
</style>