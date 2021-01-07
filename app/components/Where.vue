<template>
    <Page backgroundColor="#000000" @loaded="view_where" actionBarHidden="true">
        <StackLayout marginTop="5%" >
          
       
        <Label textWrap="true">
            <FormattedString>
            <Span fontSize="17%" fontWeight="bold" text="You can watch " textWrap="true" />
            <Span fontSize="15%" :text="title" textWrap="true" />
            <Span fontSize="17%" fontWeight="bold" text=" at these locations" textWrap="true" />
            </FormattedString>
        </Label>
        
         <ListView row="1" height="80%" @itemTap="onItemTap"
            for="w in results">
            <v-template>
                    <GridLayout columns="auto, auto">
                        <Image col="0" :src="w.icon" width="50" stretch="aspectFill" />
                        <Label col="1" fontSize="20%" fontWeight="bold" marginLeft="5%" :text="w.display_name" textWrap="true" />                        
                    </GridLayout>
            </v-template>
        </ListView>
         </StackLayout>
    </Page>
</template>
<script>
var utilityModule = require("utils/utils");
export default {
    props: ["results", "title"],
    data(){
        return{
            //results: ""//this.results.result
            watch: []
        }
    },
    methods: {
        view_where(){
          
        },

        onItemTap(args){
            
            utilityModule.openUrl(this.results[args.index].url)
           },
    }
}
</script>