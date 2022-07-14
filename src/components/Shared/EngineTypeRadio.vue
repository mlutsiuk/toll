<template>
    <div>
        <div
            v-for="type in types"
            :key="type.code"
            class="custom-control custom-radio"
        >
            <input
                type="radio"
                :value="type.code"
                v-model="engineTypeModel"
                :id="'engine_type_radio_' + type.code"
                name="engine_type_radio"
                class="custom-control-input"
            >
            <label
                v-text="type.title"
                :for="'engine_type_radio_' + type.code"
                class="custom-control-label"
            />
        </div>
    </div>
</template>

<script>
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
                code: 'benzine'
            },
            {
                title: 'Дизель',
                code: 'diesel'
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