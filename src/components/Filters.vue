<template>
    <div class="filters">
        <div class="filter-rates">
            <div class="filter-title">Опции тарифа</div>
            <div class="filter-list">
                <div class="filter-item">
                    <Checkbox id="1"/>
                    <span class="filter-item_text">Только прямые</span>
                </div>
                <div class="filter-item">
                    <Checkbox id="2" />
                    <span class="filter-item_text">Только с багажом</span>
                </div>
                <div class="filter-item">
                    <Checkbox id="refundable"/>
                    <span class="filter-item_text">Только возвратные</span>
                </div>
            </div>
        </div>
        <div class="filter-carriers">
            <div class="filter-title">Авиакомпании</div>
            <div class="filter-carriers_all">
                <div class="filter-item">
                    <Checkbox @clicked="selectAll" id="airline-all" :checked="checked" />
                    <span class="filter-item_text">Все</span>
                </div>
            </div>
            <div class="filter-list_carriers" >
                <div class="filter-item" v-for="(airline, index) in airlines" :key="index">
                    <Checkbox @clicked="addFilter" :id="index" :checked="checked" />
                    <span class="filter-item_text">{{ airline }}</span>
                </div>
            </div>
        </div>
        <div class="reset-filters">Сбросить все фильтры</div>
    </div>
</template>
<script>
import Checkbox from './Checkbox'
export default {
    name: 'Filters',
    props: {
        airlines: {
            type: Object
        }
    },
    components: {
        Checkbox
    },
    data() {
        return {
            filters: [],
            checked: false
        }
    },
    methods: {
        addFilter(value, isAddFilter) {
            
            if(isAddFilter) {
                this.filters.push(value)
            }else {
                this.filters = this.filters.filter(item=> item !== value)
            }
            this.$emit('clicked', this.filters)
        },
        selectAll(value, isAddFilter) {
            this.checked = !this.checked
            if(isAddFilter) {
                 this.filters = Object.keys(this.airlines)
                 
            }else {
                this.filters = []
            }
            this.$emit('clicked', this.filters)
           
        },
    },
    created() {
        this.selectAll("airline-all", true)
    }
    
}
</script>
<style scoped>
.filters {
    flex: 0 1 240px;
}
.filter-title {
    margin-bottom: 0.75em;
    color: #202123;
    font-weight: 700;
    line-height: 1.25em;
}
.filter-rates {
    background-color: #F5F5F5;
    border-radius: 4px;
    padding: 0.75em;
    margin-bottom: 0.75em;
}
.filter-carriers {
    background-color: #F5F5F5;
    border-radius: 4px;
    padding: 0.75em;
    padding-right: 4px;
    height: 20em;
    position: relative;
    overflow-y: hidden;
   
}
.filter-list_carriers {
    overflow-y: auto;
    height: 80%;
}


.filter-list_carriers::-webkit-scrollbar {
  width: 2px;
  background-color: #F5F5F5;
}

.filter-list_carriers::-webkit-scrollbar-thumb {
  border-radius: 2px;
  -webkit-box-shadow: inset 0 0 6px rgba(0, 0, 0, .3);
  box-shadow: inset 0 0 6px rgba(0, 0, 0, .3);
  background-color: #E1E1E1;
  cursor: pointer;
}
.filter-item {
    display: flex;
    line-height: 1em;
    padding: 0.5em 0;
}
.filter-item:hover {
    cursor: pointer;
}
.filter-item_text {
    margin-left: 0.75em;
}
.reset-filters {
    color: #7284E4;
    display: inline-block;
    border-bottom: 1px dashed #7284E4;
    margin-top: 0.75em;
}

</style>