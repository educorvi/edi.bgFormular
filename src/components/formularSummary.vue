<template>
    <b-card style="border-radius: 0" class="summary">
        <div id="funky" @click="toggleOpen=!toggleOpen">
                <h4 :class="toggleOpen?'open':''">{{formular.title}}</h4>
        </div>
        <b-collapse :id="'collapse_formular'+index" v-model="toggleOpen" accordion="overview" style="text-align: left">
            <p>{{formular.description}}</p>
            <b-button style="width: fit-content; float: right" variant="primary">Ausfüllen</b-button>
        </b-collapse>
    </b-card>
</template>

<script>
    export default {
        name: "formularSummary",
        props: {
            formular: {
                type: Array,
                required: true
            },
            index: {
                type: Number,
                required: true
            }
        },
        data() {
            return {
                toggleOpen: false
            }
        },
    }
</script>

<style scoped>
    #funky {
        width: 100%;
    }

    #funky > * {
        width: 100%;
        white-space: nowrap;
        transition: width .8s ease;
        cursor: pointer;
    }

    .open {
        width: 0 !important;
    }
</style>
