<template>
    <Page backgroundColor="#000000" @loaded="view_results" actionBarHidden="true">
         <ListView row="1" marginTop="5%" @itemTap="onItemTap"
            for="result in resultss">
            <v-template>
                    <Label height="20" :text="addmov(result)"/>
            </v-template>
        </ListView>
    </Page>
</template>
<script>
import Movie from './Movie'
export default {
    props: ["results"],
    data(){
        return{
            resultss: this.results.result
        }
    },
    methods: {
        addmov(result){
            var title = result.title
            var year
            
            if (result.year == undefined){
                if(result.release_date != null){
                var date = result.release_date.split("-")
                year = date[0]
                }
                else year = "0"
            }
            else year = result.year
            return `${title} (${year})`
        },

        onItemTap(args){

           
                this.$navigateTo(Movie, {
                       transition: {
                           name: "slideLeft",
                           duration: 200
                       }, 
                       props: {
                         imdb_id: this.resultss[args.index].imdb_id
                       }
                     });
           },
    }
}
</script>