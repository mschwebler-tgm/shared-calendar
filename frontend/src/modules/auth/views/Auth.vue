<template>
  <div>
    <amplify-authenticator :auth-config="authConfig">
      <amplify-sign-out></amplify-sign-out>
    </amplify-authenticator>
  </div>
</template>

<script>
import {AmplifyEventBus, components} from 'aws-amplify-vue';
import {rootApp} from "@/main";

export default {
  name: 'Auth',
  components: {
    ...components,
  },
  data() {
    return {
      authState: this.state,
      unsubscribeAuth: null,
      authConfig: {
        signUpConfig: {
          hiddenDefaults: [
            'phone_number'
          ],
          signUpFields: [
            {
              label: 'First name',
              key: 'name',
              required: true,
              placeholder: 'First name',
              displayOrder: 0,
            },
            {
              label: 'Last name',
              key: 'family_name',
              required: false,
              placeholder: 'Last name',
              displayOrder: 1,
            },
          ],
        },
      },
    }
  },
  created() {
    this.unsubscribeAuth = async (authState, authData) => {
      this.authState = authState;
      if (authState === 'signedIn') {
        rootApp.setUser(authData);
      }
    }
    AmplifyEventBus.$on('authState', this.unsubscribeAuth);
  },
  beforeDestroy() {
    this.unsubscribeAuth();
  }
}
</script>
