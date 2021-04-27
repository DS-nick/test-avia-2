<template>
    <div class="main_screen">
        <Filters @clicked="filterAirlines" :airlines="searchResult.airlines" />
        <TicketList :flights="filteredResult.flights" />
    </div>
</template>
<script>
import TicketList from './TicketList'
import Filters from './Filters'
import json from '../assets/results.json'
export default {
    components: {
        TicketList,
        Filters
    },
    data() {
        return {
            searchResult: json,
            filteredResult: []
        }
    },
    methods: {
        filterAirlines(filters) {
           this.filteredResult = JSON.parse(JSON.stringify(this.searchResult))
            if(filters.length > 0) {
             this.filteredResult.flights = this.filteredResult.flights.filter(flight=> filters.includes(flight.itineraries[0][0].carrier))
            }else {
                this.filteredResult.flights = []
            }
            
        }
    },
    created() {
        this.filteredResult = JSON.parse(JSON.stringify(this.searchResult))
    }
}
</script>
<style scoped>
.main_screen {
    width: 80%;
    height: 100vh;
    background-color: #D7D7D7;;
    margin: 0 auto;
    padding: 5em 0;
    display: flex;
    
}
</style>