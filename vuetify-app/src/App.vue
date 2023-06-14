<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row>
          <v-col>
            <v-btn
              color="yellow"
              v-on:click="deleteAll()"
              block
            >
              УДАЛИТЬ ВЕСЬ СПИСОК
            </v-btn>
            
          </v-col>
          <v-col>
            <v-btn
            block
              color="blue"
              v-on:click="createToDo()"
            >
            СОЗДАТЬ ToDO
             </v-btn>
             <v-bottom-sheet hide-overlay v-model="create">
               <v-sheet class="text-center" height="300px">
                 <v-row>
                   <v-btn
                     v-on:click="createToDo(), create = !create"
                     color="green"
                     block
                   >
                     Готово!
                   </v-btn>
                 </v-row>
                 <v-container>
                   <v-row>
                     <v-col>
                       <v-text-field label="title" v-model="title">
                       </v-text-field>
                     </v-col>
                     <v-col>
                       <v-text-field label="description" v-model="description">
                       </v-text-field>
                     </v-col>
                   </v-row>
                 </v-container>
                 <v-btn text color="red" @click="create = !create">
                   Закрыть
                 </v-btn>
               </v-sheet>
             </v-bottom-sheet>
           </v-col>
         </v-row>
         <v-row>
           <v-btn v-on:click="getFullData()" color="pink" block>
             Получить список
          </v-btn>
        </v-row>
        <v-row v-for="todo in todoList" :key="todo.id">
          <v-col>
            <v-card>
              <v-row>
                <v-col>
                  <v-card-title> {{ todo.title }} </v-card-title>
                </v-col>
                <v-col class="text-right">
                  <v-btn v-on:click="deleteToDo = !deleteToDo, setID(todo.id)" >
                  </v-btn>
                  <v-bottom-sheet persistent v-model="deleteToDo">
                    <v-sheet class="text-center" height="100px">
                      <div>Вы уверены, что хотите удалить ToDo?</div>
                      <v-row>
                        <v-col>
                          <v-btn
                            text
                            color="green"
                            v-on:click="deleteToDo = !deleteToDo"
                            block
                            large
                          >
                            Нет
                          </v-btn>
                        </v-col>
                        <v-col>
                          <v-btn
                            text
                            color="red"
                            v-on:click="deleteToDoById()"
                            block
                            large
                          >
                            Да
                          </v-btn>
                        </v-col>
                      </v-row>
                    </v-sheet>
                  </v-bottom-sheet>
                </v-col>
              </v-row>
              <v-row>
                <v-col>
                  <v-card-text> {{ todo.description }} </v-card-text>
                </v-col>
                <v-col class="text-right">
                  <v-btn
                    v-on:click="setFields(todo.title, todo.description), setID(todo.id)">
                  </v-btn>
                  <v-bottom-sheet hide-overlay v-model="update">
                    <v-sheet class="text-center" height="300px">
                      <v-row>
                        <v-btn
                          v-on:click="updateToDoById(todo.id)"
                          color="green"
                          block
                        >
                          Готово!
                        </v-btn>
                      </v-row>
                      <v-container>
                        <v-row>
                          <v-col>
                            <v-text-field label="title" v-model="title">
                            </v-text-field>
                          </v-col>
                          <v-col>
                            <v-text-field
                              label="description"
                              v-model="description"
                            >
                            </v-text-field>
                          </v-col>
                        </v-row>
                      </v-container>
                      <v-btn text color="error" @click="update = !update">
                        Close
                      </v-btn>
                    </v-sheet>
                  </v-bottom-sheet>
                </v-col>
              </v-row>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

            

<script>
import axios from "axios"



export default {
  name: 'App',

  data: () => ({
    create: false,
    update: false,
    deleteAllToDo: false,
    deleteToDo: false,
    title: "",
    description: "",
    todoList: [],
    id: "",

  }),
  methods: {

    setFields(title, description, id){
      this.title = title;
      this.description = description;
      this.id = id;

    },
    deleteFields(){
      this.title = "";
      this.description = "";

    },
    setId(id) {
      this.id = id;
      this.deleteToDo = !this.deleteToDo;
    },

  async deleteToDoById() {
    await axios
      .delete("http://localhost:3000/api/todos/" + this.id)
      .catch((error) => {
      console.log(error);
    });
    this.getFullData();
  },
  
  async getFullData(){
    await axios.get("http://localhost:3000/api/todos/").then(res =>
    {
    console.log("all ToDo", res.data.todoList);
    this.todoList = res.data.allToDo;
    })
  },

  async updateToDoById() {
    await axios
      .patch("http://localhost:3000/api/todos/" + this.id,{
        title: this.title,
        description: this.description,
    })
      .catch((error) => {
      console.log(error);
    });
  
  },

  async createToDo(){
    await axios.post("http://localhost:3000/api/todos/", {
        title: this.title,
        description: this.description,
    })
      .catch((error) => {
        console.log(error);
    }).then(data =>{
      this.getFullData()
    });
    this.create = !this.create;
  },

  async deleteAll(){
    await axios
      .delete("http://localhost:3000/api/todos/")
      .catch((error) => {
        console.log(error);
      }).then(data =>{
      this.getFullData()
      });
    this.deleteAllToDo = !this.deleteAllToDo;
  }
}
}
</script>
