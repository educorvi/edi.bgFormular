<template>
    <div id="bar">
        <b-navbar toggleable="lg">
            <b-navbar-brand :to="'/'" class="mr-5">
                <b-img id="logo" src="img/logoS.png"/>
                Formulare
            </b-navbar-brand>
        </b-navbar>
    </div>

</template>

<script>
    //@group Navigation
    //@vuese
    //Navbar zur Navigation

    export default {
        name: "Headbar",
    }
</script>

<style scoped>
    #logo {
        height: 40px;
    }

    #bar {
        position: sticky;
        /* fixing the position takes it out of html flow - knows
                          nothing about where to locate itself except by browser
                          coordinates */
        left: 0; /* top left corner should start at leftmost spot */
        top: 0; /* top left corner should start at topmost spot */
        /*width: 100vw; !* take up the full browser width *!*/
        z-index: 200; /* high z index so other content scrolls underneath */
        background: white;
    }
</style>
