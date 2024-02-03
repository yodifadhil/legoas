<script setup>

    import DataTable from 'datatables.net-vue3';
    import DataTablesCore from 'datatables.net';
    import Image from './assets/filter.svg';
    import 'datatables.net-buttons';
    import 'datatables.net-buttons/js/buttons.html5';
    import 'datatables.net-responsive';
    import 'datatables.net-select';
    
    import { ref } from 'vue';

    const Data = [
        {
            "noKewajiban": "001",
            "noPolisi": "ABC123",
            "pemilik": "John Doe",
            "peserta": "Company A",
            "nomorVA": "VA123",
            "hargaTerbentuk": "500000",
            "biayaAdmin": "10000",
            "ppn": "5000",
            "total": "515000",
            "tanggalLelang": "2022-02-01",
            "tanggalJatuhTempo": "2022-03-01",
            "tanggalLunas": "2022-03-05",
            "status": "1"
        },
        {
            "noKewajiban": "002",
            "noPolisi": "XYZ789",
            "pemilik": "Jane Doe",
            "peserta": "Company B",
            "nomorVA": "VA456",
            "hargaTerbentuk": "700000",
            "biayaAdmin": "15000",
            "ppn": "7000",
            "total": "722000",
            "tanggalLelang": "2022-02-05",
            "tanggalJatuhTempo": "2022-03-05",
            "tanggalLunas": "2022-03-10",
            "status": "2"
        },
        {
            "noKewajiban": "003",
            "noPolisi": "DEF456",
            "pemilik": "Alice Johnson",
            "peserta": "Company C",
            "nomorVA": "VA789",
            "hargaTerbentuk": "300000",
            "biayaAdmin": "8000",
            "ppn": "4000",
            "total": "311000",
            "tanggalLelang": "2022-02-10",
            "tanggalJatuhTempo": "2022-03-10",
            "tanggalLunas": null,
            "status": "3"
        },
        {
            "noKewajiban": "004",
            "noPolisi": "GHI789",
            "pemilik": "Bob Smith",
            "peserta": "Company D",
            "nomorVA": "VA987",
            "hargaTerbentuk": "900000",
            "biayaAdmin": "20000",
            "ppn": "8000",
            "total": "928000",
            "tanggalLelang": "2022-02-15",
            "tanggalJatuhTempo": "2022-03-15",
            "tanggalLunas": "2022-03-20",
            "status": "1"
        },
        {
            "noKewajiban": "005",
            "noPolisi": "JKL012",
            "pemilik": "Eva Rodriguez",
            "peserta": "Company E",
            "nomorVA": "VA654",
            "hargaTerbentuk": "600000",
            "biayaAdmin": "12000",
            "ppn": "6000",
            "total": "618000",
            "tanggalLelang": "2022-02-20",
            "tanggalJatuhTempo": "2022-03-20",
            "tanggalLunas": "2022-03-25",
            "status": "2"
        },
        {
            "noKewajiban": "006",
            "noPolisi": "MNO345",
            "pemilik": "Chris Brown",
            "peserta": "Company F",
            "nomorVA": "VA321",
            "hargaTerbentuk": "400000",
            "biayaAdmin": "9000",
            "ppn": "3000",
            "total": "412000",
            "tanggalLelang": "2022-02-25",
            "tanggalJatuhTempo": "2022-03-25",
            "tanggalLunas": null,
            "status": "3"
        },
        {
            "noKewajiban": "007",
            "noPolisi": "PQR678",
            "pemilik": "David Williams",
            "peserta": "Company G",
            "nomorVA": "VA012",
            "hargaTerbentuk": "800000",
            "biayaAdmin": "18000",
            "ppn": "10000",
            "total": "828000",
            "tanggalLelang": "2022-03-01",
            "tanggalJatuhTempo": "2022-04-01",
            "tanggalLunas": "2022-04-05",
            "status": "1"
        },
        {
            "noKewajiban": "008",
            "noPolisi": "STU901",
            "pemilik": "Maria Garcia",
            "peserta": "Company H",
            "nomorVA": "VA345",
            "hargaTerbentuk": "550000",
            "biayaAdmin": "11000",
            "ppn": "5500",
            "total": "566500",
            "tanggalLelang": "2022-03-05",
            "tanggalJatuhTempo": "2022-04-05",
            "tanggalLunas": "2022-04-10",
            "status": "2"
        },
        {
            "noKewajiban": "009",
            "noPolisi": "VWX234",
            "pemilik": "Michael Davis",
            "peserta": "Company I",
            "nomorVA": "VA678",
            "hargaTerbentuk": "950000",
            "biayaAdmin": "22000",
            "ppn": "9000",
            "total": "979000",
            "tanggalLelang": "2022-03-10",
            "tanggalJatuhTempo": "2022-04-10",
            "tanggalLunas": null,
            "status": "3"
        },
        {
            "noKewajiban": "010",
            "noPolisi": "YZA567",
            "pemilik": "Sophie Miller",
            "peserta": "Company J",
            "nomorVA": "VA890",
            "hargaTerbentuk": "750000",
            "biayaAdmin": "16000",
            "ppn": "7500",
            "total": "772500",
            "tanggalLelang": "2022-03-15",
            "tanggalJatuhTempo": "2022-04-15",
            "tanggalLunas": "2022-04-20",
            "status": "1"
        },
        {
            "noKewajiban": "011",
            "noPolisi": "BCD789",
            "pemilik": "Isaac Johnson",
            "peserta": "Company K",
            "nomorVA": "VA234",
            "hargaTerbentuk": "850000",
            "biayaAdmin": "19000",
            "ppn": "8500",
            "total": "873500",
            "tanggalLelang": "2022-03-20",
            "tanggalJatuhTempo": "2022-04-20",
            "tanggalLunas": "2022-04-25",
            "status": "2"
        },
        {
            "noKewajiban": "012",
            "noPolisi": "EFG012",
            "pemilik": "Lily Martinez",
            "peserta": "Company L",
            "nomorVA": "VA456",
            "hargaTerbentuk": "420000",
            "biayaAdmin": "9500",
            "ppn": "4200",
            "total": "434700",
            "tanggalLelang": "2022-03-25",
            "tanggalJatuhTempo": "2022-04-25",
            "tanggalLunas": null,
            "status": "3"
        },
        {
            "noKewajiban": "013",
            "noPolisi": "HIJ345",
            "pemilik": "Oliver Wilson",
            "peserta": "Company M",
            "nomorVA": "VA678",
            "hargaTerbentuk": "670000",
            "biayaAdmin": "14000",
            "ppn": "6700",
            "total": "687700",
            "tanggalLelang": "2022-04-01",
            "tanggalJatuhTempo": "2022-05-01",
            "tanggalLunas": "2022-05-05",
            "status": "1"
        },
        {
            "noKewajiban": "014",
            "noPolisi": "KLM901",
            "pemilik": "Sophia Davis",
            "peserta": "Company N",
            "nomorVA": "VA890",
            "hargaTerbentuk": "720000",
            "biayaAdmin": "16000",
            "ppn": "7200",
            "total": "739200",
            "tanggalLelang": "2022-04-05",
            "tanggalJatuhTempo": "2022-05-05",
            "tanggalLunas": "2022-05-10",
            "status": "2"
        },
        {
            "noKewajiban": "015",
            "noPolisi": "NOP234",
            "pemilik": "Ethan Miller",
            "peserta": "Company O",
            "nomorVA": "VA012",
            "hargaTerbentuk": "560000",
            "biayaAdmin": "12000",
            "ppn": "5600",
            "total": "577600",
            "tanggalLelang": "2022-04-10",
            "tanggalJatuhTempo": "2022-05-10",
            "tanggalLunas": null,
            "status": "3"
        },
        {
            "noKewajiban": "016",
            "noPolisi": "PQR567",
            "pemilik": "Mia Taylor",
            "peserta": "Company P",
            "nomorVA": "VA345",
            "hargaTerbentuk": "980000",
            "biayaAdmin": "23000",
            "ppn": "9500",
            "total": "1009500",
            "tanggalLelang": "2022-04-15",
            "tanggalJatuhTempo": "2022-05-15",
            "tanggalLunas": "2022-05-20",
            "status": "1"
        },
        {
            "noKewajiban": "017",
            "noPolisi": "STU890",
            "pemilik": "Aiden Garcia",
            "peserta": "Company Q",
            "nomorVA": "VA678",
            "hargaTerbentuk": "630000",
            "biayaAdmin": "13000",
            "ppn": "6300",
            "total": "646300",
            "tanggalLelang": "2022-04-20",
            "tanggalJatuhTempo": "2022-05-20",
            "tanggalLunas": "2022-05-25",
            "status": "2"
        },
        {
            "noKewajiban": "018",
            "noPolisi": "UVW123",
            "pemilik": "Ella Anderson",
            "peserta": "Company R",
            "nomorVA": "VA890",
            "hargaTerbentuk": "780000",
            "biayaAdmin": "17000",
            "ppn": "7800",
            "total": "804800",
            "tanggalLelang": "2022-04-25",
            "tanggalJatuhTempo": "2022-05-25",
            "tanggalLunas": null,
            "status": "3"
        },
        {
            "noKewajiban": "019",
            "noPolisi": "WXY456",
            "pemilik": "Logan Martin",
            "peserta": "Company S",
            "nomorVA": "VA012",
            "hargaTerbentuk": "490000",
            "biayaAdmin": "11000",
            "ppn": "4900",
            "total": "505900",
            "tanggalLelang": "2022-05-01",
            "tanggalJatuhTempo": "2022-06-01",
            "tanggalLunas": "2022-06-05",
            "status": "1"
        },
        {
            "noKewajiban": "020",
            "noPolisi": "YZA567",
            "pemilik": "Lucy Brown",
            "peserta": "Company T",
            "nomorVA": "VA345",
            "hargaTerbentuk": "890000",
            "biayaAdmin": "20000",
            "ppn": "8800",
            "total": "918800",
            "tanggalLelang": "2022-05-05",
            "tanggalJatuhTempo": "2022-06-05",
            "tanggalLunas": "2022-06-10",
            "status": "2"
        }
    ]

    DataTable.use(DataTablesCore);

    const is_show = ref(true);
    const dataTableRef = ref(null);

    const filter = {
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

    const handleFilter = () => {
        const dataTable = dataTableRef.value;
        dataTable.filter().draw();
    };

    const columns = [
        {
            title: 'V',
            render: function (data, type, row) {
                if (type === 'display') {
                    return '<input type="checkbox" class="select-checkbox">';
                }
                return '';
            },
            orderable: false,
            className: 'select-checkbox',
        },
        { title: 'No. Kewajiban', data: 'noKewajiban'},
        { title: 'No. Polisi', data: 'noPolisi'},
        { title: 'Pemilik', data: 'pemilik'},
        { title: 'Peserta', data: 'peserta'},
        { title: 'Nomor VA', data: 'nomorVA'},
        { title: 'Harga Terbentuk (Rp)', data: 'hargaTerbentuk'},
        { title: 'Biaya Admin ex PPN (Rp)', data: 'biayaAdmin'},
        { title: 'PPN (Rp)', data: 'ppn'},
        { title: 'Total (Rp)', data: 'total'},
        { title: 'Tanggal Lelang', data: 'tanggalLelang'},
        { title: 'Tanggal Jatuh Tempo', data: 'tanggalJatuhTempo'},
        { title: 'Tanggal Lunas', data: 'tanggalLunas'},
        { title: 'Status', data: 'status'},
    ];

    const options = {
        paging: true, 
        pageLength: 10,
        searching: false,
        info: true,
        dom: "rtip",
        buttons: [
            {
            extend: 'excelHtml5',
            text: 'Export to Excel',
            filename: 'data_export',
            },
        ],
        columnDefs: [
            {
                targets: [],
            },
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
    };

    const showFilter = () => {
        is_show.value = !is_show.value;
    };

</script>

<template>
    <div>
        <div class="toolbar">
            <button>REFRESH</button>
            <button>EXPORT</button>
            <button>BAYAR</button>
            <button @click="showFilter">
                <img :src="Image" alt="Example Image" width="20" height="20" style="width: fit-content !important;">
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
    </div>
    <div style="overflow-x: scroll;">
        <DataTable
            ref="dataTableRef"
            :columns="columns"
            :options="options"
            :data="Data"
            class="display nowrap"
            width="100%"
        >
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
        </DataTable>
    </div>
</template>

<style>
    @import 'datatables.net-dt';

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

