<script>
import Vue from 'vue'
export default {
  name:"dynamic",
props: ['template'],
data() {
    return {
      templateRender: null,
    };
  },
methods:{		checked(ele){
					this.$parent.livetype='checkbox'
            this.$parent.livecell = ele.target.name
            this.$parent.livevalue = ele.target.value
            this.$parent.fieldedit = ele.target.name
            this.$parent.valueedit = ele.target.value
  },
              checkclick(ele){
            //console.log(ele)
            //console.log("Edit field should update")
            //console.log(this)
            this.$parent.livetype='checkbox'
            this.$parent.livecell = ele.target.control.name
            this.$parent.livevalue = ele.target.control.value
            this.$parent.fieldedit = ele.target.control.name
            this.$parent.valueedit = ele.target.control.value
            },
clickele(){

  },
            loadeditpanel(ele){
            //console.log(ele.target.name)
            ele.target.id
            //console.log("LOADED")
            //console.log(this)
          this.$parent.livetype ="text"
            ////console.log(this.$refs.inputs.name)
            this.$parent.livecell = ele.target.name
            this.$parent.livevalue = ele.target.value
            this.$parent.fieldedit = ele.target.name
            this.$parent.valueedit = ele.target.value
            
            }
  },
render(h) {
    if (!this.templateRender) {
      return h('div', 'loading...');
    } else { // If there is a template, I'll show it

      return this.templateRender();
    }
  },
watch: {
// Every time the template prop changes, I recompile it to update the DOM
	template:{
      immediate: true, // makes the watcher fire on first render, too.
      handler() {
        console.log(this)
        var res = Vue.compile("<div v-on:click='clickele'>"+this.template+"</div>");
				////console.log(this)
        this.templateRender = res.render;
        
        // staticRenderFns belong into $options, 
        // appearantly
        this.$options.staticRenderFns = []
        
        // clean the cache of static elements
        // this is a cache with the results from the staticRenderFns
        this._staticTrees = []
        
        // Fill it with the new staticRenderFns
        for (var i in res.staticRenderFns) {
          //staticRenderFns.push(res.staticRenderFns[i]);
          this.$options.staticRenderFns.push(res.staticRenderFns[i])
        }
      }
    }
  },
}

    String.prototype.capitalize = function() {
 return this.charAt(0).toUpperCase() + this.slice(1);
    }
</script>