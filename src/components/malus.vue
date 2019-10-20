<template>
    <div>
        <b-container fluid>
            <b-row class="my-1">
            <b-col sm="6">
                <label for="malus.type">Nb de "{{ malus.label }}" ({{ malus.pts }}pts):</label>
            </b-col>
            <b-col sm="3">
                <b-form-input v-model="qte" :id="malus.type" type="number" :min="0"></b-form-input>
            </b-col>
            <b-col sm="3">
                sous-total: {{ calculerScoreMalus }} pts
            </b-col>
            </b-row>
        </b-container>
    </div>
</template>

<script>
export default {
    name: 'malus',
    /* props: propriétés qui peuvent être envoyées par le parent */
    props: {
        malus: Object,
    },
    /* data: propriétés locales au component */
    data: function() {
        return {
            qte: 0,
        }
    },
    computed:{
        calculerScoreMalus: function() {
            var totalMalus = this.qte * this.malus.pts;
            if (totalMalus > 0) 
            totalMalus = totalMalus > 0 ? totalMalus * (-1) : totalMalus;
            this.$emit('total-event-malus', totalMalus, this.malus.type);
            return totalMalus;
        }
    }
} 
</script>

<style scoped>
    input {
        width: 50px;
    }
</style>