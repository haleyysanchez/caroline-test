<template>
    <v-btn id="button" class="mx-2" fab dark color="indigo" @click="openScene">
        <v-icon dark>add</v-icon>
    </v-btn>
</template>

<script>
    export default {
        name: "Button",
        methods: {
            openScene: function() {
                this.$eventHub.$emit('openScene');
            },
            onClick: function() {
                console.log("started onClick() function");
                // the three latter numbers are the x,y,z coordinates, respectively
                this.$emit('clicked', '34568765', '-1222', '4565');
                console.log("emitted clicked");
                this.$eventHub.$emit('openBox');
                console.log("emitted openBox");
            }
        }
    }
</script>

<style scoped>
    #button{
        z-index: 1021;
        top: 0px;
        right: 9px;
        position: absolute;
    }

</style>