<template>
    <v-navigation-drawer id = "drawer"
                         v-model="drawer"
                         :mini-variant.sync="mini"
                         hide-overlay
                         stateless
                         v-bind:width="400"
    >
        <v-toolbar flat class="transparent">
            <v-list class="pa-0">
                <v-list-tile avatar>
                    <v-list-tile-avatar>
                        <img src="https://cdn.iconscout.com/icon/free/png-256/nasa-282190.png">
                    </v-list-tile-avatar>
                    <v-list-tile-content>
                        <v-list-tile-title>Web Map Menu</v-list-tile-title>
                    </v-list-tile-content>
                    <v-list-tile-action>
                        <v-btn
                                icon
                                @click.stop="mini = !mini"
                        >
                            <v-icon>chevron_left</v-icon>
                        </v-btn>
                    </v-list-tile-action>
                </v-list-tile>
                <v-divider></v-divider>
                <!--                <v-list-group-->
                <v-divider></v-divider>
                <v-list-group
                        :value="false"
                >
                    <template v-slot:activator>
                        <v-list-tile>
                            <v-list-tile-avatar>
                                <v-btn
                                        icon
                                        @click.stop="mini = !mini"
                                >
                                    <v-icon>{{items[0].icon}}</v-icon>
                                </v-btn>
                            </v-list-tile-avatar>
                            <v-list-tile-content>
                                <v-list-tile-title>{{items[0].title}}</v-list-tile-title>
                            </v-list-tile-content>
                        </v-list-tile>
                    </template>
                    <v-list-tile
                            v-for="(bookmarks, i) in bookmarks"
                            :key="i"
                            @click= ""
                            v-on:click="emitBookMark(bookmarks[0])"
                    >
                        <!--                        trying to toggle between bookmarks-->
                        <v-list-tile-title v-text="bookmarks[0]"></v-list-tile-title>
                        <v-list-tile-action>
                            <v-icon v-text="bookmarks[1]"></v-icon>
                        </v-list-tile-action>
                    </v-list-tile>
                </v-list-group>
                <v-list-group
                        :value="false"
                >
                    <!--                        prepend-icon="map"-->
                    <template v-slot:activator>
                        <v-list-tile>
                            <v-list-tile-avatar>
                                <v-btn
                                        icon
                                        @click.stop="mini = !mini"
                                >
                                    <v-icon>{{items[1].icon}}</v-icon>
                                </v-btn>
                            </v-list-tile-avatar>
                            <v-list-tile-content>
                                <v-list-tile-title>{{items[1].title}}</v-list-tile-title>
                            </v-list-tile-content>
                        </v-list-tile>
                    </template>
                    <v-list-tile
                            v-for="(basemap1, i) in basemap1"
                            :key="i"
                            @click= ""
                            v-on:click="emitLayer(basemap1[2])"
                    >
                        <!--                        trying to toggle between basemaps-->
                        <v-list-tile-title v-text="basemap1[0]"></v-list-tile-title>
                        <v-list-tile-action>
                            <v-icon v-text="basemap1[1]"></v-icon>
                        </v-list-tile-action>
                    </v-list-tile>
                </v-list-group>
                <!--                </v-list-group>-->
                <v-list-group
                        :value="false">
                    <template v-slot:activator>
                        <v-list-tile>
                            <v-list-tile-avatar>
                                <v-btn
                                        icon
                                        @click.stop="mini = !mini"
                                >
                                    <v-icon>{{items[2].icon}}</v-icon>
                                </v-btn>
                            </v-list-tile-avatar>
                            <v-list-tile-content>
                                <v-list-tile-title>Data Layers</v-list-tile-title>
                            </v-list-tile-content>
                        </v-list-tile>
                    </template>
                    <!--                    The code for each all check boxes starts here-->
                    <v-list-tile
                            v-for="(eachLayer, i) in layers"
                            :key="i"
                            @click="emitToggleLayer(eachLayer)"
                            v-on:click= "eachLayer[2] = !eachLayer[2]"
                    >
                        <v-list-tile-action>
                            <v-checkbox></v-checkbox>
                        </v-list-tile-action>
                        <v-list-tile-content>
                            <v-list-tile-title v-text="eachLayer[0]"></v-list-tile-title>
                        </v-list-tile-content>
                    </v-list-tile >
                    <!--                    end of the first chunk of code for the checkbox-->
                </v-list-group>
<!--                openScene() opens the 3D model-->
<!--                <v-list-tile @click="onClick">-->
<!--                    &lt;!&ndash;                    not calling any function or printing anything out to the console, so unable to work on toggling the sheet for scene&ndash;&gt;-->
<!--                    <v-list-tile-avatar>-->
<!--                        <v-btn-->
<!--                                icon-->
<!--                                @click.stop="mini = !mini"-->
<!--                        >-->
<!--                            <v-icon>{{items[3].icon}}</v-icon>-->
<!--                        </v-btn>-->
<!--                    </v-list-tile-avatar>-->
<!--                    <v-list-tile-content>-->
<!--                        <v-list-tile-title>{{items[3].title}}</v-list-tile-title>-->
<!--                    </v-list-tile-content>-->
<!--                </v-list-tile>-->
                <v-list-tile v-on:click="openAbout()">
                    <v-list-tile-avatar>
                        <v-btn
                                icon
                                @click.stop="mini = !mini"
                        >
                            <v-icon>{{items[3].icon}}</v-icon>
                        </v-btn>
                    </v-list-tile-avatar>
                    <v-list-tile-content>
                        <v-list-tile-title>{{items[3].title}}</v-list-tile-title>
                    </v-list-tile-content>
                </v-list-tile>
            </v-list>
        </v-toolbar>
    </v-navigation-drawer>
</template>
<script>
    //import Header from './components/Header.vue';
    //import scene from 'components/scene.vue';
    export default {
        name: "Navigation",
        props:
            {
                width: 400
            },
        data() {
            return {
                drawer: true,
                items: [
                    {title: 'Bookmarks', icon: 'bookmark'},
                    {title: 'Basemaps', icon: 'map'},
                    {title: 'Data Layers', icon: 'layers'},
                    //embed sliders to data layers
                    //have sliders pop up on screen when new data layer added
                    // { title: 'Opacity', icon: 'opacity' },
                    // {title: '3D Scene', icon: '3d_rotation'},
                    {title: 'About', icon: 'info'}
                ],
                basemap1: [
                    ['Default', 'map', 'topo'],
                    ['Street', 'map', 'streets'],
                    ['Aerial', 'map', 'aerials']//,
                    //['Google Imagery', 'map', 'google']
                ],
                layers: [
                    //made navigation drawer a little wider so that the snowmelt layer is completely shown
                    ['Change in Snowmelt Timing\n(1975-2040)', 'layers', false, 'esriSnowLayer'],
                    ['Population Density', 'layers', false, 'popDenseLayer'],
                    ['Rain Gauges', 'layers', false, 'rainGuagesLayer'],
                    ['Precipitation Change by 2050', 'layers', false, 'precipitationLayer']
                ],
                bookmarks: [
                    ['United States', 'bookmark'],
                    ['California', 'bookmark'],
                    ['Florida', 'bookmark'],
                    ['Texas', 'bookmark'],
                ],
                mini: true,
                right: null,
            }
        },
        methods:{
            emitLayer: function(layer){
                this.$eventHub.$emit('toggleMapLayers', layer);
            },
            emitBookMark: function(bookmark){
                this.$eventHub.$emit('goToBookmarks', bookmark);
            },
            // emitReset: function() {
            //     this.$eventHub.$emit('resetMap');
            // },
            emitToggleLayer: function(layer) {
                // if(!layer[2]) {
                //     this.$eventHub.$emit('layerOn', layer);
                //     console.log("layer on emitted");
                // }
                // else
                //     this.$eventHub.$emit('layerOff', layer);
                this.$eventHub.$emit('toggleLayer', layer);
                console.log("layer on emitted");
            },
            openAbout: function(){
                this.$eventHub.$emit('openAbout');
            }//,
            // onClick: function(){
            //     this.$eventHub.$emit('openScene');
            //     console.log("started onClick() function");
            //     // the three latter numbers are the x,y,z coordinates, respectively
            //     this.$emit('clicked', '34568765', '-1222', '4565');
            //     console.log("emitted clicked");
            //     this.$eventHub.$emit('openBox');
            //     console.log("emitted openBox");
            // }
        }//,
        // components:
        //     {
        //         scene
        //     }
    }
</script>
<style scoped>
    #drawer{
        z-index: 1010;
        position: absolute;
        top: 75px;
        left: 0px;
    }
</style>
