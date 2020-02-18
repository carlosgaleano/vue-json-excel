<template>

  <div class="container" id="app">
    <hr />
    <h2>Fetch Example</h2>
   
   <template  >
     



    <div class="alert alert-success"     v-if="isExportedt" :active.sync="isExported">
   <a href="#">
          <span class="glyphicon glyphicon-download  "></span>
        </a>
           Descargando Archivo de excel 
           <img src="./assets/descarga.png"   width="10%" >
    </div>
    <div class="btn btn-primary" @click="activeDownload" > Descarga Excel</div>
   </template>    
    
   

    



    <downloadexcel
      class="btn btn-primary"
      :data="json_data"
      :fields="json_fields"
      :before-generate="startDownload"
      :before-finish="finishDownload"
      @onclick="activeDownload" 
    >Download Excel </downloadexcel>
  </div>
</template>

<script>
import downloadexcel from "vue-json-excel";
import axios from "axios";

export default {
  name: "App",
  components: {
    downloadexcel
  },
   computed: {
        isExportedt() {
            return this.isExported;
        }
    },

  data() {
    return {
      
      json_fields: {
        "Complete name": "name",
        City: "city",
        Telephone: "phone.mobile",
        "Telephone 2": {
          field: "phone.landline",
          callback: value => {
            return `Landline Phone - ${value}`;
          }
        }
      },
      json_data: [
        {
          name: "Tony Peña",
          city: "New York",
          country: "United States",
          birthdate: "1978-03-15",
          phone: {
            mobile: "1-541-754-3010",
            landline: "(541) 754-3010",
            
          }
        },
        {
          name: "Thessaloniki",
          city: "Athens",
          country: "Greece",
          birthdate: "1987-11-23",
          phone: {
            mobile: "+1 855 275 5071",
            landline: "(2741) 2621-244"
          }
        },
        {
          name: "Carlos Galeano",
          city: "Athens",
          country: "Greece",
          birthdate: "1987-11-23",
          phone: {
            mobile: "+1 855 275 5071",
            landline: "(2741) 2621-244"
          }
        }
      ],
      json_meta: [
        [
          {
            key: "charset",
            value: "utf-8"
          }
        ]
      ],
      isExported: false,
    };
  },
  methods: {
    startDownload() {
        this.isExported = true
        console.log(this.isExported)
         
      alert("show loading")
      
    },
    activeDownload() {
   this.isExported = true
    console.log('boton download');
    console.log(this.isExported);
  
    },
    finishDownload() {
      alert("hide loading");
      // this.isExported = true;

       setTimeout(() => {
          this.isExported = false
        }, 3 * 1000)
        console.log(this.isExported);
    },
    /* exported(event) {
        console.log(event)
        this.isExported = true
        setTimeout(() => {
          this.isExported = false
        }, 3 * 1000)
      } */
  }
};
</script>
<style lang="scss">
 $icon-font-path: "~bootstrap-sass/assets/fonts/bootstrap/";
@import "node_modules/bootstrap-sass/assets/stylesheets/bootstrap";

</style>