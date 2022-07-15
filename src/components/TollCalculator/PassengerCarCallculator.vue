<template>
    <div>
        <div class="row">
            <div class="col-auto d-flex align-items-center pr-5">
                <engine-type-radio v-model:engine-type="engineType"/>
            </div>

            <div class="col">
                <label for="engine_volume">Вартість автомобіля</label>
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

import { rates, engineTypes } from '@/data/constants.json';
import ResultsTable from "@/components/TollCalculator/ResultsTable";

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
            return parseInt(this.carPrice) * (this.impostRate / 100.0);
        },

        exciseRate() {
            let parsedEngineVolume = parseInt(this.engineVolume);

            if (this.engineType === engineTypes.diesel) {
                return parsedEngineVolume <= 3500 ? 75 : 150;
            }
            else if(this.engineType === engineTypes.benzine) {
                return parsedEngineVolume <= 3000 ? 50 : 100;
            }

            return 0;
        },
        exciseSum() {
            let engineVolumeInLiters = parseInt(this.engineVolume) / 1000;

            return (engineVolumeInLiters * this.exciseRate *  this.carAge) || 0;
        },

        pdvRate() {
            return rates.pdv;
        },
        pdvBase() {
            return parseInt(this.carPrice) + this.exciseSum + this.impostSum;
        },
        pdvSum() {
            return this.pdvBase * (this.pdvRate / 100.0);
        },

        totalSum() {
            return this.exciseSum + this.impostSum + this.pdvSum;
        }

    }
};
</script>
