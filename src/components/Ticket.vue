<template>
    <div class="ticket">
        <div class="ticket-info">
            <div class="ticket-info_details">
                 <div class="ticket-carrier_logo">
                    <img :src="logoUrl + flight.itineraries[0][0].carrier + '.png'" alt="" srcset="">
                    </div>
                    <div class="ticket-carrier_name">{{ flight.itineraries[0][0].carrier_name }}</div>
                    <div class="ticket-depart_date">
                        <div class="ticket-depart_date-day">{{flight.itineraries[0][0].segments[0].dep_time | setDay}}</div>
                        <div class="ticket-depart_date-time">{{flight.itineraries[0][0].segments[0].dep_time | setTime}}</div>
                    </div>
                    <div class="ticket-timeline">
                        <div class="ticket-timeline_item" v-for="(segment, index) in flight.itineraries[0][0].segments.length + 1" :key="index">
                            <span class="ticket-timeline_item-depart" v-if="index==0">{{ flight.itineraries[0][0].segments[0].dest_code }}</span>
                            <span class="ticket-timeline_item-arrive" v-if="index==flight.itineraries[0][0].segments.length">{{flight.itineraries[0][0].segments.length > 1 ? flight.itineraries[0][0].segments[flight.itineraries[0][0].segments.length -1].dest_code : flight.itineraries[0][0].segments[flight.itineraries[0][0].segments.length -1].origin_code}}</span>
                        </div>
                    </div>
                    <div class="ticket-arrive_date">
                        <div class="ticket-arrive_date-day">{{flight.itineraries[0][0].segments[0].arr_time | setDay}}</div>
                        <div class="ticket-arrive_date-time">{{flight.itineraries[0][0].segments[0].arr_time | setTime}}</div>
                    </div>
            </div>
       
        <div class="ticket-info_desctiprion">
            <span class="ticket-description_details">Детали перелета</span>
            <span class="ticket-description_conditinons">Условия тарифа</span>
            <span class="ticket-description_restore">Невозвратный</span>
        </div>
        </div>
        <div class="ticket-price">
            <div class="ticket-price_text">{{flight.price}} ₸</div>
            <Button label="Выбрать" />
            <div class="ticket-price_description">
                Цена за всех пассажиров
            </div>
            <div class="ticket-price_baggage">
                <span class="ticket-price_baggage-info">Нет багажа</span>
                <span class="ticket-price_baggage-add">+Добавить багаж</span>
            </div>
        </div>
    </div>
</template>
<script>
import Button from './Button'
export default {
    props: {
        flight: {
            type: Object
        }
    },
    components: {
        Button
    },
    data() {
        return {
            logoUrl: "https://aviata.kz/static/airline-logos/80x80/",
            weekDays: {
                1: "пн",
                2: "вт",
                3: "ср",
                4: "чт",
                5: "пн",
                6: "суб",
                7: "вс"
            }
        }
    },
    filters: {
        setDay(time) {
            const dayArray = time.split(' ')
            return `${dayArray[0]} ${dayArray[1]} ${dayArray[2].toLowerCase()}`
        },
        setTime(time) {
             const dayArray = time.split(' ')
             return dayArray[dayArray.length - 1]
        }
    },
    
}
</script>
<style scoped>
.ticket {
   background-color: #fff;
   padding-left: 2.75em;
   display: flex;
   border-radius: 4px;
}
.ticket-info {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;
    padding-top: 2.5em;
    padding-right: 6.25em;

}
.ticket-info_details {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    margin-bottom: 2.875em;
    width: 100%;
}
.ticket-carrier_logo {
    width: 1.5em;
    height: 2em;
}
.ticket-carrier_logo img{
    width: 100%;
}
.ticket-carrier_name {
    color:#202123;
    font-size: 0.875em;
    font-weight: 600;
    min-width: 100px;
    margin: 0 0.75em;
}
.ticket-depart_date {
    color: #202123;
    margin-right: 1.75em;
}
.ticket-arrive_date {
    color: #202123;
    margin-left: 1.75em;
}

.ticket-depart_date-day, .ticket-arrive_date-day {
    font-size: 0.75em;
    line-height: 1em;
    font-weight: 400;
}
.ticket-depart_date-time, .ticket-arrive_date-time {
    font-size: 1.5em;
    line-height: 1.2em;
    font-weight: 600;
}

.ticket-timeline {
    width: 100%;
    flex: 1 0 180px;
    position: relative;
    display: flex;
    justify-content: space-between;

}
.ticket-timeline::after {
    content: "";
    width: 100%;
    height: 0.1px;
    position: absolute;
    top: 5px;
    background-color: #B9B9B9;
    z-index: 1;
}
.ticket-timeline_item {
    width: 10px;
    height: 10px;
    background-color: #fff;
    border: 1px solid #B9B9B9;
    border-radius: 50%;
    z-index: 2;
    position: relative;
}
.ticket-timeline_item span {
    position: absolute;
   
    color: #B9B9B9;
    font-size: 0.625em;
}
.ticket-timeline_item-depart {
    top: -15px;
}
.ticket-timeline_item-arrive {
    top: -15px;
    left: -15px;
}
/* .ticket-timeline::before {
    content: "";
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background-color: black;
} */
.ticket-info_desctiprion {
    width: 100%;
    display: flex;
    align-items: flex-end;
}
.ticket-info_desctiprion span {
    margin-right: 1.5em;
}
.ticket-description_details, .ticket-description_conditinons {
    color: #7284E4;
    border-bottom: 1px dashed #7284E4;
}
.ticket-price {
    background-color: #F5F5F5;
    flex-basis: 30%;
    padding: 1.25em;
    border-top-right-radius: 4px;
    border-bottom-right-radius: 4px;
    
}
.ticket-price_text {
    color: #202123;
    font-size: 1.5em;
    line-height: 1.75em;
    font-family: Arial;
    text-align: center;
    margin-bottom: 0.75em;
}
.ticket-price_description {
    text-align: center;
    color: #707276;
    font-size: 0.75em;
    margin-top: 0.5em;
}

.ticket-price_baggage {
    margin-top: 0.75em;
    text-align: center;
    font-size: 0.75em;
}
.ticket-price_baggage-add {
    color: #5763B3;
    margin-left: 0.875em;
}
</style>