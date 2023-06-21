
  <v-app>
    <v-main>
      <v-container>
        <v-row>
          <v-col>
            <v-btn
              color="yellow"
              v-on:click="deleteTodoList(), deleteAllToDo = !deleteAllToDo"
              block
            >
              Удалить весь список
            </v-btn>
          </v-col>
          <v-col>
            <v-btn
            block
              color="blue"
              v-on:click="create = !create"
            >
            Создать ToDO
             </v-btn>
             <v-bottom-sheet hide-overlay v-model="create">
               <v-sheet class="text-center" height="300px">
                 <v-row>
                   <v-btn
                     v-on:click="createToDo()"
                     @click="create = !create"
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
                            v-on:click="deleteToDoById(), deleteToDo = !deleteToDo"
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
                          v-on:click="updateToDoById(todo.id), update = !update"
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
</template> -->
<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row>
          <v-col>
            <v-btn
              color="red"
              v-on:click= "deleteAllToDo = !deleteAllToDo"
            >
              Удалить весь список
            </v-btn>
            <v-bottom-sheet persistent v-model="deleteAllToDo">
              <v-sheet class="text-center">
                Подтверждение
                <v-row>
                  <v-col>
                    <v-btn
                      color="green"
                      v-on:click="deleteAllToDo = !deleteAllToDo"
                      block
                      medium
                    >
                      Нет
                    </v-btn>
                  </v-col>
                  <v-col>
                    <v-btn
                      color="red"
                      v-on:click="deleteTodoList(), deleteAllToDo = !deleteAllToDo"
                      block
                      medium
                    >
                      Да
                    </v-btn>
                  </v-col>
                </v-row>
              </v-sheet>
            </v-bottom-sheet>
          </v-col>
        <v-col></v-col><v-col>
            <v-btn
              color="green"
              v-on:click="deleteFields(), create = !create"
              block
            >
              Создать ToDO
            </v-btn>
            <v-bottom-sheet persistent v-model="create">
              <v-sheet class="text-center">
                <v-row>
                  <v-btn
                    v-on:click="createToDo(), create = !create"
                    block
                    color = "green"
                  >
                    Готово
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
                <v-btn color = "red"
                v-on:click="create = !create" block>
                  Закрыть
                </v-btn>
              </v-sheet>
            </v-bottom-sheet>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-btn v-on:click="getFullData()" color="orange" block>
              Получить список
            </v-btn>
          </v-col>
        </v-row>
        <v-row v-for="todos in todoList" :key="todos.id">
          <v-col>
            <v-card>
              <v-row>
                <v-col>
                  <v-card-title> {{ todos.title }} </v-card-title>
                </v-col>
                <v-col class="text-right">
                  <v-btn v-on:click="deleteToDo = !deleteToDo, setId(todos.id)">
                    Удаление 
                  </v-btn>
                  <v-bottom-sheet persistent v-model="deleteToDo">
                    <v-sheet class="text-center">
                      Подтверждение
                      <v-row>
                        <v-col>
                          <v-btn
                            color="green"
                            v-on:click="deleteToDo = !deleteToDo"
                            block
                            medium
                          >
                            Нет
                          </v-btn>
                        </v-col>
                        <v-col>
                          <v-btn
                            color="red"
                            v-on:click="deleteToDoById(), deleteToDo = !deleteToDo"
                            block
                            medium
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
                  <v-card-text> {{ todos.description }} </v-card-text>
                </v-col>
                <v-col class="text-right">
                  <v-btn
                    v-on:click="setFields(todos.title, todos.description), setId(todos.id), update = !update"
                  >
                      Изменение
                  </v-btn>
                  <v-bottom-sheet v-model="update">
                    <v-sheet class="text-center">
                      <v-row>
                        <v-btn
                          v-on:click="updateToDoById(todos.id), update = !update"
                          color="green"
                          block
                          medium
                        >
                          Готово
                        </v-btn>
                      </v-row>
                      <v-container>
                        <v-row>
                          <v-col>
                            <v-text-field label="title" 
                            v-model="title"
                            >
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
                      <v-btn v-on:click="update = !update"
                      color="red"
                      block>
                        Закрыть
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

    setFields(title, description){
      this.title = title;
      this.description = description;
    },
    deleteFields(){
      this.title = "";
      this.description = "";

    },
    setId(id) {
      this.id = id;
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
    console.log("all ToDo", res.data.allToDo);
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
    this.deleteFields()
    this.getFullData()
  
  },

  async createToDo(){
    await axios.post("http://localhost:3000/api/todos/", {
        title: this.title,
        description: this.description,
    })
      .catch((error) => {
        console.log(error);
    }).then(data =>{
      this.deleteFields();
      this.getFullData()
    });
    
  },

  async deleteTodoList(){
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
