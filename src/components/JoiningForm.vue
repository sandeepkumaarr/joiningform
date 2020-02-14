<template class="">
  <v-container class="mt-5 mb-12" >
    <h2 class="text-center display-1 mb-12 mt-8 red--text darken-1">SocialBeat Teams Page Details Form</h2>
    <v-row no-gutters justify="center">
      <v-col
        cols="10"
        sm="10"
        md="6"
        lg="5"
      >
        <v-form @submit="formSubmit" id="form">
         <v-text-field
            v-model="name"
            :label="nameinput.namelabel"
            :hint="nameinput.namehint"
            :outlined=true
            :clearable=true
            color="indigo darken-1"
            required
          ></v-text-field>

         <v-text-field
            v-model="email"
            :label="emailinput.emaillabel"
            :hint="emailinput.emailhint"
            :outlined=true
            :clearable=true
            color="indigo darken-1"
            type="email"
            required
          ></v-text-field>

          <v-select
          v-model="team"
          :items="teaminput.teamitems"
          :label="teaminput.teamlabel"
          :outlined=true
          :clearable=true
          color="indigo darken-1"
          ></v-select>

          <v-select
          v-model="designation"
          :items="designationinput.designationitems"
          :label="designationinput.designationlabel"
          :outlined=true
          :clearable=true
          color="indigo darken-1"
          ></v-select>

          <v-text-field
            v-model="designation_text"
            :label="jobprofileinput.jobprofilelabel"
            :hint="jobprofileinput.jobprofilehint"
            :outlined=true
            :clearable=true
            color="indigo darken-1"
            required
          ></v-text-field>

            <v-textarea
            v-model="write_up"
            clearable
            :auto-grow=true
            label="Write up about yourself"
            :outlined=true

          ></v-textarea>

          <!-- <v-file-input
            type="file"
            @click="processFile($event)"
            accept="image/png, image/jpeg"
            label="Pick an avatar"
            prepend-icon="mdi-camera"
            :outlined=true

          ></v-file-input> -->

            <v-image-input
              v-model="avatar"
              clearable
              image-format="jpeg"
              uploadIcon="Pick your avatar"
            />
          <v-btn class="mt-5"
            type="submit"
            color="success"
            block
            x-large
          >
          SUBMIT
          </v-btn>

          
        </v-form>
      </v-col>
    </v-row>
  </v-container>
</template>
     
<script>
export default {
  mounted() {
    console.log("Component mounted.");
  },
  data() {
    return {
      name: "",
      email:"",
      team:"",
      designation:"",
      designation_text:"",
      write_up: "",
      avatar: "",
      nameinput:{
        namelabel: 'Name',
        namehint: 'Please enter your full name',
      },
      emailinput:{
        emaillabel: 'Email',
        emailhint: 'Please enter your official email',
      },

      teaminput:{
        teamlabel:'Select Team',
        teamitems:['Web','Design','Video','SEO','Content','Tech','Analytics','Ads','HR','Accounts','Social','Business Development','Influencer'],
      },

      designationinput:{
        designationlabel:'Select Designation',
        designationitems:['Head','EVP','AVP','Sr Manager','Manager','Lead','Sr Associate', 'Associate'],
      }, 

      jobprofileinput:{
        jobprofilelabel:"Job Profile",
        jobprofilehint: 'Please enter your job profile',
      }

    };
  },
  methods: {
    formSubmit(e) {
      e.preventDefault();
            
      let currentObj = this;
      this.axios
        .post("http://leave.socialbeat.in/api/team/create-user", {
          
          name:this.name,
          email:this.email,
          team:this.team,
          designation:this.designation,
          designation_text:this.designation_text,
          write_up: this.write_up,
          avatar: this.avatar,
        })
        .then(function(response) {
          currentObj.output = response.data;
          console.log('success');
        })
        .catch(function(error) {
          currentObj.output = error;
        });
    },
  }
};
</script>