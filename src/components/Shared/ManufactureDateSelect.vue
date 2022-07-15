<template>
    <div>
        <div class="form-group input-group-lg">
            <label for="car_manufacture_year">Рік виготовлення</label>
            <select
                id="car_manufacture_year"
                v-model="ageModel"
                class="form-control"
            >
                <option v-for="year in years" :value="year.value" :key="year.value">
                    {{ year.text }}
                </option>
            </select>
        </div>
    </div>
</template>

<script>
import { maxCarAgeModifier } from "@/data/constants.json";

export default {
    name: "ManufactureDateSelect",
    props: {
        age: {
            type: Number,
            required: true
        }
    },
    emits: [
        'update:age'
    ],
    computed: {
        ageModel: {
            get() {
                return this.age;
            },
            set(val) {
                this.$emit('update:age', val);
            }
        },
        years() {
            let currentYear = new Date().getFullYear();
            let years = [];

            for (let year = currentYear; year >= currentYear - maxCarAgeModifier; year--) {
                let age = currentYear - year;

                years.push({
                    text: year,
                    value: age < 1 ? 1 : age,
                })
            }

            years.push({
                text: 'Старіша',
                value: maxCarAgeModifier
            });
            return years;
        }
    },
    mounted() {
        this.ageModel = this.years[0].value;
    }
}
</script>