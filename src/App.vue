<template>
<div id="app" class= "container">
  <div class="row">
    <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-offset-3">
      <div class="form-group">
          <label for="name">Name</label>
          <input type="text" name="name" id="name"  class="form-control" v-model= "user.name">
      </div>
      <div class="form-group">
          <label for="name">Email</label>
          <input type="text" name="mail" id="name"  class="form-control" v-model = "user.mail">
      </div>
      <div class="form-group">
          <button class="btn btn-primary form-control" @click.prevent = "submit">Submit</button>
      </div>
      <br>
      <input type="text" name="getData" id="dta" class="form-control" v-model= "node">
      <button class="btn btn-primary" @click ="fetch">Get Data</button>
      <ul class="list-group">
        <li class="list-item" :key= "index" v-for= "(x,index) in udata">
          <pre>Name:{{x.name}}</pre>
          <pre>Mail:{{x.mail}}</pre>

        </li>
      </ul>
    </div>
  </div>
</div>

</template>
<script>
export default {
  data(){
    return{
      user:{
        name:'',
        mail:''
      },
      udata:[],
      resource:{},
      altSave:{},
      node:'data'

    }
  },
  methods:{
    submit(){
      // this.$http.post('',this.user).then(Response=>{
      //   console.log(Response),console.error();})

      // this.resource.save({},this.user)
      this.altSave.alterSave(this.user)
      this.user.name =""
      this.user.mail =""
    },
    fetch(){
      this.$http.get('').then(Response=>Response.json()).then(data=>{
        const dt = []
        for(let k in data){
          dt.push(data[k])
        }
        this.udata = dt
      });
      //this.resource.getData({node:this.node})
    }
  },
  created(){
    const alt = {
      alterSave:{method:'POST',URL :'altlk.json'},
      // getData :{method:'GET'}
    }

    this.altSave = this.$resource('data.json',{},alt)
    //this.resouce = this.$resource('{node}.json,{},alt)
  }

}
</script>
<style scoped>

</style>
