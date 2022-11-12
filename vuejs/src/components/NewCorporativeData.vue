<template>
  <div class="q-pa-md" style="max-width: 400px">

    <q-form
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <q-input
        filled
        v-model="name"
        label="Your names *"
        hint="Names"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />

      <q-input
        filled
        v-model="apellidos"
        label="Your apellidos *"
        lazy-rules
        :rules="[ val => val && val.length > 0 || 'Please type something']"
      />


      <q-input
        filled
        type="number"
        v-model="cc"
        label="Identification number *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your cc',
        ]"
      />

      <q-input
        filled
        type="number"
        v-model="cn"
        label="Contact number *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your contact number',
        ]"
      />

      <q-input
        filled
        type="email"
        v-model="emailp"
        label="Personal email *"
        lazy-rules
        :rules="[
          [val => !!val || 'Email is missing', isValidEmail(),]
        ]"
      />
      <q-input
        filled
        type="email"
        v-model="emailc"
        label="Corporative email *"
        lazy-rules
        :rules="[
          val => val !== null && val !== '' || 'Please type your email',
        ]"
      />

      <q-toggle v-model="accept" label="I accept the license and terms" />

      <div>
        <q-btn label="Submit" type="submit" color="primary"/>
        <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
      </div>
    </q-form>

  </div>
</template>
<script>
import { useQuasar } from 'quasar'
import { ref } from 'vue'

export default {
  setup () {
    const $q = useQuasar()

    const name = ref(null)
    const apellidos = ref(null)
    const cc = ref(null)
    const cn = ref(null)
    const emailp = ref(null)
    const emailc = ref(null)
    const accept = ref(false)

    return {
      name,
      apellidos,
      cc,
      cn,
      emailp,
      emailc,
      accept,

      onSubmit () {
        if (accept.value !== true) {
          $q.notify({
            color: 'red-5',
            textColor: 'white',
            icon: 'warning',
            messcc: 'You need to accept the license and terms first'
          })
        }
        else {
          console.log("df");
          $q.notify({
            color: 'green-4',
            textColor: 'white',
            icon: 'cloud_done',
            messcc: 'Submitted'
          })
        }
      },

      onReset () {
        name.value = null
        apellidos.value = null
        cc.value = null
        cn.value = null
        emailc.value = null
        emailp.value = null
        accept.value = false
      },
      isValidEmail (val) {
        const emailPattern = /^(?=[a-zA-Z0-9@._%+-]{6,254}$)[a-zA-Z0-9._%+-]{1,64}@(?:[a-zA-Z0-9-]{1,63}\.){1,8}[a-zA-Z]{2,63}$/;
        return emailPattern.test(val) || 'Invalid email';
      },
    }
  }
}
</script>
