<template>
  <div class="submit-form">
    <div v-if="!submitted">
      <div class="container">
        <div class="row">
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="nama">Nama</label>
              <input
                type="text"
                class="form-control"
                id="nama"
                required
                v-model="data.nama"
                name="nama"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="nik">NIK</label>
              <input
                type="number"
                class="form-control"
                id="nik"
                required
                v-model="data.nik"
                name="nik"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="nomor_kartu_keluarga">Nomor Kartu Keluarga</label>
              <input
                type="number"
                class="form-control"
                id="nomor_kartu_keluarga"
                required
                v-model="data.nomor_kartu_keluarga"
                name="nomor_kartu_keluarga"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="foto_ktp">Foto KTP</label>
              <input type="file" @change="uploadFotoKtp" ref="file" accept="image/*">
            </div>
            <div id="preview">
              <img v-if="urlFotoKtp" :src="urlFotoKtp" />
            </div>
          </div>
          
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="foto_kartu_keluarga">Foto Kartu Keluarga</label>
              <input type="file" @change="uploadFotoKartuKeluarga" ref="file" accept="image/*">
            </div>
            <div id="preview">
              <img v-if="urlFotoKartuKeluarga" :src="urlFotoKtp" />
            </div>
          </div>
          
          <div class="col-md-3"> 
            <div class="form-group m-2">
              <label for="umur">Umur</label>
              <input
                type="number"
                class="form-control"
                id="umur"
                required
                v-model="data.umur"
                name="umur"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="jenis_kelamin">Jenis Kelamin</label>
              <select v-model="data.jenis_kelamin" class="form-control">
                <option disabled value="">Pilih Jenis Kelamin</option>
                <option value="L">Laki - Laki</option>
                <option value="P">Perempuan</option>
              </select>
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="provinsi">Provinsi</label>
              <select v-model="data.provinsi" class="form-control" @change="getKab(data.provinsi)">
                <option disabled value="">Pilih Provinsi</option>
                <option v-for="model in itemProvinsi" :key="model.id" :value="model.id">{{ model.name  }}</option>
              </select>
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="kab_kota">Kab / Kota</label>
              <select v-model="data.kab_kota" class="form-control" @change="getKecamatan(data.kab_kota)">
                <option disabled value="">Pilih Kab / Kota</option>
                <option v-for="model in itemKabKota" :key="model.id" :value="model.id">{{ model.name  }}</option>
              </select>
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="kecamatan">Kecamatan</label>
              <select v-model="data.kecamatan" class="form-control" @change="getKelurahan(data.kecamatan)">
                <option disabled value="">Pilih Kecamatan</option>
                <option v-for="model in itemKecamatan" :key="model.id" :value="model.id">{{ model.name  }}</option>
              </select>
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="kelurahan">Kelurahan</label>
              <select v-model="data.kelurahan" class="form-control">
                <option disabled value="">Pilih Kelurahan</option>
                <option v-for="model in itemKelurahan" :key="model.id" :value="model.id">{{ model.name  }}</option>
              </select>
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="alamat">Alamat</label>
              <textarea v-model="data.alamat" class="form-control" @input="assertMaxChars"></textarea>
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="rt">RT</label>
              <input
                type="text"
                class="form-control"
                id="rt"
                required
                v-model="data.rt"
                name="rt"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="rw">RW</label>
              <input
                type="text"
                class="form-control"
                id="rw"
                required
                v-model="data.rw"
                name="rw"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="penghasilan_sebelum_pandemi">Penghasilan Sebelum Pandemi</label>
              <input
                type="number"
                class="form-control"
                id="penghasilan_sebelum_pandemi"
                required
                v-model="data.penghasilan_sebelum_pandemi"
                name="penghasilan_sebelum_pandemi"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="penghasilan_setelah_pandemi">Penghasilan Setelah Pandemi</label>
              <input
                type="number"
                class="form-control"
                id="penghasilan_setelah_pandemi"
                required
                v-model="data.penghasilan_setelah_pandemi"
                name="penghasilan_setelah_pandemi"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <label for="alasan_membutuhkan_uang">Alasan Membutuhkan Uang</label>
              <select v-model="data.alasan_membutuhkan_uang" class="form-control">
                <option disabled value="">Pilih Alasan Membutuhkan Uang</option>
                <option value="1">Kehilangan Pekerjaan</option>
                <option value="2">Kepala Keluarga</option>
                <option value="3">Tergolong Fakir Miskin</option>
                <option value="4">Lainnya</option>
              </select>
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group m-2">
              <input type="checkbox" id="checkbox" v-model="data.checked" />
              Saya menyatakan bahwa data yang diisikan adalah benar dan siap mempertanggungjawabkan apabila ditemukan ketidaksesuaian dalam data tersebut
            </div>
          </div>
        </div>
      </div>

      <div class="form-group m-2">
        <button @click="saveTutorial" class="btn btn-success">Submit</button>
      </div>
    </div>

    <div v-else>
      <h4>You submitted successfully!</h4>
      <button class="btn btn-success" @click="newTutorial">Add</button>
    </div>
  </div>
</template>

<script>

import axios from "axios";

export default {
  name: "add",
  data() {
    return {
      data: {
        id: null,
        nama: "",
        nik: "",
        nomor_kartu_keluarga: "",
        description: "",
        umur: "",
        jenis_kelamin: "",
        provinsi: "",
        kab_kota: "",
        kecamatan: "",
        kelurahan: "",
        alamat: "",
        rt: "",
        rw: "",
        penghasilan_sebelum_pandemi: "",
        penghasilan_setelah_pandemi: "",
        alasan_membutuhkan_uang: "",
        checked: ""
      },
      foto_ktp: null,
      foto_kartu_keluarga: null,
      submitted: false,
      itemProvinsi: [],
      itemKabKota: [],
      itemKecamatan: [],
      itemKelurahan: [],
      maxLengthInCars: 255,
      urlFotoKtp: null,
      urlFotoKartuKeluarga: null
    };
  },
  mounted () {
    axios
      .get('https://www.emsifa.com/api-wilayah-indonesia/api/provinces.json')
      .then(response => {
        this.itemProvinsi = response.data;
      });
  },
  methods: {
    uploadFotoKtp(e) {
        const file = e.target.files[0];
        this.urlFotoKtp = URL.createObjectURL(file);
        this.foto_ktp = this.$refs.file.files[0];
    },
    assertMaxChars: function () {
        if (this.value.length >= this.maxLengthInCars) {
            this.value = this.value.substring(0,this.maxLengthInCars);
        }
    },
    uploadFotoKartuKeluarga(e) {
        const file = e.target.files[0];
        this.urlFotoKartuKeluarga = URL.createObjectURL(file);
        this.foto_kartu_keluarga = this.$refs.file.files[0];
    },
    getKab(provinsi) {
      axios
      .get('https://www.emsifa.com/api-wilayah-indonesia/api/regencies/' + provinsi + '.json')
      .then(response => {
        this.itemKabKota = response.data;
      });
    },
    getKecamatan(kab_kota) {
      axios
      .get('https://www.emsifa.com/api-wilayah-indonesia/api/districts/' + kab_kota + '.json')
      .then(response => {
        this.itemKecamatan = response.data;
      });
    },
    getKelurahan(kecamatan) {
      axios
      .get('https://www.emsifa.com/api-wilayah-indonesia/api/villages/' + kecamatan + '.json')
      .then(response => {
        this.itemKelurahan = response.data;
      });
    },
    saveTutorial() {
      var data = this.data;
      console.log(data);
      setTimeout(function(){
          this.submitted = false;
      }, 1500);
    },
    
    newTutorial() {
      this.submitted = false;
      this.data = {};
    }
  }
};
</script>

<style>
#preview {
  display: flex;
  justify-content: center;
  align-items: center;
}

#preview img {
  max-width: 100%;
  max-height: 500px;
}
</style>
