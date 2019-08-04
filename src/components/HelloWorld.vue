<template>
  <b-container class="bv-example-row">
    <b-row class="justify-content-md-center">
      <b-col cols="6">
        <b-form-file v-model="selectedFile" :state="Boolean(selectedFile)" placeholder="请选择Excel文件上传..."  @change="onSelectedFile"></b-form-file>
      </b-col>
    </b-row>
    <b-row class="justify-content-md-center"> 
      <b-col cols="6"><div class="mt-3">已选文件: {{ selectedFile ? selectedFile.name : '' }}</div></b-col>
    </b-row>
    <b-row class="justify-content-md-center">
      <b-col cols="6">
        <b-button  variant="primary" @click="executeFile" v-bind:disabled="!ableToExecute">执行</b-button>
        <b-button  variant="primary" @click="handleDownload" v-bind:disabled="!ableToDownload">下载</b-button>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import axios from 'axios';
export default {
  name: 'HelloWorld',

  data () {
    return {
      selectedFile: null,
      ableToDownload:false,
      ableToExecute:false,
      executeUrl:'/',
      downloadUrl:'/'
    }
  },
  methods:{
    onSelectedFile(event){
      this.selectedFile=event.target.files[0]
      this.ableToExecute=true;
    },
    executeFile(){
      if(!this.ableToExecute){
        return 
      }else{
        const fd = new FormData();
        fd.append('excel',this.selectedFile,this.selectedFile.name)
        axios.post(this.executeUrl,fd)
        .then(res=>{
          // Todo check if excuted successfully
          // If excuted successfully then this.ableToDownload=true
          console.log(res)
        })
        .catch((error)=>{
          console.log(error)
        })
        .finally(
        )
      }
    },
    handleDownload(){
      if(!this.ableToDownload){
        return 
      }else{
        // TODO axios.post download api
        axios.post(this.downloadUrl)
        .then((res)=>{
          console.log(res)
        })
        .catch((error)=>{
          console.log(error)
        })
      }
    }

  }
  
}
</script>

