<template>
    <div id="home">
        <div id="events">
            
            <div class="week" v-for="week in Object.entries(events)" :key="week[0]">
                <h2 class="week-num">Semaine {{ week[0].slice(1) }}</h2>
                
                <div class="day" v-for="day in Object.entries(week[1])" :key="day[0]">
                    <div class="day-num" :class="isToday(day[0])">
                        <div class="day-num-weekday">{{ dayList[new Date(day[0]).getDay()] }}</div>
                        <div class="day-num-number">{{ new Date(day[0]).getDate() }}</div>
                    </div>
                    <div class="event-list">
                        <Event v-for="event in day[1]" :key="event.raw" :event="event" />
                    </div>
                </div>
            </div>

        </div>
    </div>
  
</template>



<script>
  import Event from '@/components/Event.vue'

  export default {
    name: 'Home',

    components: { Event },

    methods: {
        isToday(day) {
            const isToday = (new Date().toDateString() == new Date(day).toDateString())
            return isToday ? 'today' : ''
        }
    },

    data: () => ({
        dayList: ['Dim', 'Lun', 'Mar', 'Mer', 'Jeu', 'Ven', 'Sam'],
        events: {}
    }),

    mounted() {
        fetch("http://localhost:4000/events").then(x => x.json()).then(res => this.events = res)
    }
  }
</script>



<style scoped>
  #home {
      width: 95%;
      max-width: 1200px;

      margin: 0 auto;
  }

  

  .week-num {
      margin-bottom: 20px;
  }



  .day {
      margin-bottom: 20px;
      display: flex;
      gap: 20px;
      align-items: flex-start;
  }

  .day-num {
    aspect-ratio: 1/1;
    width: 100px;

    padding: 20px;

    border-radius: 10px;

    background-color: #ededed;
    
    display: grid;
    place-items: center;
  }

  .day-num.today {
      background-color: #000;
      color: #fff;
  }

  .day-num .day-num-weekday {
      text-transform: uppercase;
      font-family: 'B612 Mono', monospace;
  }

  .day-num .day-num-number {
      font-size: 1.5em;
  }

  .event-list {
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 10px;
  }
</style>