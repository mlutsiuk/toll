<template>
    <div class="container">
        <brand-tabs
            :headers="tabHeaders"
        >
            <template #tab-diesel>
                <h2>Diesel</h2>
                <diesel-calculator/>
            </template>
            <template #tab-benzine>
                <h2>Benzine</h2>
            </template>
        </brand-tabs>
    </div>
</template>

<script>
import BrandTabs from '@/components/Shared/BrandTabs';
import DieselCalculator from '@/components/TollCalculator/DieselCalculator';

export default {
    name: 'TollCalculator',
    components: {
        DieselCalculator,
        BrandTabs
    },
    data: () => ({
        tabHeaders: [
            {
                id: 'benzine',
                title: 'Бензин'
            },
            {
                id: 'diesel',
                title: 'Дизель'
            }
        ]
    })
};
</script>

<style scoped>

</style>
