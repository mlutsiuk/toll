<template>
    <brand-tabs
        :headers="tabHeaders"
    >
        <template #tab-passenger>
            <passenger-car-calculator/>
        </template>
        <template #tab-truck>
            <truck-calculator/>
        </template>
    </brand-tabs>
</template>

<script>
import BrandTabs from '@/components/Shared/BrandTabs';
import PassengerCarCalculator from '@/components/TollCalculator/PassengerCarCallculator';
import TruckCalculator from "@/components/TollCalculator/TruckCalculator";

export default {
    name: 'TollCalculator',
    components: {
        TruckCalculator,
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
