<template>
    <div>
        <div
            v-for="type in types"
            :key="type.code"
            class="radio"
        >

            <label>
                <input
                    v-model="engineTypeModel"
                    :value="type.code"
                    type="radio"
                    name="engine_type_radio"
                >
                {{ type.title }}
            </label>
        </div>
    </div>
</template>

<script>
import { engineTypes } from '@/data/constants.json';

export default {
    name: "EngineTypeRadio",
    emits: [
        'update:engine-type'
    ],
    props: {
        engineType: {
            type: String,
            required: true
        },
    },
    data: () => ({
        types: [
            {
                title: 'Бензин',
                code: engineTypes.benzine
            },
            {
                title: 'Дизель',
                code: engineTypes.diesel
            }
        ]
    }),
    computed: {
        engineTypeModel: {
            get() {
                return this.engineType;
            },
            set(val) {
                this.$emit('update:engine-type', val);
            }
        }
    },
    mounted() {
        this.engineTypeModel = this.types[0].code;
    }
}
</script>