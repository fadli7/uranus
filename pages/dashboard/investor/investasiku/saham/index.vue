<template>
	<div>
		<div class="hero is-white">
        <div class="hero-body has-text-centered">
            <p class="title is-3 has-text-primary">Saham Investasiku</p>
            <p class="subtitle">Daftar perusahaan yang anda memiliki saham di dalamnya</p>
        </div>
    </div>
    <div class="section">
        <div class="container">
            <div class="columns">
                <div class="column is-3">
                    <div class="box">
                        <div class="field">
                            <label class="label">Cari Bisnis</label>

                            <p class="control has-icons-left">
                                <input class="input" type="text" placeholder="Text input">
                                <span class="icon is-small is-left">
                                        <i class="fas fa-search"></i>
                                    </span>
                            </p>

                        </div>
                        <div class="field">
                            <label class="label">Kategori Bisnis</label>
                            <p class="control has-icons-left">
                                    <span class="select is-fullwidth">
                                          <select>
                                            <option selected>Kategori</option>
                                              
                                            <option v-for="item in 10" :key="item">Select dropdown</option>
                                              
                                          </select>
                                    </span>
                                <span class="icon is-small is-left">
                                        <i class="fas fa-globe"></i>
                                    </span>
                            </p>
                        </div>
                        <div class="field">
                            <label class="label">Status Pendanaan</label>
                            <p class="control has-icons-left">
                                    <span class="select is-fullwidth">
                                        <select>
                                            <option selected>status</option>
                                            <option>Tersedia</option>
                                            <option>Selesai</option>
                                            <option>Dihentikan</option>
                                            <option>Melanggar Aturan</option>
                                         </select>
                                    </span>
                                <span class="icon is-small is-left">
                                        <i class="fas fa-globe"></i>
                                    </span>
                            </p>
                        </div>
                        <div class="field">
                            <div class="control">
                                <a href="" class="button is-primary is-fullwidth">Filter Data</a>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="column is-9">
                    <div class="">
                        
                            <div v-for="item in companies" :key="item.id" class="box">
                                <div class="media">
                                    <div class="media-left">
                                        <figure class="image is-64x64">
                                            <img :src="item.image" alt="Image">
                                        </figure>
                                    </div>
                                    <div class="media-content">
                                        <div class="content">
                                            <p>
                                                <a :href="'/dashboard/investor/investasiku/saham/' + item.id" class="has-text-weight-bold has-text-black">{{ item.name }}</a>
                                                <br>
                                                {{ item.description }}
                                                <br>
                                                <!-- <span class="has-text-weight-light">{{ item.name }} - Sampai 23 Juni 2019</span> -->
                                            </p>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        

                        <div class="field">
                            <div class="control">
                                <a href="/dashboard/investasiku/saham" class="button is-primary is-fullwidth">Selanjutnya</a>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
	</div>
</template>

<script>
export default {
    data() {
        return {
            companies: []
        }
    },

    mounted() {
        this.getSahamku()
    },

    methods: {
        getSahamku() {
            this.$axios.get('/core/companies/my/').then(response => {
                console.log(response.data.results)
                this.companies = response.data.results
            })
        }
    },
}
</script>