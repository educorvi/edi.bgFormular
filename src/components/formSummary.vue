<template>
    <b-card style="border-radius: 0" class="summary">
        <div :class="!tooLong?'funky':''" @click="toggleOpen=!toggleOpen">
                <h5 :class="toggleOpen&&!tooLong?'open':''">{{formular.title}}</h5>
        </div>
        <b-collapse :id="'collapse_formular'+index" v-model="toggleOpen" accordion="overview" style="text-align: left">
            <p>{{formular.description}}</p>
            <b-button style="width: fit-content; float: right" variant="primary" :to="'/forms/'+formular.id">Ausfüllen</b-button>
        </b-collapse>
    </b-card>
</template>

<script>
    export default {
        name: "formularSummary",
        props: {
            formular: {
                type: Object,
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
        computed: {
            tooLong: function () {
                return this.formular.title.length > 24 && (Math.max(document.documentElement.clientWidth || 0, window.innerWidth || 0) < 700);
            }
        }
    }
</script>

<style scoped>
        .funky {
            width: 100%;
        }

        .funky > * {
            width: 100%;
            white-space: nowrap;
            transition: width .8s ease;
            cursor: pointer;
        }

        .open {
            width: 0 !important;
        }
</style>
