<template>
    <div class= "conversor" >
        <h2> {{moedaA}} para {{moedaB}}</h2>
        <input type="text" v-model="moedaA_value" v-bind:placeholder="moedaA">
        <input type="button" value="converter" v-on:click="converter">
        <h2>{{moedaB_value}}</h2>
    </div>
</template>

<script>
export default {
    name: "Conversor",
    props: ["moedaA","moedaB"],
    data(){
        return{
            moedaA_value : "",
            moedaB_value : 0
        };
    },
    methods:{
        converter(){
            let de_para = this.moedaA + "_" + this.moedaB
            let url = "https://free.currconv.com/api/v7/convert?q=" + 
            de_para +
            "L&compact=y";
            fetch(url).then(res=>{return res.json();
            })
            .then (json=>{
                let cotacao = json [de_para].val;
                this.moedaB_value = (cotacao * parseFloat(this.moedaA_value).tofixed(2))
            })
        }
    }
    
};
</script>

<style scoped>
</style>