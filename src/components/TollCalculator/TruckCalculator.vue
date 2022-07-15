<template>
    <div>
        <div class="row">
            <div class="col">
                <label for="engine_volume">Вартість автомобіля</label>
                <div class="input-group mb-2 mr-sm-2">
                    <input v-model="carPrice" id="car_price" type="text" class="form-control">
                    <div class="input-group-append">
                        <div class="input-group-text">EUR</div>
                    </div>
                </div>
            </div>
        </div>

        <results-table
            :excise="{
                base: 0,
                rate: 0,
                sum: 0
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
import ResultsTable from "@/components/TollCalculator/ResultsTable";
import { rates } from "@/data/constants.json";

export default {
    name: "TruckCalculator",
    components: {
        ResultsTable
    },
    data() {
        return {
            carPrice: 0
        }
    },
    computed: {
        impostRate() {
            return rates.impost;
        },
        impostSum() {
            return this.carPrice * (this.impostRate / 100.0);
        },

        pdvRate() {
            return rates.pdv;
        },
        pdvBase() {
            return parseInt(this.carPrice) + this.impostSum;
        },
        pdvSum() {
            return this.pdvBase * (this.pdvRate / 100.0);
        },

        totalSum() {
            return this.impostSum + this.pdvSum;
        }
    },

}
</script>