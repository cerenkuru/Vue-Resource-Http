<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6 col-md-offset-3">
        <h3>Vue-Resource</h3>
        <div class="form-group">
          <input type="text class=form-control" v-model="userName">
        </div>
        <button class="btn btn-primary" @click="saveUser">Kaydet</button>
        <button class="btn btn-success" @click="getUser">Verileri Al</button>
        <hr>
        <ul class="list-group">
          <li class="list-group-item" v-for="user in userList">
            <span>{{ user.data.userName }}</span>
            <button class="btn btn-xs btn-danger" @click="deleteUser(user.key)">Sil</button>

          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      userName : null,
      userList : [],
      resource : {}
    }
  },
  methods : {
     saveUser(){
    //   this.$http.post("users.json", { userName : this.userName})
    //     .then((response)=> {
    //     console.log(response);
      //  })
    // this.$resource("users.json").save({}, { userName : this.userName});
    this.resource.kaydet({}, {userName : this.userName});
    },
    getUser(){
      

      this.$resource("users.json").get()
        .then((response)=> {
         return response.json();
        }).then(data =>{
          for(let key in data.userList){
            // console.log(data[key]);
            this.userList.push(
            {
              key: key,
              data: data.userList[key]

            }

            )
          }
        })
    },
    deleteUser(userKey){
    // this.$http.delete("users/" + userKey + ".json")
    // .then(response => {
    //   console.log(response)
    // })
    this.$resource.delete("users/" + userKeu + ".json");
 }



  },
  created(){
    const customActions = {
      kaydet : { method : "POST", url : "users.json"}

    };
    this.resource = this.$resource("users.json", {},customActions);
  }
}
</script>

<style>
</style>
