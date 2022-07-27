<template>
  <section>
    <div class="signup-form">
      <Toast />
      <div class="error" v-show="errors.length > 0">
          <li v-for="(error, index) in errors" :key="index">{{error}}</li>
      </div>
      <form class="signup" >
        <div class="field">
          <label for="name">Name</label>
          <InputText v-model.trim="text"/>
          <!-- <small class="error" v-if="submitted && !text">{{errors}}</small> -->
          <!-- <Button label="Green" icon="pi pi-user" @click="greet" class="p-button-green ml-2"/> -->
        </div>
        <div class="field">
          <label for="mail">Mail</label>
          <InputText v-model="mail"/>
          <!-- <small class="error" v-if="submitted && !text">{{errors}}</small> -->
        </div>
        <Button label="Green" icon="pi pi-user" @click.prevent="greet" class="p-button-green ml-2"/>
      </form>
    </div>
    
  </section>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      text: null,
      mail: null,
      errors:[]
    }
  },
  methods: {
    greet() {
      // this.$toast.add({severity:'info', summary: 'Hello', detail:this.text, life: 3000});
      if (this.text && this.mail) {
        return true
      }
       this.errors = []

      if(!this.text) {
        this.errors.push("field is empty")
      } else if (!this.text.match(/^[a-zA-Z]/)) {
          this.errors.push("This field must begin with a letter")
        } else {
        if(this.text.length < 3) {
          this.errors.push("This field must be at least 3 characters long")
        }  
      }

      if(!this.mail) {
        this.errors.push("email is empty")
      } else {
        if(!this.validEmail(this.mail)) {
          this.errors.push("invalid email")
        }
      }
    },

    validEmail(mail) {
    let re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
    return re.test(mail)
    }

  }
}
</script>

<style scoped>
.signup {
  display: flex;
  justify-content: center;

}
.error {
  color: red;
}
.field {
  margin-right:5px;
}

</style>
