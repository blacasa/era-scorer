<template>
    <div id="app">
        Era: Medieval Age
        <br/>
        <b-form-group
            id="fieldset-1"
            label="Batiments">
            <batiment
                v-for="batiment in scorer.batiments"
                :key="batiment.type"
                v-bind:batiment="batiment"
                v-on:total-event-batiment="updateTotalScoreBatiment"/>
        </b-form-group>
        <b-form-group
            id="fieldset-1"
            label="Bonus">
            <bonus
                v-for="bonusLine in scorer.bonus"
                :key="bonusLine.type"
                v-bind:bonus="bonusLine"
                v-on:total-event-bonus="updateTotalScoreBonus"/>
        </b-form-group>
        <b-form-group
            id="fieldset-1"
            label="Malus">
            <malus
                v-for="malusLine in scorer.malus"
                :key="malusLine.type"
                v-bind:malus="malusLine"
                v-on:total-event-malus="updateTotalScoreMalus"/>
        </b-form-group>
        <b-form-group
            id="fieldset-1"
            label="Total">
            <total v-bind:score="[scorer.batiments, scorer.bonus, scorer.malus]"/>
        </b-form-group>
    </div>
</template>

<script>
import batiment from './components/batiment.vue'
import bonus from './components/bonus.vue'
import malus from './components/malus.vue'
import total from './components/total.vue'

import eraJson from './assets/era-scorer.json'

export default {
    name: 'app',
    data: function() {
        return {
            scorer: eraJson
        };
        /* Return avant mise en place d'un fichier json
        return {
            batiments: [
                {type: 'KEEP', label: 'Keep/Donjon', pts: 1, score: 0, icon: ''},
                {type: 'LONGHOUSE', label: 'Longhouse/Chaumière', pts: 1, score: 0, icon: ''},
                {type: 'TOWNHOUSE', label: 'Townhouse/Maison', pts: 1, score: 0, icon: ''},
                {type: 'CHURCH', label: 'Church/Eglise', pts: 1, score: 0, icon: ''},
                {type: 'FARM', label: 'Farm/Ferme', pts: 1, score: 0, icon: ''},
                {type: 'LUMBERMILL', label: 'Lumbermill/Scierie', pts: 2, score: 0, icon: ''},
                {type: 'HOSPITAL', label: 'Hospital/Hôpital', pts: 3, score: 0, icon: ''},
                {type: 'MONASTERY', label: 'Monastery/Monastère', pts: 4, score: 0, icon: ''},
                {type: 'MARKET', label: 'Market/Marché', pts: 2, score: 0, icon: ''},
                {type: 'GUILDHALL', label: 'Guildhall/Guilde', pts: 3, score: 0, icon: ''},
                {type: 'UNIVERSITY', label: 'University/Université', pts: 4, score: 0, icon: ''},
                {type: 'CATHEDRAL', label: 'Cathedral/Cathédrale', pts: 5, score: 0, icon: ''},
            ],
            bonus: [
                {type: 'MARKET_BONUS', label: 'Market/Marché', pts: 1, typeBonus: 'Espace libre', score: 0, unique: false, icon:''},
                {type: 'GUILDHALL_BONUS', label: 'Guildhall/Guilde', pts: 1, typeBonus: 'Ressource', score: 0, unique: false, icon:''},
                {type: 'UNIVERSITY_BONUS', label: 'University/Université', pts: 1, typeBonus: 'Culture', score: 0, unique: false, icon:''},
                {type: 'CATHEDRAL_BONUS', label: 'Cathedral/Cathédrale', pts: 1, typeBonus: 'Dés', score: 0, unique: false, icon:''},
                {type: 'CULTURE_BONUS', label: 'Culture', pts: 1, typeBonus: 'Culture', score: 0, unique: false, icon:''},
                {type: 'MOST_CULTURE_BONUS', label: 'Most Culture', pts: 5, typeBonus: 'Le plus de culture', score: 0, unique: true, icon:''},
                {type: 'MOST_WALLED_BONUS', label: 'Most Walled Area', pts: 10, typeBonus: 'Plus grande aire', score: 0, unique: true, icon:''},
            ],
            malus: [
                {type: 'DISASTER', label: 'Disaster/Désastre', pts: -1, score: 0, icon: ''},
            ],
        };
        //*/
    },
    components: {
        batiment,
        bonus,
        malus,
        total,
    },
    methods: {
        updateTotalScoreBatiment: function(total, type) {
            var updatedBatiment = this.scorer.batiments.find(function(batiment) {
                if (batiment.type === type) {
                    return batiment;
                }
            });
            updatedBatiment.score = total;
        },
        updateTotalScoreBonus: function(total, type) {
            var updatedBonus = this.scorer.bonus.find(function(bonusLine) {
                if (bonusLine.type === type) {
                    return bonusLine;
                }
            });
            updatedBonus.score = total;
        },
        updateTotalScoreMalus: function(total, type) {
            var updatedMalus = this.scorer.malus.find(function(malusLine) {
                if (malusLine.type === type) {
                    return malusLine;
                }
            });
            updatedMalus.score = total;
        },
    }
}
</script>