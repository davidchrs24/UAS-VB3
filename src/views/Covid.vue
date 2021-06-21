/<template>
        <table class="bg-pink-400 max-w-full mx-0 m-3 mx-32"> 
            <!-- <tr>
                <th class="text-black font-bold border-black py-2 px-3 mx-3">No</th>
                <th class="text-black font-bold border-black py-2 px-3 mx-3">Negara<th>
                <th class="text-black font-bold border-black py-2 px-3 mx-3">Baru Positif</th>
                <th class="text-black font-bold border-black py-2 px-3 mx-3">Positif</th>
                <th class="text-black font-bold border-black py-2 px-3 mx-3">Baru Meninggal</th>
                <th class="text-black font-bold border-black py-2 px-3 mx-3">Meninggal</th>
                <th class="text-black font-bold border-black py-2 px-3 mx-3">Baru Sembuh</th>
                <th class="text-black font-bold border-black py-2 px-3 mx-3">Sembuh</th>
                
            </tr> -->
            <tr>
                <td class="text-black font-bold border py-2 px-3">No</td>
                <td class="text-black font-bold border py-2 px-3 ">Negara</td>
                <td class="text-black font-bold border py-2 px-3">Kasus Terbaru</td>
                <td class="text-black font-bold border py-2 px-3">Positif</td>
                <td class="text-black font-bold border py-2 px-3">Baru Meninggal</td>
                <td class="text-black font-bold border py-2 px-3">Meninggal</td>
                <td class="text-black font-bold border py-2 px-3">Baru Pulih</td>
                <td class="text-black font-bold border py-2 px-3">Sembuh</td>      
            </tr>
            <tr v-for="(item, kasus) in data.Countries" :key="kasus">
                <th class="text-black font-semibold border py-2 px-3" scope="row">{{kasus +1}}</th>
                <th class="text-black font-semibold border py-2 px-3">{{item.Country}}</th>
                <th class="text-black font-semibold border py-2 px-3">{{item.NewConfirmed}}</th>
                <th class="text-black font-semibold border py-2 px-3">{{item.TotalConfirmed}}</th>
                <th class="text-black font-semibold border py-2 px-3">{{item.NewDeaths}}</th>
                <th class="text-black font-semibold border py-2 px-3">{{item.TotalDeaths}}</th>
                <th class="text-black font-semibold border py-2 px-3">{{item.NewRecovered}}</th>
                <th class="text-black font-semibold border py-2 px-3">{{item.TotalRecovered}}</th>
            </tr>
        
        </table>    
</template>

<script>
export default {
data() {
    return {
        countries:{},
        data: {},
        posbaru: 0,
        positif: 0,
        barumati: 0,
        meninggal: 0,
        barusembuh:0,
        recovered: 0,

    }
},
filters: {
    numberFormat(number) {
        return number.toLocaleString();
    }
},
methods: {
    getCountries(){
        axios.get('https://api.covid19api.com/countries')
        .then(response =>{
                this.countries = response.data;
            })
    },
    getSummaryData() {
        axios.get('https://api.covid19api.com/summary')
            .then(response => {
                const data = response.data;
                this.data = data;
                this.posbaru = data.Global.NewConfirmed;
                this.positif = data.Global.TotalConfirmed;
                this.barumati =data.Global.NewDeaths;
                this.meninggal = data.Global.TotalDeaths;
                this.barusembuh = data.Global.NewRecovered;
                this.recovered = data.Global.TotalRecovered;
            })
         }    
    },
    mounted() {
        this.getCountries();
        this.getSummaryData()
    }
}

</script>