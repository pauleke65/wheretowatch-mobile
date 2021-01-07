<template>
    <Page actionBarHidden="true" backgroundColor="#000000">

        <StackLayout>
          <TextField color="black" class="field" marginTop="45%" v-model="movie_search" paddingLeft="10%" hint="Enter Movie Name..."/>
          <Button backgroundColor="#DB0000" marginTop="0" @tap="searchMovie" width="60%" class="btn-main" :text="btnSearch"  />
                    
        </StackLayout>
        
    </Page>
</template>

<script>
import axios from 'axios'
import Results from './Results'
    export default {
        data(){
            return{
                movie_search: "",
                btnSearch: "Search"
            }
        },

        methods: {
            searchMovie(){
                axios({
                     url: "https://wheretowatch-backend.herokuapp.com/findmovie",
                     method: "POST",
                    data: {
                        movie_search: this.movie_search
                     }
                 })
                 .then((r) => {
                     if(r.data != "Nothing Found"){
                        this.$navigateTo(Results, {
                         animated:true,
                         transition: {
                             name:'slideLeft',
                             duration: 200
                         },
                         props: {
                            results: r.data
                         }
                    })
                     }
                     else alert("Nothing Found")
                 })
                 .catch((e) => {
                     console.log(e)
                     alert(e)
                 })
            }
        }
    };
</script>

<style scoped lang="scss">
</style>
