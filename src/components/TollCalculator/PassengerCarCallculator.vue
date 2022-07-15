<template>
    <div>
        <div class="flex-row">
            <div class="col-xs-6 col-lg-2 flex-row flex-align-items-center">
                <engine-type-radio v-model:engine-type="engineType"/>
            </div>

            <div class="col-xs-6 col-lg-4">
                <label for="engine_volume">Вартість автомобіля</label>
                <div class="input-group input-group-lg">
                    <input v-model="carPrice" id="car_price" type="text" class="form-control">
                    <div class="input-group-addon">EUR</div>
                </div>
            </div>

            <div class="col-xs-6 col-lg-4">
                <label for="engine_volume">Об'єм двигуна</label>
                <div class="input-group input-group-lg">
                    <input v-model="engineVolume" id="engine_volume" type="text" class="form-control">
                    <div class="input-group-addon">см<sup>3</sup></div>
                </div>
            </div>

            <div class="col-xs-6 col-lg-2">
                <manufacture-date-select v-model:age="carAge"/>
            </div>
        </div>

        <results-table
            :excise="{
                base: engineVolume,
                rate: `${carAge}×${exciseRate}`,
                sum: exciseSum
            }"
            :impost="{
                base: carPrice,
                rate: impostRate,
                sum: impostSum
            }"
            :pdv="{
                base: pdvBase,
                rate: pdvRate,
                sum: pdvSum
            }"
            :total-sum="totalSum"
        />
    </div>
</template>

<script>
import ManufactureDateSelect from "@/components/Shared/ManufactureDateSelect";
import EngineTypeRadio from "@/components/Shared/EngineTypeRadio";
import ResultsTable from "@/components/TollCalculator/ResultsTable";
import { rates, engineTypes } from '@/data/constants.json';

export default {
    name: 'PassengerCarCalculator',
    components: {
        ResultsTable,
        EngineTypeRadio,
        ManufactureDateSelect
    },
    data: () => ({
        engineType: '',
        engineVolume: '',
        carAge: 1,
        carPrice: 0,
    }),
    computed: {
        impostRate() {
            return rates.impost;
        },
        impostSum() {
            return (parseInt(this.carPrice) * (this.impostRate / 100.0)) || 0;
        },

        exciseRate() {
            let parsedEngineVolume = parseInt(this.engineVolume);

            if (this.engineType === engineTypes.diesel) {
                return parsedEngineVolume <= 3500 ? 75 : 150;
            } else if (this.engineType === engineTypes.benzine) {
                return parsedEngineVolume <= 3000 ? 50 : 100;
            }

            return 0;
        },
        exciseSum() {
            let engineVolumeInLiters = parseInt(this.engineVolume) / 1000;

            return (engineVolumeInLiters * this.exciseRate * this.carAge) || 0;
        },

        pdvRate() {
            return rates.pdv;
        },
        pdvBase() {
            return parseInt(this.carPrice) + this.exciseSum + this.impostSum;
        },
        pdvSum() {
            return (this.pdvBase * (this.pdvRate / 100.0)) || 0;
        },

        totalSum() {
            return this.exciseSum + this.impostSum + this.pdvSum;
        }

    }
};
</script>

<style scoped>
.flex-row {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    margin-right: -15px;
}

.flex-align-items-center {
    -ms-flex-align: center !important;
    align-items: center !important;
}
</style>