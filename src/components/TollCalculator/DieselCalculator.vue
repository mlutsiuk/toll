<template>
    <div>
        <h3>{{ engineVolume }}</h3>
        <text-field v-model="engineVolume" id="engine_volume" label="Об'єм двигуна"/>
        <manufacture-date-select v-model:age="carAge"/>
        <text-field v-model="carPrice" id="car_price" label="Ціна автомобіля"/>



        <h4>Акциз - {{ excise }}</h4>
        <h4>Мито - {{ impost }}</h4>
        <h4>ПДВ - {{ PDV }}</h4>
        <hr>
        <h4>Загальна ціна - {{ totalSum }}</h4>
    </div>
</template>

<script>
import TextField from '@/components/Shared/TextField';
import ManufactureDateSelect from "@/components/Shared/ManufactureDateSelect";

export default {
    name: 'DieselCalculator',
    components: {
        ManufactureDateSelect,
        TextField
    },
    data: () => ({
        engineVolume: '',
        carAge: 0,
        carPrice: 0,
        impostRate: 10
    }),
    computed: {
        engineVolumeInLiters() {
            return this.engineVolume / 1000;
        },
        rate() {
            return this.engineVolume < 3500 ? 75 : 150;
        },
        excise() {
            return this.rate * this.engineVolumeInLiters * this.carAge;
        },
        impost() {
            return this.carPrice * (this.impostRate / 100.0);
        },
        PDV() {
            const PDVRate = 20;
            return (parseInt(this.carPrice) + parseInt(this.excise) + parseInt(this.impost)) * (PDVRate / 100.0);
        },
        totalSum() {
            return this.excise + this.impost + this.PDV;
        }

    }
};
</script>
