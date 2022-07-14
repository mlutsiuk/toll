<template>
    <div class="row">
        <div class="col-auto d-flex align-items-center pr-5">
            <engine-type-radio v-model:engine-type="engineType"/>
        </div>

        <div class="col">
            <label for="engine_volume">Ціна автомобіля</label>
            <div class="input-group mb-2 mr-sm-2">
                <input v-model="carPrice" id="car_price" type="text" class="form-control">
                <div class="input-group-append">
                    <div class="input-group-text">EUR</div>
                </div>
            </div>
        </div>

        <div class="col">
            <label for="engine_volume">Об'єм двигуна</label>
            <div class="input-group mb-2 mr-sm-2">
                <input v-model="engineVolume" id="engine_volume" type="text" class="form-control">
                <div class="input-group-append">
                    <div class="input-group-text">см<sup>3</sup></div>
                </div>
            </div>
        </div>

        <div class="col">
            <manufacture-date-select v-model:age="carAge"/>
        </div>



<!--        <h4>Акциз - {{ excise }}</h4>-->
<!--        <h4>Мито - {{ impost }}</h4>-->
<!--        <h4>ПДВ - {{ PDV }}</h4>-->
<!--        <hr>-->
<!--        <h4>Загальна ціна - {{ totalSum }}</h4>-->
    </div>
</template>

<script>
import ManufactureDateSelect from "@/components/Shared/ManufactureDateSelect";
import EngineTypeRadio from "@/components/Shared/EngineTypeRadio";

export default {
    name: 'DieselCalculator',
    components: {
        EngineTypeRadio,
        ManufactureDateSelect
    },
    data: () => ({
        engineType: '',
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
