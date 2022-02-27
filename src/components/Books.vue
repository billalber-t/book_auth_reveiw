<template>
 <div class="books">
    <v-container>
       <v-row>
          <h1>BOOKS TABLE</h1>
       </v-row>
       <v-row>
          <v-data-table
            :headers="headers"
            :items = "details"
            class="elevation-1"
          >
         <template v-slot:top>
            <v-toolbar flat>
               <v-spacer></v-spacer>
                <v-dialog
                  v-model="dialog"
                  max-width="500px"
                  v-if="dialog"
                  >
                  <template v-slot:activator="{on, attrs}">
                     <v-btn 
                        color="primary"
                        class="mb-2"
                        v-bind="attrs"
                        v-on="on"
                     >
                        New Item
                     </v-btn>

                  </template>
                  <!-- NEW ITEM card -->
                  <v-card >
                     <v-card-title>
                        <span>NEW ITEM</span>
                     </v-card-title>
                     <v-card-text>
                           <v-container>
                              <!-- NEW ITEM -->
                           
                              <v-row>
                                 <v-col
                                 cols="12"
                                 sm="6"
                                 md="4"
                                 >
                                 <v-text-field
                                 v-model="newItem.title"
                                 label="Title">

                                 </v-text-field>
                                 </v-col>
                                 
                                 <v-col cols="12" sm="6" md="4">
                                 <v-text-field
                                 v-model="newItem.author"
                                 label="Author">

                                 </v-text-field>
                                 </v-col>

                                 <v-col cols="12" sm="6" md="4">
                                 <v-text-field
                                 v-model="newItem.description"
                                 label="Description"
                                 >

                                 </v-text-field>
                                 </v-col>

                                 <v-col cols="12" sm="6" md="4">
                                 <v-text-field
                                 v-model="newItem.date_of_publication"
                                 label="Date of Publication"
                                 >
                                 </v-text-field>
                              
                                 </v-col>
                              </v-row>
                           
                              

                           </v-container> 
                        </v-card-text>   
                        <v-card-actions>
                           <v-btn
                           color="blue"
                           text
                           @click="this.dialog = false"
                           >
                              Cancel
                           </v-btn>
                           <v-spacer></v-spacer>
                           <v-btn
                              color="blue"
                              text
                              @click="createRecord"
                           >
                              Create
                           </v-btn>
                        </v-card-actions>         
               
                  </v-card>
               </v-dialog>
                  <!-- EDIT ITEM card -->
               <v-dialog
                v-model="dialogEdit"
                max-width="500px"
                v-if="dialogEdit"

               >
                 
                  <v-card >
                     <v-card-title>
                        <span>EDIT ITEM</span>
                     </v-card-title>
                     <v-card-text>
                           <v-container>
                           
                              <v-row>
                                 <v-col
                                 cols="12"
                                 sm="6"
                                 md="4"
                                 >
                                 <v-text-field
                                 v-model="editedItem.title"
                                 label="Title">

                                 </v-text-field>
                                 </v-col>
                                 
                                 <v-col cols="12" sm="6" md="4">
                                 <v-text-field
                                 v-model="editedItem.author"
                                 label="Author">

                                 </v-text-field>
                                 </v-col>

                                 <v-col cols="12" sm="6" md="4">
                                 <v-text-field
                                 v-model="editedItem.description"
                                 label="Description"
                                 >

                                 </v-text-field>
                                 </v-col>

                                 <v-col cols="12" sm="6" md="4">
                                 <v-text-field
                                 v-model="editedItem.date_of_publication"
                                 label="Date of Publication"
                                 >
                                 </v-text-field>
                              
                                 </v-col>
                              </v-row>
                           
                              

                           </v-container> 
                        </v-card-text>   
                        <v-card-actions>
                           <v-btn
                           color="blue"
                           text
                           @click="this.dialogEdit = false"
                           >
                              Cancel
                           </v-btn>
                           <v-spacer></v-spacer>
                           <v-btn
                              color="blue"
                              text
                              @click="editRecordConfirm"
                           >
                              Edit
                           </v-btn>
                        </v-card-actions>         
               
                  </v-card>

               </v-dialog>




                <!-- <v-dialog v-model="dialogDelete">
                   <v-card class="text-h5">
                      <v-card-title>Are you sure you want to delete this item?</v-card-title>
                   </v-card>
                   <v-card-actions>
                      <v-btn color="blue darken-1" text @click="dialogDelete=false ">Cancel</v-btn>
                      <v-spacer></v-spacer>
                     <v-btn color="blue darken-1" text @click="deleteRecord(item)">Delete</v-btn>

                   </v-card-actions>
                </v-dialog> -->
            </v-toolbar>
         </template>
         <template v-slot:[`item.actions`]= "{ item }"> 
            <v-icon
             small
             class="mr-2"
             @click="editRecord(item)"
            >mdi-pencil</v-icon>
            <v-icon
             small
             class="mr-2" 
              @click="deleteRecord(item)"
            >mdi-delete
            </v-icon>
            
         </template>

          </v-data-table>
       </v-row>
    </v-container>
     
 </div>
    
</template>
<script>
import axios from 'axios'
export default {
   name : "Books",
   
   data(){
      return{
         dialog: false,
         dialogEdit : false,
         newItem :{
                  date_of_publication:'',
                  author:'',
                  title:'',
                  description:''

               },
         editedItem: {
                  date_of_publication: "",
                  author: '',
                  title: '',
                  description: '',
                  _id:''
               },
               
         headers:[
            {
               text:'Title', 
               value:'title',
               align:'start',
               sortable: false
            },
             {
               text:'Author', 
               value:'author',
               sortable: false
            },
             {
               text:'Description', 
               value:'description',
               sortable: false
            },
             {
               text:'Date of Publication', 
               value:'date_of_publication',
            
            },
            {
               text:'Actions',
               value:'actions',
            }
         ],
         details:[]
      }
   },

   methods:{
         initialize(){

            
         axios
            .get("https://crudcrud.com/api/1c7476859438413a9442416090f1d8ca/books")
            .then((response)=>{
                  console.log("GET books REQUEST successfull")
                  this.details = response.data.reverse()
            })
            .catch((error)=>{
               console.log("ERROR in the GET books Request" + error.response)
            })

         },

         deleteRecord(item){
            axios
               .delete(`https://crudcrud.com/api/1c7476859438413a9442416090f1d8ca/books/${item._id}`)
               .then(()=>{
                  console.log("DELETE request SUCCESSFULL")
                  this.initialize()
               })
               .catch((error)=>{
                  console.log("ERROR in the DELETE request" + error.response)
               })
         },
         createRecord(){
            axios
               .post("https://crudcrud.com/api/1c7476859438413a9442416090f1d8ca/books",this.newItem)
               .then(()=>{
                  console.log("POST request SUCCESSFULL")
                  this.close()
                  this.initialize()
                  
               })
               .catch((error)=>{
                  console.log("ERROR in the POST request" + error.response)
               })
         },
          editRecord(item){
            this.dialog = false;
            this.dialogEdit = true;
            this.editedItem = Object.assign({}, item);
         
         },
         editRecordConfirm(){
            
            axios
               .put(`https://crudcrud.com/api/1c7476859438413a9442416090f1d8ca/books/${this.editedItem._id}`,
                  {
                     title : this.editedItem.title , 
                     author : this.editedItem.author,
                     description : this.editedItem.description,
                     date_of_publication : this.editedItem.date_of_publication
                  }
               )
               .then(()=>{
                  this.dialogEdit = false
                  console.log("PUT request SUCCESSFULL")
                  this.initialize()
               })
               .catch((error)=>{
                  console.log("ERROR in the PUT request" + error.response)
               })
         },


         close(){
            this.dialog=false
         }
        
   },
   created(){
         this.initialize()
   }


   
}
</script>