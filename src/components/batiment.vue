<template>
    <div>
        <b-container fluid>
            <b-row class="my-1">
            <b-col sm="5">
                <label for="batiment.type">Nb de "{{ batiment.label }}" ({{ batiment.pts }}pts):</label>
            </b-col>
            <b-col sm="1">
                <b-form-input v-model="qte" :id="batiment.type" type="number" :min="0"></b-form-input>
            </b-col>
            <b-col sm="1">
                <label for="batiment.label">dont</label>
            </b-col>
            <b-col sm="1">
                <b-form-input v-model="qteEntoure" :id="batiment.label" type="number" :max="qte" :min="0"></b-form-input>
            </b-col>
            <b-col sm="4">
                <label for="batiment.label">entouré(s).</label>
                Sous-total: {{ calculerScoreBatiment }} pts
            </b-col>
            </b-row>
        </b-container>
    </div>
</template>

<script>
export default {
    name: 'batiment',
    /* props: propriétés qui peuvent être envoyées par le parent */
    props: {
        batiment: Object,
    },
    /* data: propriétés locales au component */
    data: function() {
        return {
            qte: 0,
            qteEntoure: 0,
        }
    },
    /*
    created: function() {
        console.log(this.type + ' est créé');
    },
    //*/
    computed:{
        calculerScoreBatiment: function() {
            var totalBatiment = (this.qte * this.batiment.pts) + (this.qteEntoure * this.batiment.pts);
            this.$emit('total-event-batiment', totalBatiment, this.batiment.type);
            return totalBatiment;
        }
    }
} 
</script>

<style scoped>
    input {
        width: 50px;
    }
</style>