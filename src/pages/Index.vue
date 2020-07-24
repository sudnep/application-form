<template>
  <q-page class="col-md-8">
    <q-card class="my-card ">
      <h5
        class="q-ma-md"
        style="margin-top:20px;color:#333;border-bottom:2px solid #e60000;"
      >
        Student Career Services and Resume Preparation Form
      </h5>
      <q-card-section>
        <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
          <q-input
            filled
            v-model="firstname"
            label="First Name *"
            lazy-rules
            :rules="[val => (val && val.length > 0) || 'Please type something']"
          />
          <q-input filled v-model="middlename" label="Middile Initial" />

          <q-input
            filled
            label="Last Name *"
            v-model="lastname"
            lazy-rules
            :rules="[val => (val && val.length > 0) || 'Please type last name']"
          />
          <q-input
            filled
            label="Student Identification Number *"
            v-model="studentId"
            lazy-rules
            :rules="[
              val =>
                (val && val.length > 0) ||
                'Please enter valid identification number'
            ]"
          />
          <q-input
            filled
            v-model="email"
            suffix="@students.umgc.edu"
            input-class="text-right"
            label-slot
            clearable
            lazy-rules
            :rules="[
              val => (val && val.length > 0) || 'Please type your student email'
            ]"
          >
            <template v-slot:label>
              <div class="row items-center all-pointer-events">
                <q-icon
                  class="q-mr-xs"
                  color="deep-orange"
                  size="24px"
                  name="mail"
                />
                Email *

                <q-tooltip
                  content-class="bg-grey-8"
                  anchor="top left"
                  self="bottom left"
                  :offset="[0, 8]"
                  >eMail address</q-tooltip
                >
              </div>
            </template>
          </q-input>

          <q-input
            filled
            label="Phone *"
            v-model="phone"
            hint="000-000-0000"
            type="tel"
            lazy-rules
            :rules="[
              val => (val && val.length >= 10) || '10 digit Phone is required'
            ]"
          />

          <label for="">Prefered Mode of Communication:</label>
          <q-checkbox v-model="emailMode" label="Email" color="teal" />
          <q-checkbox v-model="phoneMode" label="Phone" color="orange" />
          <q-checkbox v-model="textMode" label="Text" color="cyan" />

          <q-select
            filled
            outlined
            v-model="major"
            :options="majors"
            label="Major *"
            lazy-rules
            :rules="[
              val => (val && val.length > 1) || 'Please select your major'
            ]"
          />
          <q-input
            v-model="graduationdate"
            filled
            type="date"
            hint="Expected Graduation Date *"
            lazy-rules
            :rules="[
              val =>
                (val && val.length > 8) ||
                'Please enter expected graduation date'
            ]"
          />

          <q-input
            v-model="interests"
            filled
            clearable
            type="textarea"
            color="red-12"
            label="Interests"
            hint="Describe your of your career interests and ambition in short."
            :shadow-text="textareaShadowText"
            @keydown="processTextareaFill"
            @focus="processTextareaFill"
          />
          <q-file
            v-model="files"
            label="Upload resume and cover letter"
            filled
            counter
            :counter-label="counterLabelFn"
            max-files="3"
            multiple
            style="max-width: 300px"
          >
            <template v-slot:prepend>
              <q-icon name="attach_file" />
            </template>
          </q-file>

          <q-toggle
            v-model="accept"
            label="I accept the terms and agreements."
          />
          <q-card-actions horizontal>
            <q-btn label="Submit" type="submit" color="primary" />
            <q-btn
              label="Reset"
              type="reset"
              color="primary"
              flat
              class="q-ml-sm"
            />
          </q-card-actions>
        </q-form>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script>
export default {
  data() {
    return {
      firstname: null,
      middlename: null,
      lastname: null,
      emailMode: null,
      phoneMode: null,
      textMode: null,
      email: null,
      studentId: null,
      graduationdate: null,
      phone: null,
      files: null,
      accept: false,
      major: null,
      interests: null,
      majors: [
        "Computer Science",
        "Natural Science",
        "BioTechnology",
        "Physical Science",
        "Cybersecurity",
        ""
      ]
    };
  },

  methods: {
    counterLabelFn({ totalSize, filesNumber, maxFiles }) {
      return `${filesNumber} files of ${maxFiles} | ${totalSize}`;
    },
    onSubmit() {
      if (this.accept !== true) {
        this.$q.notify({
          color: "red-5",
          textColor: "white",
          icon: "warning",
          message: "You need to accept the agreements and terms first"
        });
      } else {
        this.$q.notify({
          color: "green-4",
          textColor: "white",
          icon: "cloud_done",
          message: "Submitted"
        });
      }
    },

    onReset() {
      this.firstname = null;
      this.lastname = null;
      this.major = false;
      this.phone = false;
      this.email = false;
      this.middlename = false;
    }
  }
};
</script>
