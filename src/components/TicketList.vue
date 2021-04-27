<template>
    <transition-group name="list" tag="ul" class="tickets">
        <li class="ticket-item" v-for="flight in flights" :key="flight.id" >
            <Ticket :flight="flight" />
        </li>
    </transition-group>
</template>
<script>
import Ticket from './Ticket'
export default {
    props: {
        flights: {
            type: Array
        }

    },
    components: {
        Ticket
    },
}
</script>
<style scoped>
.tickets {
    list-style: none;
    flex: 1 1;
    margin-left: 1.75em;
}
.ticket-item {
    margin-bottom: 0.75em;
}
.list-enter {
    opacity: 0;
    transform: translateX(30px);
}
.list-leave-to {
    transform: translateX(30px);
}
.ticket-item {
    transition: all 1s;
}
</style>