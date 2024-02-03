<template>
<div>
    <div class="header">
      
    </div>
    <div class="toolbar">
      <button>REFRESH</button>
      <button>EXPORT</button>
      <button>BAYAR</button>
      <button @click="showFilter">
        <img :src="imagePath" alt="Example Image" width="20" height="20" style="width: fit-content !important;">
      </button>
    </div>
    <div class="form-search" v-if="is_show">
      <div class="form-group">
        <div class="form">
          <label>No. Kewajiban</label>
          <input v-model="filter.no_kewajiban" type="text">
        </div>
        <div class="form">
          <label>No. Polisi</label>
          <input v-model="filter.no_polisi" type="text">
        </div>
        <div class="form">
          <label>Pemilik</label>
          <input v-model="filter.pemilik" type="text">
        </div>
        <div class="form">
          <label>Peserta</label>
          <input v-model="filter.peserta" type="text">
        </div>
        <div class="form">
          <label>Nomor VA</label>
          <input v-model="filter.no_va" type="text">
        </div>
      </div>
      <div class="form-group">
        <div class="form">
          <label>Harga Terbentuk</label>
          <input v-model="filter.harga_terbentuk_min" type="number">
          <label>s/d</label>
          <input v-model="filter.harga_terbentuk_max" type="number">
        </div>
        <div class="form">
          <label>Biaya Admin</label>
          <input v-model="filter.harga_biaya_admin_min" type="number">
          <label>s/d</label>
          <input v-model="filter.harga_biaya_admin_min" type="number">
        </div>
        <div class="form">
          <label>PPN</label>
          <input v-model="filter.harga_ppn_min" type="number">
          <label>s/d</label>
          <input v-model="filter.harga_ppn_max" type="number">
        </div>
      </div>
      <div class="form-group">
        <div class="form">
          <div class="form">
            <label>Total</label>
            <input v-model="filter.harga_total_min" type="number">
            <label>s/d</label>
            <input v-model="filter.harga_total_max" type="number">
          </div>
          <div class="form">
            <label>Tanggal Lelang</label>
            <input v-model="filter.tanggal_lelang_min" type="date">
            <label>s/d</label>
            <input v-model="filter.tanggal_lelang_max" type="date">
          </div>
          <div class="form">
            <label>Tanggal Jatuh Tempo</label>
            <input v-model="filter.tanggal_jatuh_tempo_min" type="date">
            <label>s/d</label>
            <input v-model="filter.tanggal_jatuh_tempo_max" type="date">
          </div>
        </div>
      </div>
      <div class="form-group">
        <div class="form">
            <label>Tanggal Lunas</label>
            <input v-model="filter.tanggal_lunasa_min" type="date">
            <label>s/d</label>
            <input v-model="filter.tanggal_lunasa_max" type="date">
          </div>
      </div>
      <div class="form-group" style="justify-content: flex-end">
        <button @click="handleFilter">Search</button>
      </div>
    <div>
        
      </div>
    </div>
    <!-- <table id="myTable" class="display my-bordered-table">
      <thead>
        <tr>
          <th>V</th>
          <th>No. Kewajiban</th>
          <th>No. Polisi</th>
          <th>Pemilik</th>
          <th>Peserta</th>
          <th>Nomor VA</th>
          <th>Harga Terbentuk (Rp)</th>
          <th>Biaya Admin ex PPN (Rp)</th>
          <th>PPN (Rp)</th>
          <th>Total (Rp)</th>
          <th>Tanggal Lelang</th>
          <th>Tanggal Jatuh Tempo</th>
          <th>Tanggal Lunas</th>
          <th>Status</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in filteredTableData" :key="item.noKewajiban">
          <td><input type="checkbox" /></td>
          <td>{{ item.noKewajiban }}</td>
          <td>{{ item.noPolisi }}</td>
          <td>{{ item.pemilik }}</td>
          <td>{{ item.peserta }}</td>
          <td>{{ item.nomorVA }}</td>
          <td>{{ item.hargaTerbentuk }}</td>
          <td>{{ item.biayaAdmin }}</td>
          <td>{{ item.ppn }}</td>
          <td>{{ item.total }}</td>
          <td>{{ item.tanggalLelang }}</td>
          <td>{{ item.tanggalJatuhTempo }}</td>
          <td>{{ item.tanggalLunas }}</td>
          <td>{{ item.status }}</td>
        </tr>
      </tbody>
    </table> -->
    <vue-good-table
      :columns="columns"
      :rows="tableData"
      :pagination-options="{enabled: true}"
      :lineNumbers="true"
    ></vue-good-table>
  </div>
</template>

<script>
import "datatables.net";
import "datatables.net-dt";
import 'datatables.net-dt/css/jquery.dataTables.css';
import { Data } from "./Data.vue";
import $ from 'jquery';
import FilterIcon from './assets/filter.svg';
import VueGoodTablePlugin from 'vue-good-table';
import 'vue-good-table/dist/vue-good-table.css';

export default {
  data() {
    return {
      columns: [
        { label: 'V', field: 'v', width: '50px' },
        { label: 'No. Kewajiban', field: 'no_kewajiban', width: '100px' },
        { label: 'No. Polisi', field: 'no_polisi', width: '100px' },
        { label: 'Pemilik', field: 'pemilik', width: '100px' },
        { label: 'Peserta', field: 'peserta', width: '100px' },
        { label: 'Nomor VA', field: 'no_va', width: '100px' },
        { label: 'Harga Terbentuk (Rp)', field: 'harga_terbentuk', width: '150px', numeric: true },
        { label: 'Biaya Admin ex PPN (Rp)', field: 'biaya_admin_ex_ppn', width: '150px', numeric: true },
        { label: 'PPN (Rp)', field: 'ppn', width: '100px', numeric: true },
        { label: 'Total (Rp)', field: 'total', width: '100px', numeric: true },
        { label: 'Tanggal Lelang', field: 'tanggal_lelang', width: '100px' },
        { label: 'Tanggal Jatuh Tempo', field: 'tanggal_jatuh_tempo', width: '120px' },
        { label: 'Tanggal Lunas', field: 'tanggal_lunas', width: '100px' },
        { label: 'Status', field: 'status', width: '100px' },
      ],
      tableData: Data,
      filteredData: [],
      searchTerm: "",
      imagePath: FilterIcon,
      is_show: true,
      filteredChange: 0,
      filter: {
        no_kewajiban: "",
        no_polisi: "",
        pemilik: "",
        peserta: "",
        no_va: "",
        harga_terbentuk_min: 0,
        harga_terbentuk_max: 0,
        harga_biaya_admin_min: 0,
        harga_biaya_admin_max: 0,
        harga_ppn_min: 0,
        harga_ppn_max: 0,
        harga_total_min: 0,
        harga_total_max: 0,
        tanggal_lelang_min: "",
        tanggal_lelang_max: "",
        tanggal_jatuh_tempo_min: "",
        tanggal_jatuh_tempo_max: "",
        tanggal_lunas_min: "",
        tanggal_lunas_max: "",
        // tanggal_lelang_min: this.dateFormat(new Date()),
        // tanggal_lelang_max: this.dateFormat(new Date()),
        // tanggal_jatuh_tempo_min: this.dateFormat(new Date()),
        // tanggal_jatuh_tempo_max: this.dateFormat(new Date()),
        // tanggal_lunas_min: this.dateFormat(new Date()),
        // tanggal_lunas_max: this.dateFormat(new Date())
      }
    };
  },
  computed: {
    filteredTableData() {

      let filters = this.filter

      return this.tableData.filter((item) => {

        let noKewajiban = item.noKewajiban.includes(filters.no_kewajiban);
        let noPolisi = item.noPolisi.includes(filters.no_polisi);
        let pemilik = item.pemilik.includes(filters.pemilik);
        let peserta = item.peserta.includes(filters.peserta);
        let noVa = item.nomorVA.includes(filters.no_va);
        let hargaTerbentuk = parseInt(filters.harga_terbentuk_min) > 0 ? parseInt(item.hargaTerbentuk) >= filters.harga_terbentuk_min : true && parseInt(filters.harga_terbentuk_max) > 0 ? parseInt(item.hargaTerbentuk) <= filters.harga_terbentuk_max : true;
        let hargaBiayaAdmin = filters.harga_biaya_admin_max > 0 ? parseInt(item.biayaAdmin) >= filters.harga_biaya_admin_min : true && parseInt(filters.harga_biaya_admin_min) > 0 ? parseInt(item.biayaAdmin) <= filters.harga_biaya_admin_max : true;
        let hargaPpn = parseInt(filters.harga_ppn_min) > 0 ? parseInt(item.ppn) >= filters.harga_ppn_min : true && parseInt(item.harga_ppn_max) > 0 ? parseInt(item.harga_ppn_max) <= filters.ppn_max : true;
        let hargaTotal = parseInt(filters.harga_total_min) > 0 ? parseInt(item.total) >= filters.harga_total_min : true && parseInt(item.harga_total_max) ? parseInt(item.harga_total_max) <= filters.total_max : true;

        return noKewajiban && noPolisi && pemilik && peserta && noVa && hargaBiayaAdmin && hargaPpn && hargaTotal && hargaTerbentuk;
      });
    },
  },
  methods: {
    showFilter(){
      this.is_show = !this.is_show;
    },
    handleFilter(){ 
      
    },
    dateFormat(date){
      const year = date.getFullYear();
      const month = String(date.getMonth() + 1).padStart(2, '0'); // Month is zero-based
      const day = String(date.getDate()).padStart(2, '0');

      return `${year}-${month}-${day}`;
    },
    initializeTable(){

    },
    initializeDataTable(){
      this.$nextTick(() => {
        $("#myTable").DataTable({
          paging: true, 
          pageLength: 5,
          searching: false,
          info: true,
          dom: "rtip",
          columnDefs: [
            {
              targets: [6, 7, 8, 9],
              render: function (data, type, row) {
                if (type === "display" && data !== null) {
                  return parseFloat(data).toLocaleString(undefined, { maximumFractionDigits: 2 }).replaceAll(",", ".");
                }
                return data;
              },
            },
            {
              targets: [10, 11, 12],
              render: function (data, type, row) {
                if (type === "display" && data) 
                {
                  const date = new Date(data);
                  return (
                    ("0" + date.getDate()).slice(-2) +
                    "/" +
                    ("0" + (date.getMonth() + 1)).slice(-2) +
                    "/" +
                    date.getFullYear()
                  );
                } 
                
                return "-";
              },
            },
          ],
        });
      });
    }
  },
  mounted() {
    // this.initializeDataTable();
    this.initializeTable();
  },
};
</script>

<style scoped>

  .toolbar{
    display: flex;
    justify-content: flex-end;
    margin-bottom: 16px;
    gap: 8px;
  }

  .my-bordered-table {
    width: 100%;
    border-collapse: collapse;
  }

  .my-bordered-table th,
  .my-bordered-table td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }

  .my-bordered-table th {
    background-color: #f2f2f2;
  }

  .form-search{
    display: flex;
    flex-direction: column;
    gap: 24px;    
    background-color: #DEDEDE;
    padding: 24px;
    padding-bottom: 0px;
    margin-bottom: 24px;
  }

  .form-group{
    display: flex;
    gap: 16px;
  }

  .form{
    display: flex;
    align-items: center;
    gap: 16px;
  }

  button{
    width: "fit-content";
    border: none;
    background-color: #ABABAB;
    font-weight: bold;
    color: white;
    border-radius: 8px;
    padding: 8px;
  }

  .dataTables_wrapper .dataTables_length{
    margin-bottom: 20px;
  }
</style>