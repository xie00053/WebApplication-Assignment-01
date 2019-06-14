<template>
  <div id="app">

    <img alt="Vue logo" src="./assets/smile.png" />
    <HelloWorld msg="Welcome to my online contact form." />

<!-- //  Button for open the form dialog  //-->   
    <el-button type="primary" @click="myForm = true">Click to open the form</el-button>   


<!-- //  Dialog for the submitted imformation // -->
    <el-dialog title="Your message was submitted. Thank you!" :visible.sync="dialogFormVisible">
      <el-form class="infoDialog" label-width="160px">
        <el-form-item label="Your Name: ">{{form.fristName}} {{form.lastName}}</el-form-item>
        <el-form-item label="Your Email: ">{{form.email}}</el-form-item>
        <el-form-item label="Your Subject: ">{{form.subject}}</el-form-item>
        <el-form-item label="Your Message: ">{{form.desc}}</el-form-item>
        <el-form-item label="I agree to the terms: "> Ture </el-form-item>
      </el-form>
    </el-dialog>

<!-- //  The dialog of the form  //-->
    <el-dialog title="Please fill your information and message here." :visible.sync="myForm">

      <!-- the form start from here -->
      <el-form :model="form" :rules="rules" ref="form" label-width="120px">

        <!-- First Name -->
        <el-form-item prop="fristName" label="Frist Name">
          <el-input placeholder="Frist Name" v-model="form.fristName"></el-input>
        </el-form-item>

        <!-- Last Name -->
        <el-form-item prop="lastName" label="Last Name">
          <el-input placeholder="Last Name" v-model="form.lastName"></el-input>
        </el-form-item>

        <!-- Email --> 
        <el-form-item prop="email" label="Email">
          <el-input placeholder="Your Email" v-model="form.email"></el-input>
        </el-form-item>
        
        <!-- Subject Title -->
        <el-form-item prop="subject" label="Subject Title">
        <el-input placeholder="Subject Title (no more than 30 words)" v-model="form.subject"></el-input>
        </el-form-item>
        
        <!-- Description -->
        <el-form-item label="Message">
        <el-input type="textarea" placeholder="type message here" v-model="form.desc"></el-input>
        </el-form-item>
        
        <!-- Checkbox for agreement -->
        <el-form-item prop="agreement">
            <el-checkbox name="agreement" v-model="form.agreement">I have read and agree to the terms</el-checkbox>
        </el-form-item>

      </el-form>
    
        <!-- Submit button -->
        <el-button type="primary" @click="submitForm('form')">Submit</el-button>
      
    </el-dialog> 
  </div>
</template>

<script>

// -----import component -----//
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "app",
  components: {
    HelloWorld
  },

  data() {
      return {
        myForm: false,
        dialogFormVisible: false,
        formDialog: false,
        form: {
          fristName: '',
          lastName: '',
          email: '',
          subject: '',
          desc: '',
          agreement: [],
        },

        // Rules for the form:--------
        // first name, last name, email, subject can not be empty;
        // email should have the correct format; Subject can not more than 30 words.
        rules: {
          fristName:[
            {required: true, message: 'Please input Frist Name', trigger: 'blur'}
          ],
          lastName:[
            {required: true, message: 'Please input Last Name', trigger: 'blur'}
          ],
          email:[
            { required: true, message: 'Please input email address', trigger: 'blur' },
            { type: 'email', message: 'Please input correct email address', trigger: ['blur', 'change'] }
          ],
          subject:[
            { required: true, message: 'Please input the subject', trigger: 'blur' },
            { min:0, max: 30, message: 'Subject title cannot be more than 30 words', trigger: ['blur', 'change'] }
          ],

          agreement: [
            { required: true, message: 'Please agree to the terms', trigger: 'change' }
          ],
        }
      };
    },

// ---method to check if the form can be submitted----//
    methods: {
      submitForm(form) {
        this.$refs[form].validate((valid) => {
          if (valid) {
            this.dialogFormVisible = true;
            // alert('submit!');
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
    }
};

</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  // -------Style for the from-------

  margin-top: 60px;
    .el-checkbox {
      margin-top: 1rem;
    }
    .el-form {
      margin: auto;
      width:70%;
    }

    .infoDialog {
      text-align: left;

      .el-form-item__label {
        font-weight: 600;
        text-align: left;
       }
    }

    
  
}

</style>
