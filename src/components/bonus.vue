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
                    unchecked-value="0">
                </b-form-checkbox>
            </b-col>
            <b-col sm="3">
                sous-total: {{ calculerScoreBonus }} pts
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
    computed:{
        calculerScoreBonus: function() {
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