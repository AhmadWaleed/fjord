<template>
    <b-col :cols="responsiveCols">
        <b-row>
            <component
                v-for="(c, key) in component"
                :key="key"
                :is="c.name"
                v-bind="{ ...c.props, ...attrs(c.props) }"
                v-on="$listeners"
            />
        </b-row>
    </b-col>
</template>

<script>
export default {
    name: 'FormCol',
    props: {
        component: {
            type: Array,
            default() {
                return [];
            }
        },
        cols: {
            type: [String, Number],
            default() {
                return 12;
            }
        }
    },
    computed: {
        responsiveCols() {
            if (typeof this.cols == 'number') {
                return this.bCols(this.cols);
            } else {
                return this.cols;
            }
        }
    },
    methods: {
        attrs(props) {
            let attrs = this.$attrs;
            for (let name in props) {
                delete attrs[name];
            }
            return attrs;
        }
    }
};
</script>
