<template xmlns:v-slot="http://www.w3.org/1999/XSL/Transform">
  <q-page padding class="items-center-justify-center bg-grey-3">
    <q-card flat class="bg-white q-pa-md">
      <span class="text-h5 text-weight-light q-pa-md">
        <span class="text-blue-grey-14">Tambah Data Perhiasan</span>
      </span>
      <div class="q-pa-md">
        <q-form
          @submit="onSubmit"
          class="q-gutter-md"
        >

          <q-input
            label="Kode Perhiasan"
            lazy-rules
            color="teal"
            v-model="form.kodePerhiasan"
            :rules="[
           val => val !== null && val !== '' || 'Kode Perhiasan Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="dns"/>
            </template>
          </q-input>

          <q-input
            label="Jenis Perhiasan"
            lazy-rules
            color="teal"
            v-model="form.jenisPerhiasan"
            :rules="[
           val => val !== null && val !== '' || 'Jenis Perhiasan Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="title"/>
            </template>
          </q-input>
          <q-input
            label="Kadar Perhiasan"
            lazy-rules
            color="teal"
            v-model="form.kadarPerhiasan"
            :rules="[
           val => val !== null && val !== '' || 'Kadar Perhiasan Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="local_offer"/>
            </template>
          </q-input>
          <q-input
            label="Berat Perhiasan"
            lazy-rules
            color="teal"
            v-model="form.beratPerhiasan"
            :rules="[
           val => val !== null && val !== '' || 'Berat Perhiasan Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="gavel"/>
            </template>
          </q-input>
          <q-input
          label="Harga Perhiasan"
          lazy-rules
          color="teal"
          v-model="form.hargaPerhiasan"
          :rules="[
           val => val !== null && val !== '' || 'Harga Perhiasan Dibutuhkan'
           ]">
          <template v-slot:append>
            <q-icon name="attach_money"/>
          </template>
        </q-input>
          <q-input
            lazy-rules
            hint="Pilih gambar"
            type="file"
            ref="file"
            @input="selectFile()"
            color="teal"
            :rules="[
           val => val !== null && val !== '' || 'Gambar Dibutuhkan'
           ]">
            <template v-slot:append>
              <q-icon name="add_photo_alternate"/>
            </template>
          </q-input>
          <div>
            <q-btn
              unelevated
              icon="add"
              type="submit"
              label="Tambah Data Perhiasan"
              style="height: 50px"
              color="teal-6"/>
          </div>
        </q-form>
      </div>
    </q-card>
  </q-page>
</template>

<script>
export default {
  data () {
    return {
      form: {
        kodepPerhiasan: null,
        jenisPerhiasan: null,
        kadarPerhiasan: null,
        beratPerhiasan: null,
        hargaPerhiasan: null
      },
      gambar: null
    }
  },
  methods: {
    selectFile () {
      this.gambar = this.$refs.file.$refs.input.files[0]
    },
    onSubmit () {
      const formData = new FormData()
      formData.append('gambar', this.gambar)
      formData.append('kodePerhiasan', this.form.kodePerhiasan)
      formData.append('jenisPerhiasan', this.form.jenisPerhiasan)
      formData.append('kadarPerhiasan', this.form.kadarPerhiasan)
      formData.append('beratPerhiasan', this.form.beratPerhiasan)
      formData.append('hargaPerhiasan', this.form.hargaPerhiasan)
      this.$axios.post('/perhiasan/input', formData)
        .then((res) => {
          if (res.data.error) {
            this.$q.notify({
              color: 'negative',
              message: res.data.msg,
              icon: 'ion-close'
            })
          } else {
            this.$q.notify({
              color: 'positive',
              message: res.data.msg,
              icon: 'ion-close'
            })
            this.$router.push('/')
          }
        })
    }
  }
}
</script>

<style scoped>

</style>
