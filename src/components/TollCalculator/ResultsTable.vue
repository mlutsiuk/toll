<template>
    <table class="table table-hover text-center table-striped table-bordered">
        <thead>
        <tr>
            <th scope="col">Платіж</th>
            <th scope="col">Основа</th>
            <th scope="col">Ставка</th>
            <th scope="col">Сума</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <th scope="row">Акциз</th>
            <td>{{ excise.base || 0 }} EUR</td>
            <td>{{ excise.rate }}</td>
            <td>{{ excise.sum.toFixed(2) }} EUR</td>
        </tr>
        <tr>
            <th scope="row">Мито</th>
            <td>{{ impost.base || 0 }} EUR</td>
            <td>{{ impost.rate }}%</td>
            <td>{{ impost.sum.toFixed(2) }} EUR</td>
        </tr>
        <tr>
            <th scope="row">ПДВ</th>
            <td>{{ pdv.base || 0 }} EUR</td>
            <td>{{ pdv.rate }}%</td>
            <td>{{ pdv.sum.toFixed(2) }} EUR</td>
        </tr>
        <tr>
            <th scope="row">Загалом</th>
            <td colspan="2"></td>
            <td class="font-weight-bold">{{ totalSum.toFixed(2) }} EUR</td>
        </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    name: "ResultsTable",
    props: {
        excise: {
            type: Object,
            default: () => ({
                base: '',
                rate: '',
                sum: ''
            }),
            required: true
        },

        impost: {
            type: Object,
            default: () => ({
                base: '',
                rate: '',
                sum: ''
            }),
            required: true
        },
        pdv: {
            type: Object,
            default: () => ({
                base: '',
                rate: '',
                sum: ''
            }),
            required: true
        },

        totalSum: {
            type: Number,
            required: true
        }
    }
}
</script>

<style scoped>
.table td, .table th {
    border: none;
}
</style>