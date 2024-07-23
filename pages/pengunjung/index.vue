<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">DAFTAR KUNJUNGAN</h2>
        <div class="my-3">
        </div>
        <table class="table">
          <thead>
            <tr>
              <td>#</td>
              <td>NAMA</td>
              <td>KEANGGOTAAN</td>
              <td>WAKTU</td>
              <td>KEPERLUAN</td>
            </tr>
        </thead>
        <tbody>
          <tr v-for="(visitor,i) in visitors" :key="i">
            <td>{{ i+1 }}.</td>
            <td>{{ visitor.nama }}</td>
            <td>{{ visitor.keanggotaan.nama }}</td>
            <td>{{ visitor.tanggal }}, {{ visitor.waktu }}</td>
            <td>{{ visitor.Keperluan.nama }}</td>
            </tr>
        </tbody>
        </table>
        <nuxt-link to="http://localhost:3000/Pengunjung/">
          <button type="submit" class="btn btn-secondary btn-lg rounded-5 px-5">Selesai</button>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script setup>
const supabase = useSupabaseClient()

const visitors = ref([])

const getPengunjung = async () => {
  const {data,error} = await supabase
    .from('pengunjung')
    .select(`*,keanggotaan(*), Keperluan(*)`)
  if (data) visitors.value = data
  if (error)console.log(error)
  // if(data) console.log(data)
}

  onMounted(() => {
    getPengunjung()
})
</script>