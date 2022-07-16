<template>
    <div>
        <div class="flex-row fields-row">
            <div class="col-xs-4">
                <label for="engine_volume">Вартість автомобіля</label>
                <div class="input-group input-group-lg">
                    <input v-model="carPrice" id="car_price" type="text" class="form-control">
                    <div class="input-group-addon">EUR</div>
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
            return (this.pdvBase * (this.pdvRate / 100.0)) || 0;
        },

        totalSum() {
            return this.impostSum + this.pdvSum;
        }
    },

}
</script>

<style scoped>
.flex-row {
    display: -ms-flexbox;
    display: flex;
    -ms-flex-wrap: wrap;
    flex-wrap: wrap;
    /*margin-right: -15px;*/
}

.fields-row {
    margin-bottom: 15px;
}
</style>