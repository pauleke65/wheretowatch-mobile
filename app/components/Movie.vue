<template>
    <Page backgroundColor="#000000" @loaded="getdets" actionBarHidden="true">

            <StackLayout marginTop="5%" height="95%">
            <Label fontWeight="bold" :text="title" horizontalAlignment="center" fontSize="40%" textWrap="true" />

            <GridLayout marginTop="3%" rows="auto" columns="auto, auto">
            <Image :src="movieImage" stretch="aspectFill" row="0" col="0" width="50%"/>

            <StackLayout marginLeft="2%" row="0" col="1">
                <Label >
                    <FormattedString>
                    <Span fontSize="17%" fontWeight="bold" text="Year: " textWrap="true" />
                    <Span fontSize="15%" :text="year" textWrap="true" />
                    </FormattedString>
                </Label>
                
                <Label >
                    <FormattedString>
                    <Span fontSize="17%" fontWeight="bold" text="IMDB Rating: " textWrap="true" />
                    <Span fontSize="15%" :text="irating" textWrap="true" />
                    </FormattedString>
                </Label>

                <Label  >
                    <FormattedString>
                    <Span fontSize="17%" fontWeight="bold" text="Age Rating: " textWrap="true" />
                    <Span fontSize="15%" :text="arating" textWrap="true" />
                    </FormattedString>
                </Label>

                <Label  >
                    <FormattedString>
                    <Span fontSize="17%" fontWeight="bold" text="Runtime: " textWrap="true" />
                    <Span fontSize="15%" :text="runtime" textWrap="true" />
                    </FormattedString>
                </Label >

                <Label  >
                    <FormattedString>
                    <Span fontSize="17%" fontWeight="bold" text="Genres: " textWrap="true" />
                    <Span fontSize="15%" :text="genre" textWrap="true" />
                    </FormattedString>
                </Label>

                <Label   textWrap="true">
                    <FormattedString>
                    <Span fontSize="17%" fontWeight="bold" text="Stars: " textWrap="true" />
                    <Span fontSize="15%" :text="stars" textWrap="true" />
                    </FormattedString>
                </Label>

                <Label  >
                    <FormattedString>
                    <Span fontSize="17%" fontWeight="bold" text="Languages: " textWrap="true" />
                    <Span fontSize="15%" :text="language" textWrap="true" />
                    </FormattedString>
                </Label>
              
            </StackLayout>
             
           </GridLayout>

          
           <Label text="Details:" marginTop="5%" horizontalAlignment="left" fontSize="17%" textWrap="true" />
           <Label 
           :text="details" 
           fontSize="20%"

           paddingLeft="2%"
           paddingRight="2%"
           textWrap="true" />

           <GridLayout height="20%" columns="*, *">

               <Button height="55%" background="#db1010" col="0" text="Where to Watch" @tap="wherePage" />
               <Button height="55%" background="#221f1f" col="1" text="Similar Movies" @tap="similarPage" />
               
               
             
           </GridLayout>

        </StackLayout>
<!--            
         <ListView row="1" marginTop="20%" @itemTap="onItemTap"
            for="w in watch">
            <v-template>
                    <GridLayout columns="auto, auto">
                        <Image col="0" :src="w.icon" width="50" stretch="aspectFill" />
                        <Label col="1" fontSize="20%" fontWeight="bold" marginLeft="5%" :text="w.name" textWrap="true" />                        
                    </GridLayout>
            </v-template>
        </ListView>

        <Label text="Similar Movies: " horizontalAlignment="left" fontSize="17%" color="#db1010" marginTop="50" textWrap="true" />
 
        <ListView row="1" marginTop="20%" marginBottom="20%" @itemTap="onItemTap"
            for="w in watch">
            <v-template>
                        <Label fontSize="20%" fontWeight="bold" marginLeft="5%" verticalAlignment="center" :text="w.name" textWrap="true" />                        
            </v-template>
        </ListView> -->
                      
            
         
         
    </Page>
</template>
<script>
import axios from 'axios'
export default {
   props: ["imdb_id"],
    data(){
        return{
            movieImage: "",
            year: "",
            irating: "",
            arating: "",
            runtime: "",
            genre: "",
            stars: "",
            language: "",
            details: "",
            title: ""
        
        }
    },
    methods: {
        getdets(){
             axios({
                     url: "http://192.168.43.103:5000/getdets",
                     method: "POST",
                    data: {
                        imdb_id: this.imdb_id
                     }
                 })
                 .then((r) => {
                     var res = r.data
                     
                     console.log(res)
                    if (res.movieImage.status != "not found"){
                        this.movieImage = res.movieImage.poster
                    }
                    
                    this.year = res.year
                    this.irating = res.irating
                    this.arating = res.arating
                    this.runtime = res.runtime
                    this.genre = res.genre
                    this.stars = res.stars
                    this.language = res.language
                    this.details = res.details
                    this.title = res.title
                    
                 })
                 .catch(e => alert(e))
        }
        
    }
}
</script>