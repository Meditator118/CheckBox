<template>
  <div class="continer" >
    <div class="top-nav">
        <div class="title">Status</div>
        <div class="dot" v-if="count!=0">{{count}}</div>
    </div>
    <div class="option" >
        <table class="option-list" @click="select">
        </table>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import type { PropType } from 'vue'
interface boxCell {
  label: string
  value: number
}
export default defineComponent ({
    props:{
        options:{
            type: Array as PropType<boxCell[]>,
            required: true,
        },
        columns:{
            type:Number,
            required: true
        }
    },
    data(){
        return{
            count:0
        }
    },
  mounted() {
    if(this.columns<1||this.options.length<1){
        throw new Error("invaild data for checkBox components");
    }
    console.log('11223');
    let tbody=document.querySelector('.option-list')!;
    let rows=Math.ceil((this.options.length+1)/this.columns)
    let trlist=[]
        for(let i=0;i<rows;i++){
            let tr = document.createElement('tr');
            tbody.appendChild(tr);
            trlist.push(tr)
        }
        let index=0
        for (let j = 0; j < this.columns; j++) {
            
            for (let k = 0; this.columns*k+j<=this.options.length; k++) {
                let td = document.createElement('td');
                let checkbox = document.createElement('input');
                checkbox.type='checkbox'
                let text
                if(k==0&&j==0){
                    text=document.createTextNode('Select All');
                    checkbox.addEventListener('click',this.selelectALL)
                }else{
                    text=document.createTextNode(this.options[index].label);
                    index++;
                }
                td.appendChild(checkbox); 
                td.appendChild(text); 
                trlist[k].appendChild(td);
            }
        }
    console.log(tbody);
  },
  methods:{
    
  select(e:Event){
    let target = e.target!;
    if ((target as HTMLElement).tagName != 'INPUT'){
        return;
    }else{
        if((target as HTMLInputElement).checked){
            this.count++
        }else{
            this.count--
        }
    }
    let selectAll=document.getElementsByTagName('input')[0]
    if(this.count==this.options.length){
        selectAll.checked=true
    }else{
        selectAll.checked=false
    }
    console.log(this.count);
  },
  selelectALL(e:Event){
    e.stopPropagation()
    let checked=(e.target as HTMLInputElement).checked
    let List =document.getElementsByTagName('input')
    if(checked){
        this.count=this.options.length
    }else{
        this.count=0
    }
    for (let i=1;i<=this.options.length;i++) {
            List[i].checked=checked
        }
  }

  }
  
});

</script>

<style>
.continer{
    display: inline-block;
    width: auto;  
    background: rgb(222, 222, 222);
    margin: 200px auto;
}
.continer .top-nav{
    width: 100%;
    height: 40px;
    display: flex;
    background: black;
    align-items: center;
}
.continer .top-nav .title{
    color: white;
    font-size: 20px;
    margin-left: 30px;
}
.continer .top-nav .dot{
    width: 25px;
    height: 25px;
    border-radius: 25px;
    background: red;
    margin-left: 20px;
    text-align: center;
    line-height: 25px;
}
.continer .option{
    padding: 5px;
    box-sizing: border-box;
}
.continer .option .option-list{
    background: rgb(155, 155, 155);
}
.continer .option .option-list td{
    min-width: 80px;
    height: 30px;
    text-align: left;
    white-space:nowrap
}
</style>
