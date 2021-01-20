<template>
    <div class="container mx auto">
        <h1 id="titulo" class="text-4xl mt-5 text-white font-bold uppercase text-center">Busca el Clima</h1>
        <div class="max-w-lg mx-auto">
            <div class="p-6 mt-10">
                <div v-if="typeof weather.main != 'undefined'">
                    <p class="text-color-white font-bold text-2xl">{{ weather.name }}, {{ weather.sys.country }}</p>
                    <p class="text-color-white font-bold text-6xl p-4">{{parseInt(weather.main.temp - 273.15)}} &#8451;</p>
                    <p class="p-4 font-bold">{{dateBuilder()}}</p>
                </div>
                <div v-else class="text-center text-white mt-6 font-bold">Agrega tu ciudad y país, el resultado se mostrará aquí</div>
            </div>
            <div class="mt-10">
                <div class="mt-5">
                    <input type="text" placeholder="Escribe tu Ciudad" class="w-full p-2 rounded outline-none text-black" v-model="city">
                </div>
                <div class="mt-5">
                    <select 
                        class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500" v-model="country">
                        <option disabled selected value="">-- Seleccione --</option>
                        <option value="AR">Argentina</option>
                        <option value="CO">Colombia</option>
                        <option value="CR">Costa Rica</option>
                        <option value="ES">España</option>
                        <option value="US">Estados Unidos</option>
                        <option value="MX">México</option>
                        <option value="PE">Perú</option>
                        <option value="VE">Venezuela</option>
                    </select>
                    <button @click="getData" class="mt-5 w-full bg-yellow-500 p-3  uppercase font-bold cursor-pointer rounded focus:outline-none">Obtener Clima</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Form',
    data(){
        return{
            key: 'a53e466207f023a8b8156097aadb7565',
            city: '',
            country: '',
            weather: {}
        }
    },

    methods:{
        getData(){
            const url = `http://api.openweathermap.org/data/2.5/weather?q=${this.city},${this.country}&appid=${this.key}`
            if (this.city==='' || this.country==='') {
                console.log('error');
                return;
            }
            fetch(url)
                .then(res=> res.json())
                .then(this.setResults)
            this.city = "",
            this.country = ""
        },

        setResults(results){
            this.weather = results;
        },
        dateBuilder () {
            let d = new Date();
            let months = ["Enero", "Febrero", "Marzo", "Abril", "Mayo", "Junio", "Julio", "Agosto", "Semptiembre", "Octubre", "Noviembre", "Diciembre"];
            let days = ["Lunes", "Martes", "Miercoles", "Jueves", "Viernes", "Sabado", "Domingo"];

            let day = days[d.getDay()];
            let date = d.getDate();
            let month = months[d.getMonth()];
            let year = d.getFullYear();

            return `${day} ${date} ${month} ${year}`;
        }
    }
}
</script>