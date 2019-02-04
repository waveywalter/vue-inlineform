/* eslint-disable */ 
<template>
<div id="mainContent">
           
        
<span style="color:red">{{error}}</span><br>
<button type="button " class="btn btn-primary" v-on:click="addinput()">
Add Text Field 
</button><br>
<button type="button " class="btn btn-primary" v-on:click="addcheck()">
Add Checkbox 
</button><br>
  <input type="checkbox" ref="labelled" id="label" name="label" value="Label" v-model="labelled">
  <label for="label">Labeled</label><input name="labelvalue" type="text" id="labelvalue" v-model="labelvalue">
  <div>
  <label for="valuevalue">Default value</label>
  <input name="valuevalue" type="text" id="valuevalue" v-model="valuevalue" >
  </div>
  <div class="flexor">
  
  <div>
  {{text | removehtml}}
  </div>
  </div>
<textarea ref="edit" id="textarea" contenteditable="true" style="width:400px;height:300px;background-color:white;color:black" v-model="text">



</textarea>
<div>
Edit Input Field<span style="color:red">{{error2}}</span>
<input ref="fieldedit" id="fieldedit" v-model="fieldedit" v-on:change="updatetext">
<input ref="valueedit" id="valueedit" v-model="valueedit" v-on:change="updateval">
<button v-on:click="removeInput">
Remove Field
</button>
</div>
<dynamic ref="dynamic" v-bind:template="text"></dynamic>
</div>

</template>

<script>
import dynamic from './dynamic'

export default {
  name: 'FormBuilder',
  data: 
function(){
            return {       
              fieldedit:'',
              valueedit:'',
            labelled:false,
            labelvalue:'',
            valuevalue:'',
            livetype:'',
                text:'',
                fnames:[],
                error:'',
                error2:''
            }
      
            },
            filters:{
              removehtml(input){
              var n = input.replace(/<input ref='inputs' v-on:click='loadeditpanel' type='text' name='[a-zA-Z0-9 ]*' value='[a-zA-Z0-9 ]*' id='[a-zA-Z0-9 ]*' disabled>/g, " [input type='text'] ")
              n = n.replace(/<label v-on:click='checkclick' for='[a-zA-Z0-9 ]*'>[a-zA-Z0-9 ]*<\/label><input ref='[a-zA-Z0-9 ]*' v-on:focus='checked' type='checkbox' name='[a-zA-Z0-9 ]*' value='[a-zA-Z0-9 ]*' id='[a-zA-Z0-9 ]*' disabled>/,"[input type='checkbox']")
              //var n = input.replace(/\<.*\>/, " [input type='checkbox'] ")
              return n
            },
            formalize(input){
            //console.log(input)
            let newer = input.replace("[input test]","<input type='text'>")
            return newer
            }
            },
             components: {
               dynamic
            },
            computed:{
            text2:{
              get: function () {
      return this.text
          },
      // setter
        set: function (newValue) {
      this.text2 = newValue
    }
            }
            },
  methods:{
						
						
            removeInput(){
            //console.log(this)
            //console.log(ele)
            this.$delete(this.$refs.valueedit)
            //remove html from text
            //console.log(this.livetype)
            if(this.livetype=="text"){
            var remove = "<input ref='inputs"+this.livecell+"' v-on:focus='loadeditpanel' type='text' name='"+this.livecell+"' value='"+this.livevalue+"' id='"+this.livecell+"'>"}
            if(this.livetype=="checkbox"){
               remove = "<label v-on:click='checkclick' for='"+this.livecell+"'>"+this.livecell.capitalize()+"</label><input ref='inputs"+this.livecell+"' v-on:focus='checked' type='checkbox' name='"+this.livecell+"' value='"+this.livevalue+"' id='"+this.livecell+"' disabled>"
            }
            //console.log(remove,this.text,this.livecell)
            this.text = this.text.replace(remove,"")
             let nfnames = this.fnames.filter(name=>name!=this.livecell)
            this.fnames = nfnames;
            this.fieldedit=''
             this.valueedit=''
            this.livecell=''
            this.livevalue=''
            },
            updateval(){
            //console.log("UPDATE VLAUE")
            //console.log(this)
            let newval = this.$refs.valueedit.value;
            //console.log(this.text)
            //console.log(this.livevalue,newval)
            this.text = this.text.replace("value='"+this.livevalue+"'","value='"+newval+"'")
            this.livevalue = newval
            },
            updatetext(){
            //console.log("UPDATE TEXT")
            //console.log(this)
            let newval = this.$refs.fieldedit.value;
            if(!this.fnames.includes(newval)){
            //console.log("NEWWWWWWWWWWWWWWWWWWWWWWWWWW")
            let _t = this;
            let nfnames = this.fnames.filter(name=>name!=_t.livecell)
            this.fnames = nfnames;
            nfnames.push(newval)
            //console.log("NEW")
            //console.log(this)
            //console.log(this.livecell,newval)
            this.text = this.text.replace("name='"+this.livecell+"'","name='"+newval+"'")
            this.livecell = newval
            }
            else{
            //console.log("OLDDDDDDDDDDDDDDDDDDDDDDDDDDD")
                      this.error2 = "Label must be unique"
                  let _t = this
                  setTimeout(()=>{_t.error2=''},3000)
            }
            },
            loadeditpanel(){
            //console.log("LOADED2")
            },
            addinput(){
                    var val = '';
                  var id = '';
                  var name ='';
                  //console.log("addinout")
                  //console.log(this)
                if(!this.fnames.includes(this.labelvalue)){
                  if(this.labelled==true){
                  val = this.valuevalue;
                  id = this.labelvalue;
                  name =this.labelvalue;
                  }
                  this.fnames.push(this.labelvalue)
                  this.$refs.edit.value = this.$refs.edit.value+"<input ref='inputs"+
                  name+"' v-on:click='loadeditpanel' type='text' name='"+name+"' value='"+val+"' id='"+id+"' disabled>";
                  this.$refs.edit.dispatchEvent(new Event('input'))
                  }
                  else{
                  this.error = "Field must be unique"
                  let _t = this
                  setTimeout(()=>{_t.error=''},3000)
                  }
               },            	 
               addcheck(){
                  var val = '';
                  var id = '';
                  var name ='';
                  //console.log("addcheck")
                  //console.log(this)
                if(!this.fnames.includes(this.labelvalue)){
                if(this.labelled==true){
                  val = false;
                  id = this.labelvalue;
                  name =this.labelvalue;
                  }
                  this.fnames.push(this.labelvalue)
                  this.$refs.edit.value = this.$refs.edit.value+"<label v-on:click='checkclick' for='"+name+"'>"+name.capitalize()+"</label>"
                  +"<input ref='inputs"+name+"' v-on:focus='checked' type='checkbox' name='"+name+"' value='"+val+"' id='"+id+"' disabled>";
                  this.$refs.edit.dispatchEvent(new Event('input'))
                  }
                  else{
                  this.error = "Label must be unique"
                  let _t = this
                  setTimeout(()=>{_t.error=''},3000)
                  }
               }
            }
}




        String.prototype.capitalize = function() {
    return this.charAt(0).toUpperCase() + this.slice(1);
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.flexor{
  display:flex
}
</style>



