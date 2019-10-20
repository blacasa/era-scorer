<template>
    <div>
        Score total: {{ calculateScore }} pts
    </div>
</template>

<script>
export default {
    name: 'total',
    /* props: propriétés qui peuvent être envoyées par le parent */
    props: {
        score: Array,
    },
    computed: {
        calculateScore: function() {
            var subtotal = 0
            this.score.forEach(function(typeSCore) {
                typeSCore.forEach(function(line) {
                    subtotal += line.score;
                });
            });
            return subtotal;
        }
    },
}
</script>