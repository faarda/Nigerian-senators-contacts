<template>
  <div class="home">
    <h1>Search for senators contacts by name or state</h1>

    <div class="actions">
      <div class="search">
        <input type="text" v-model="query" @input="searchSenators"  placeholder="Enter name or state" class="form-input">
        <button class="btn">
          <span data-feather="search"></span>
        </button>
      </div>
      <button :disabled="results.length === 0" class="download-csv-btn" @click="downloadCSV(results, query)">
        Download CSV
      </button>
    </div>
    <div class="senators">
      <senator-view :id="++id" v-for="(senator, id) in results" :key="id" :senator="senator"></senator-view>
    </div>
  </div>
</template>

<script>
require('../../public/feather');
import senatorView from '@/components/Senator';
import senators from "../components/senators.js";
export default {
  name: 'home',
  components: {
    senatorView
  },
  data(){
    return {
      senators: [],
      results: [],
      query: ""
    }
  },
  created(){
    this.senators = senators.map((val, id) => {
      return {id: ++id, ...val}
    });
    this.results = [...this.senators];
  },
  mounted(){
    feather.replace();
  },
  methods:{
    searchSenators(){
      this.results = [...this.senators].filter((val) => {
        return val.state.toLowerCase().indexOf(this.query.toLowerCase()) !== -1 || val.name.toLowerCase().indexOf(this.query.toLowerCase()) !== -1;
      });
    },
    downloadCSV(data, query) {
      let csv = 'State,Name,Email,Phone\n';
      data.forEach((senator) => {
        csv += `${senator.state},${senator.name},${senator.email},${senator.phone}\n`;
      });

      let filePrefix = query || 'all';
      let anchor = document.createElement('a');

      anchor.href = 'data:text/csv;charset=utf-8,' + encodeURIComponent(csv);
      anchor.target = '_blank';
      anchor.download = `${filePrefix}-senators.csv`;
      anchor.click();
    }
  }
}
</script>

<style>
  .home{
    display: grid;
    grid-template-columns: minmax(70%, 500px);
    align-items: center;
    justify-content: center;
    margin: 50px auto;
  }

  h1{
    text-align: center;
  }


  .search{
    width: 70%;
    margin: 30px 10px;
    border: solid 1px rgba(0,31, 63, 0.70);
    display: flex;
    align-items: center;
    height: 50px;
    border-radius: 10px;
    overflow: hidden;
  }

  .search .form-input{
    height: 100%;
    flex: 1;
    border: 0;
    outline: 0;
    padding: 5px 15px;
    font-family: 'Lato', sans-serif;
  }

  .btn{
    outline: none;
    border: none;
    background: transparent;
    padding: 8px 10px;
    margin-right: 8px;
    border-radius: 5px;
    cursor: pointer;
    transition: .5s all;
  }

  .btn .feather{
    width: 16px;
    height: 16px;
    color: #008751;
    transition: .5s all;
  }

  .btn:hover{
    background: #008751;
  }

  .btn:hover > .feather{
    color: #f2f2f2;
  }

  .actions {
    margin: 60px 0;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: row wrap;
  }

  .download-csv-btn {
    height: 50px;
    padding: 15px;
    border-radius: 10px;
    border: 1px solid #008751;
    background-color: #008751;
    color: white;
    font-family: 'Lato', sans-serif;
    cursor: pointer;
  }

  .download-csv-btn:disabled {
    opacity: .5;
    cursor: auto;
  }

  .senators{
    margin: 30px auto;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-column-gap: 30px;
    flex-direction: column;
    align-items: center;
  }

  .senator{
    background: #ffffff;
    border: solid 1px #C7CAC7;
    border-radius: 10px;
    display: flex;
    margin-top: 30px;
    position: relative;
    margin-left: 75px;
    padding: 20px 20px 20px 105px;
    margin-bottom: 30px;
  }

  .senator-img{
    width: 150px;
    height: 150px;
    position: absolute;
    top: -25%;
    left: -60px;
  }

  .senator-img img{
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 15px;
  }

  .senator .details .name{
    margin-bottom: 15px;
  }

  .senator .details .name h3{
    margin-right: 10px;
    font-size: 18px;
  }

  .senator .details .name span{
    font-style: italic;
    color: rgba(0,31, 63, 0.70);
  }

  .senator .details .contacts p{
    margin-bottom: 5px;
  }

  a{
    color: #008751;
    text-decoration: none;
    transition: .5s all;
  }

  a:hover{
    text-decoration: underline;
  }

  @media screen and (max-width: 600px){
    .home{
      grid-template-columns: 95%;
    }

    h1{
      font-size: 22px;
    }

    .actions {
      display: block;
    }

    .search{
      width: 100%;
      margin-bottom: 10px;
      margin-left: 0;
      margin-right: 0;
    }

    .download-csv-btn {
      width: 100%;
    }

    .senators{
      width: 95%;
      grid-template-columns: 100%;
      grid-column-gap: 0;
    }

    .senator-img{
      width: 120px;
      height: 120px;
      top: -20%;
      left: 50%;
      transform: translateX(-50%);
    }

    .senator{
      margin-top: 50px;
      margin-left: 0px;
      padding: 100px 15px 15px 15px;
      margin-bottom: 30px;
    }

    .senator .details{
      margin: 0 auto;
      text-align: center;
    }
  }

</style>
