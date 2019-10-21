<template>
    <div>
        <b-container fluid>
            <b-row class="my-1">
            <b-col sm="6">
                <label for="bonus.type">{{ bonus.label }} - {{ bonus.pts }}pts <span v-if="!bonus.unique">par</span><span v-else>pour</span> {{ bonus.typeBonus }}:</label>
            </b-col>
            <b-col sm="3">
                <b-form-input v-if="!bonus.unique" v-model="qte" :id="bonus.type" type="number" :min="0"></b-form-input>
                <b-form-checkbox
                    v-else
                    :id="bonus.type"
                    v-model="qte"
                    :name="bonus.type"
                    value="1"
                    :disabled="!bonus.actif"
                    unchecked-value="0">
                </b-form-checkbox>
            </b-col>
            <b-col sm="3">
                sous-total: {{ calculerScoreBonus() }} pts
            </b-col>
            </b-row>
        </b-container>
    </div>
</template>

<script>
export default {
    name: 'bonus',
    /* props: propriétés qui peuvent être envoyées par le parent */
    props: {
        bonus: Object,
    },
    /* data: propriétés locales au component */
    data: function() {
        return {
            qte: 0,
        }
    },
    // Utilisation de methods au lieu de computed
    // Lire: https://medium.com/@arieldi/bref-comprendre-le-computed-en-profondeur-dans-vue-js-ses-diff%C3%A9rences-avec-watch-methods-62635c2bb394
    methods:{
        calculerScoreBonus: function() {
            if (!this.bonus.actif) {
                // Si le bouton est inactif, on force qte à 0
                // pour décocher et forcer le score à 0
                this.qte = 0;
            }
            var totalBonus = this.qte * this.bonus.pts;
            this.$emit('total-event-bonus', totalBonus, this.bonus.type);
            return totalBonus;
        }
    }
} 
</script>

<style scoped>
    input {
        width: 50px;
    }
</style>