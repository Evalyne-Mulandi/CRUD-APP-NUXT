<template>
    <div class="">
        <h3 class=" text-2xl  font-bold text-left py-2 ">Product list</h3>

        <div class="flex justify-center items-end space-x-3">
      <div>
        <h1>Name</h1>
        <input type="text" class="border border-gray-500 px-3 py-2" v-model="name">
      </div>
      <div>
        <h1>color</h1>
        <input type="text" class="border border-gray-500 px-3 py-2" v-model="color">
      </div>
      <div>
        <h1>category</h1>
        <input type="text" class="border border-gray-500 px-3 py-2" v-model="category">
      </div>
      <div>
        <h1>price</h1>
        <input type="text" class="border border-gray-500 px-3 py-2" v-model="price">
      </div>
      <div>
        <button class="bg-gray-600 text-white py-2 px-3   hover:bg-gray-500" @click="saveData(haveID)">Save</button>
      </div>
     

        </div>
        <div class="overflow -x- auto relative sm:rounded-lg  p-10"></div>
<table class="w-full text-sm text-left bg-slate-600  text-gray-500 dark:text-gray-400">
    <thead class=" text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400  ">
        <tr>
            <th scope="col" class="py-3 px-6 text-lg">product name</th>
            <th scope="col" class="py-3 px-6 text-lg">color</th>
            <th scope="col" class="py-3 px-6 text-lg">category</th>
            <th scope="col" class="py-3 px-6 text-lg">price</th>
            <th scope="col" class="py-3 px-6  text-right text-lg">Action</th>
        </tr>
    </thead>
 <tbody>
    <tr class=" bg-white border-b  dark:bg-gray-800 dark:border-gray-800" v-for="product in products" :key="product.id">
     
    <th class="py-4 px-6">{{product.name}}</th>
    <td class="py-4 px-6"> {{product.color}}</td>
    <td class="py-4 px-6"> {{product.category }}</td>
    <td class="py-4 px-6"> {{product.price }}</td>
    <td  class="py-4 px-6 text-right">
        <div class="inline-flex gap-1">
            <button class="bg-blue-500  hover:bg-blue-400 text-white font-bold py-2 px-4 rounded-l "  @click="getData(product.id)" >Edit</button>
            <button class="bg-red-500  hover:bg-red-400 text-white font-bold py-2 px-4 rounded-l"  @click="deleteData(product.id)">Delete</button>
        </div>
    </td>
</tr>
    
 </tbody>
</table>
    </div>
</template>
 <script>
 export default {
 data(){
    return{
        name:'',
        color:'',
        category:'',
        price:0,
        haveID:null,

        products:[
            {
                id:1,
                name:"Apple",
                color:"Silver",
                category:'laptop',
                price:2999

            },
            
        ]
    }
 },
methods:{
    deleteData(id){
        //index is index of id we want to delete
       let index =this.products.findIndex((product) => product.id==id)
        //onsole.log(index)
        //remove data by index and remove i item
        this.products.splice(index, 1)
      console.log(index);
    },
    getData(id){
       this.haveID=id
       var dataObj = this.products.filter((product) =>(product.id==id))
       //assign to input
       this.name=dataObj[0].name
       this.color=dataObj[0].color
       this.category=dataObj[0].category
       this.price=dataObj[0].price

        },
    saveData(haveID){
        //update data
        if(haveID){
            var dataObj = this.products.filter((product) =>(product.id==haveID))
            dataObj[0].name= this.name
            dataObj[0].color= this.color
            dataObj[0].category= this.category
            dataObj[0].price= this.price
        }else{ 
            //add data
        const id = this.products.length +1
        const data = {
            id:id,
            name:this.name,
            color:this.color,
            category:this.category,
            price:this.price,
            }
            this.products.push(data);
        }
        }

    }
 }
 </script>