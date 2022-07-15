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

                <truck-calculator/>
            </template>
        </brand-tabs>
    </div>
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
