<template>
    <div class="container">
        <brand-tabs
            :headers="tabHeaders"
        >
            <template #tab-passenger>
                <h2>Легковий</h2>

                <passenger-car-calculator/>
            </template>
            <template #tab-truck>
                <h2>Тягач</h2>


            </template>
        </brand-tabs>
    </div>
</template>

<script>
import BrandTabs from '@/components/Shared/BrandTabs';
import PassengerCarCalculator from '@/components/TollCalculator/PassengerCarCallculator';

export default {
    name: 'TollCalculator',
    components: {
        PassengerCarCalculator,
        BrandTabs
    },
    data: () => ({
        tabHeaders: [
            {
                id: 'passenger',
                title: 'Легковий'
            },
            {
                id: 'truck',
                title: 'Тягач'
            }
        ]
    })
};
</script>
