<template>
    <div class="select">
        <input class="block" v-if="searchLine" type="text" @input="$emit('input', $event.target.value); inputFilter($event);" />
        <select class="block">
            <option v-for="(e,i) in mass" :key="i">{{e.value}}</option>
        </select>
    </div>
</template>

<script>
export default {
    props: {
        source: Array,
        searchLine: {
            type: Boolean
        },
        allowEmpty: Boolean
    },
    data: function(){
        return {
            inputMessage: "",
            mass: []
        }
    },
    mounted: function() {
        this.mass = this.source;
    },
    watch: {
        allowEmpty: function() {
            this.refreshSelect();
        }
    },
    computed: {
        newSource: {
            get: function () {
                return this.massEmpty();
            },
            set: function(newValue) {
                this.mass = newValue;
            } 
        }
    },
    methods: {
        inputFilter: function(event) {
            let mass = this.massEmpty();
            this.mass = mass.filter(e => e.value.indexOf(event.target.value) !== -1);
        },
        massEmpty: function() {
            this.mass = this.source;
            if (!this.allowEmpty) {
                return this.mass.filter(e => e.value.length > 0);
            } else {
                return this.mass;
            }
        },
        refreshSelect: function() {
            this.mass = this.massEmpty();
        }
    }
}
</script>

<style lang="scss" scoped>
.select {
    display: flex;
    justify-content: center;

    :active, :hover, :focus {
        outline: 0;
        outline-offset: 0;
    }

    .block {
        font-size: 13px;
        padding: 6px 0 4px 10px;
        border: 1px solid #cecece;
        background: #F6F6f6;
    }

    input {
        border-radius: 3px 0px 0px 3px;
        width: 300px;
    }

    select {
        border-radius: 0px 3px 3px 0px;
        min-width: 150px;
        cursor: pointer;
    }
}
</style>