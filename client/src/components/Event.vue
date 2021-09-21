<template>
    <div class="card" :class="getClass(event)" v-on:click="toggleFilter">
        <h3>{{ event.raw }}</h3>
        <div class="submenu">{{ getTime(event.start, event.end) }}</div>
    </div>
</template>



<script>
export default {
    name: 'Event',

    data: () => ({

    }),

    props: ['event'],

    methods: {
        getTime(start, finish) {
            const sd = new Date(start)
            const fd = new Date(finish)

            const _ = x => (x < 10) ? `0${x}` : x

            return `${_(sd.getHours())}:${_(sd.getMinutes())} - ${_(fd.getHours())}:${_(fd.getMinutes())}`
        },

        getClass(event) {
            const find = str => (event.raw.indexOf(str) != -1)
            let mClass = 'other'
            if(find("EXAMEN"))
                mClass = 'exam'
            else if(find("( C)"))
                mClass = 'cm'
            else if(find("(TD)"))
                mClass = 'td'
            else if(event.group.indexOf('TP') != -1 || find('EPS'))
                mClass = 'tp'
            else if(find("Xfree"))
                mClass = 'xfree'

            return mClass
        },

        toggleFilter() {
            console.log(this.event.infos.lesson)
        }
    },
}
</script>



<style scoped>

    .card {
        padding: 20px;
        border-radius: 5px;
        background-color: #efefef;

        --cm: #FFA100;
        --td: #E87700;
        --tp: #FF9900;
        --ex: #373737;
        --xf: #A7A7A7;
    }

    .card h3 {
        font-size: 1em;
        font-family: 'B612 Mono', monospace;
    }

    .card.cm {
        background-color: var(--cm);
    }

    .card.td {
        background-color: var(--td);
    }

    .card.tp {
        background-color: var(--tp);
    }

    .card.xfree {
        background-color: var(--xf);
    }

    .card.exam {
        background-color: var(--ex);
        color: #fff;
    }

</style>