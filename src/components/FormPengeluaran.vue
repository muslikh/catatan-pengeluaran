<template>
    <form class="form-pengeluaran" @submit.prevent="catat">
        <div>
            <label>Pengeluaran</label>
            <input v-model="pengeluaran" type="number" id="pengeluaran"/>
        </div>
        <div>
            <label>Keterangan</label>
            <input v-model="keterangan" type="text" id="keterangan"/>
        </div>
        <div>
            <button>Catat!</button>
        </div>
    </form>
</template>

<script>
export default {
    data(){
        return{
            pengeluaran : null,
            keterangan : null,
        }
    },
    methods:{
        catat(){
            this.$emit('entri-pengeluaran', {
                nominal: this.pengeluaran,
                keterangan:this.keterangan
            });

            this.pengeluaran = null;
            this.keterangan = null;
            document.getElementById("pengeluaran").focus()
        }
    }
}
</script>